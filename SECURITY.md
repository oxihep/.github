# Security policy

## Supported versions

Fixes go into the latest release of each crate (the most recent git tag of
its repository). Older tags are not patched; update to the latest.

## Reporting a vulnerability

Please do not open a public issue. Report it privately through GitHub: in the
repository concerned, open the **Security** tab and choose **Report a
vulnerability**. Include what is affected, how to reproduce it (a crafted
ROOT file, for example), and what it leads to: a crash, a hang, unbounded
memory, or a wrong read.

You will get an answer within a week. Once a fix is released, the advisory is
published with credit to you, unless you prefer otherwise.

oxiroot reads files that may come from anywhere, so its readers are built
not to panic or allocate without bound on malformed input, and they are
fuzzed weekly. A crafted file that crashes a reader, hangs it, or makes it
allocate far beyond the file's size is a vulnerability worth reporting.
