+++
title = "Test Code Highlighting"
date = 2025-09-17
+++

This is my first blog post.

```rust,linenos,hl_lines=1 3-5 9
#[snafu(visibility(pub(crate)))]
pub enum DnsError {
    #[snafu(transparent)]
    Timeout { source: tokio::time::error::Elapsed },
    #[snafu(display("No response"))]
    NoResponse {},
    #[snafu(display("Resolve failed ipv4: {ipv4}, ipv6 {ipv6}"))]
    ResolveBoth {
        ipv4: Box<DnsError>,
        ipv6: Box<DnsError>,
    },
    #[snafu(display("missing host"))]
    MissingHost {},
    #[snafu(transparent)]
    Resolve {
        source: hickory_resolver::ResolveError,
    },
    #[snafu(display("invalid DNS response: not a query for _iroh.z32encodedpubkey"))]
    InvalidResponse {},
}
```
