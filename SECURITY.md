# Security policy

The projects of the physical-edge-native organization are research prototypes. Some of them (for example the
firmware and network protocol of dyne) have no authentication or encryption and are meant only for isolated
test networks; each repository's README or `SECURITY.md` says so where it applies.

## Reporting a vulnerability

Please **do not open a public issue** for a security problem.

Report it privately through GitHub: open the repository, go to the **Security** tab and press
**Report a vulnerability** (private vulnerability reporting). Only the maintainer can see the report.

Please include what is affected, how to reproduce it, and what an attacker could do. You will get a reply,
usually within a week.

If you committed a secret (a password, a key, a token) by mistake, report it the same way, and change the secret
at once: removing it in a later commit does not remove it from the history.
