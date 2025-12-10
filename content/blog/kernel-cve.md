+++
title = "kernel-cve"
date = 2025-12-10
+++

Not too long ago I learned via [this lwn post](https://lwn.net/Articles/1000871/) that stable and supported
Linux Kernels contain a lot of unpatched CVEs, that will never be patched.
In hindsight, this makes total sense of course, as the codebase evolves,
patches get harder and harder to apply and there are only so many hands working on
the maintenance of the Linux Kernels.

As I'm surely not the only that is or was surprised by this, I've decided to
try to make this fact more visible by creating a database of all Linux Kernel versions since
2.6.12 and all the CVEs that are currently assigned to them. You can find the
result at [kernelcve.com](https://kernelcve.com).

The site is currently running on a pretty weak Azure VM (in Europe) as I'm not expecting
enormous amounts of traffic, but it feels very snappy, I'm pretty happy with it!

There's an API, you can read about its usage in the [Docs](https://www.kernelcve.com/docs.html).

So, take a look at that ancient Linux Version running on your home router and
find out all of its unpatched security issues :-)
