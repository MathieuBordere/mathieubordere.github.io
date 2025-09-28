+++
title = "Contributing to coreutils."
date = 2025-09-28
+++

In the [previous blog post](/blog/simd/) we briefly looked at the AVX2
implementation of newline counting in coreutils' wc. As I have a Zen 4 processor
that supports AVX512, and wc was lacking an AVX512 implementation of the newline
counting algorithm I thought it would be useful to contribute to the project and
write an AVX512 implementation.

Long story short, after porting the code to use AVX512, adapting the build system and
the tests, it was time to submit the patch to the team. The coreutils team is
very friendly, answers mails promptly, no complaints, they seem to be very
professional. The problem however is that coreutils requires a copyright
assignment, where the user transfers copyright (or gives permission to, I don't
really know) to the [FSF, the Free Software Foundation](https://www.fsf.org/). The ritual requires
filling out a form and emailing it to the FSF, which is all fine, were it not
for the fact that:
> "no one at the FSF seems to watch the email for requesting
one."

Just great. What a way to chase away new contributors.

It's been only 4 days since I sent a mail, but I'm not expecting a reply soon.
Anyway, I hope I can update this post with the news that someone started
watching the email for requesting copyright assignments at the FSF.
