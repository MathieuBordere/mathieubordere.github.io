+++
title = "A gentle introduction to SIMD."
date = 2025-09-18
+++

A few weeks ago I was reading up on the [one billion row challenge](https://github.com/gunnarmorling/1brc) and was wondering what the fastest way
would be to read a file from disk. For comparison I decided it would be
interesting to find out how `wc` does it on my Fedora 42 workstation. Turns out
`wc` just uses `read` but with a buffersize of 256KiB, a value that seems to be [optimized for an
average
system](https://github.com/coreutils/coreutils/blob/dc30eab3146163be18b70d8d5fed63706b6a4110/src/ioblksize.h#L25).

My attention immediately diverted to the actual implementation that uses AVX2
when available, I've never really taken a closer look at SIMD instructions
before and decided it was the right moment as the code didn't look daunting.

```c,linenos,hl_lines=7 21 22 23
extern struct wc_lines
wc_lines_avx2 (int fd)
{
  intmax_t lines = 0;
  intmax_t bytes = 0;

  __m256i endlines = _mm256_set1_epi8 ('\n');

  while (true)
    {
       __m256i avx_buf[IO_BUFSIZE / sizeof (__m256i)];
      ssize_t bytes_read = read (fd, avx_buf, sizeof avx_buf);
      if (bytes_read <= 0)
        return (struct wc_lines) { bytes_read == 0 ? 0 : errno, lines, bytes };

      bytes += bytes_read;
      __m256i *datap = avx_buf;

      while (bytes_read >= 32)
        {
           __m256i to_match = _mm256_load_si256 (datap);
           __m256i matches = _mm256_cmpeq_epi8 (to_match, endlines);
           int mask = _mm256_movemask_epi8 (matches);
           lines += __builtin_popcount (mask);
           datap += 1;
           bytes_read -= 32;
        }

      /* Finish up any left over bytes */
      char *end = (char *) datap + bytes_read;
      for (char *p = (char *) datap; p < end; p++)
        lines += *p == '\n';
    }
}
```

The algorithm is pretty simple. It first prepares a 256 bit buffer with 32 `\n` values at L7,
then reads a chunk of data, and as long as there is data to read, it loads 256
bits of the data at L21 and compares the data with the buffer of newlines using
`_mm256_cmpeq_epi8`. This sets the corresponding bits of the matches buffer to all
1's in case a data byte is a newline or all 0's in case it's not.

To count the number of lines, `_mm256_movemask_epi8` creates a mask from the most significant bit of each
byte of the source vector and stores the result in the returned value, in short it transforms `1111 1111` (a newline match)
into `1000 0000`, and leaves `0000 0000` alone. Now what remains is counting the
number of set bits in the mask with `__builtin_popcount`.

That's it! The remainder is some accounting when there's leftover data that is
too small to fit an AVX2 instruction. Now, that was a gentle introduction, wasn't it?
