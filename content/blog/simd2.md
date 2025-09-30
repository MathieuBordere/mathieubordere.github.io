+++
title = "Contributing to Coreutils."
date = 2025-09-30
+++

In the [previous blog post](/blog/simd) we briefly looked at the AVX2
implementation of `wc -l` in Coreutils. I have a Ryzen 9 7900 that supports
AVX512 instructions, so I figured it would be useful and fun to try to
contribute an AVX512 version of the linecounting algorithm to Coreutils.

Porting the code and build instructions was quite straightforward, the only hurdle was getting a [copyright assignment](https://github.com/coreutils/coreutils/blob/67e9068c5f5fdae5666279717a4c19bdfe5c21de/HACKING#L469) from the [FSF](https://www.fsf.org/).
I was a bit worried when someone told me that

> "no one at the FSF seems to watch the email for requesting one."

All in all, I received a quick reply and [the patch](https://github.com/coreutils/coreutils/commit/67e9068c5f5fdae5666279717a4c19bdfe5c21de) could finally land!

Thanks to the Coreutils maintainers who were very prompt, friendly and
professional!
