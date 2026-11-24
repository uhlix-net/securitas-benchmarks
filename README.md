# Securitas benchmarks

CIS benchmark packages for [Securitas](https://github.com/uhlix-net/securitas), built from the **official CIS
benchmark documents**, so Securitas's compliance scans follow the benchmark exactly as CIS publishes it.

Each package (`<name>-<CIS version>.zip`) holds:

- `securitas-benchmark.json`: every recommendation as the CIS document states it: ID, title, **Automated** or
  **Manual**, and profiles (Level 1 / Level 2, Server / Workstation), plus the section names, the document's title,
  version and date, and the SHA-256 of the PDF it was read from. Only these facts are taken from the document.
- `audit/`: the checks that test the rules (Goss), unchanged from their source, pinned to one commit.
- `SOURCES.txt` (where both came from, and which Automated recommendations have no check yet) and `LICENSE.md`.

Packages are built with [`tools/cis_package.py`](https://github.com/uhlix-net/securitas/blob/main/tools/cis_package.py),
which stops when the checks name a rule the document does not have.

## Packages

| Package | CIS document | Checks | Rules | Download |
|---|---|---|---|---|
| RHEL9-CIS-2.0.0 | CIS Red Hat Enterprise Linux 9 Benchmark v2.0.0 (06-24-2024) | Ansible-Lockdown RHEL9-CIS-Audit `d9c0f2c` (branch benchmark_v2.0.0) | 297: 275 Automated, 22 Manual | [RHEL9-CIS-2.0.0.zip](https://github.com/uhlix-net/securitas-benchmarks/releases/download/RHEL9-CIS-2.0.0-r1/RHEL9-CIS-2.0.0.zip) |

SHA-256 of RHEL9-CIS-2.0.0.zip: `84d34c4e918b3cedf5dedf88ed3b6bb5d23bb23f02f1e6778c2f36d4508182eb`

Automated recommendations the checks do not cover yet (they show as "No automated check" in Securitas):
4.2.2, 4.3.1, 4.3.4, 6.3.3.6.

## Using a package

In Securitas (0.6.0 or later): **Compliance → Benchmarks**, upload the zip, and make it active for its operating
system. Its checks become the benchmark's audit content, which Securitas copies to each Linux host at scan time
(the [Securitas agent](https://github.com/uhlix-net/securitas#installing-the-agent-on-linux-targets-compliance-checks)
runs them). Exceptions are kept per benchmark name (e.g. RHEL9-CIS), so they carry over to newer versions.

## Licence

The rule data in each package is derived from CIS Benchmarks by the Center for Internet Security, Inc., licensed
under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), and is shared under the same licence
for **non-commercial use**. The checks in `audit/` keep their own licence (Ansible-Lockdown: MIT), included in each
package. CIS has not reviewed or endorsed these packages. CIS® and CIS Benchmarks™ are trademarks of the Center for
Internet Security, Inc. See [LICENSE](LICENSE).
