# Digivas Development

SRE / platform engineering. I audit and repair the tools that automation depends on — especially
MCP servers, where a mis-wired tool fails silently instead of loudly.

**→ [MCP Server Audit service](https://digivasserver-ai.github.io/mcp-audit-toolkit/)** ·
[sample audit report](https://github.com/digivasserver-ai/mcp-audit-toolkit/blob/main/docs/SAMPLE-AUDIT.md)

## Recent work · October 2026

- Published **[durable-sh](https://github.com/digivasserver-ai/durable-sh)**, an MIT-licensed Bash library for atomic writes, parent-shell retries, Git lock handling and process supervision. Its local test suite passes **18/18** tests.
- Proposed an **[IzzyOnDroid repository hub](https://github.com/DUpdateSystem/UpgradeAll-rules/pull/213)** for UpgradeAll's app-discovery rules. The generated configuration was checked; app-level behaviour has not been tested. The PR is open.
- Investigated **[ARM64 Android builds for UpgradeAll](https://github.com/DUpdateSystem/UpgradeAll/pull/529)**: a Kotlin module compiled on-device with Termux's native `aapt2`. A full APK/Rust build has **not** passed; the installed NDK host compilers are x86_64 binaries. The build-guide PR is open and still needs validation.

## What I do

**MCP server audits.** I connect to an MCP server the way a real client does, call every read-only
tool, and cross-check each answer against independent ground truth (`rpm -ql`, `/proc/uptime`, `df`).
Then I compare each tool's advertised schema against the signature its dispatcher actually calls.

Three defect classes show up repeatedly:

| class | symptom | detection |
|---|---|---|
| **Dispatcher drift** | schema advertises arguments the function never accepted — `TypeError` on every call | static schema-vs-signature diff |
| **Platform path drift** | paths hard-coded to the wrong distribution (e.g. `/etc/zypper/zypper.conf` where openSUSE ships `/etc/zypp/zypper.conf`) | run it on the real platform, verify the answer |
| **Shell-dependency drift** | command detection relies on an external `which` that minimal images may lack | run it on a minimal image; use `shutil.which` in Python |

Findings ship as **PRs with fixes and regression tests written red first** — not as issue dumps.

## Work

| repo | what it demonstrates | licence |
|---|---|---|
| **[durable-sh](https://github.com/digivasserver-ai/durable-sh)** | Tested shell primitives for recoverable writes, retries, Git operations and daemon liveness in the Android/Termux lab. | MIT |
| **[mcp-audit-toolkit](https://github.com/digivasserver-ai/mcp-audit-toolkit)** | Fingerprint-based credential leak scanner (`PUBLISHED` / `LOCAL` / `CLEAN`), MCP stdio health probe, and the written methodology. Has a [live service page](https://digivasserver-ai.github.io/mcp-audit-toolkit/). | MIT |
| **[demo-emulator](https://github.com/digivasserver-ai/demo-emulator)** | Headless Android emulator on GitHub Actions driving a DroidGuard/microG demo without KVM — wrapped around an open protocol investigation where a byte-identical rebuild still changed runtime behaviour. | MIT |
| **[puter-lab](https://github.com/digivasserver-ai/puter-lab)** | Full-stack on Puter: React 19 + TypeScript on Puter hosting plus a serverless worker (`/ping`, `/echo/:msg`, `/health`), both deployed from GitHub Actions on push. Build on one platform, deploy onto someone else's, keep URLs stable. | MIT |
| **[PROXY-JOURNAL](https://github.com/digivasserver-ai/PROXY-JOURNAL)** | Portable AI/LLM development journal — identity, memory and progress for any model, so work never restarts from a blank slate. | MIT |
| **[ci-repro](https://github.com/digivasserver-ai/ci-repro)** | Gradle CI reference: build, artifact, release, dependency-submission and CodeQL workflows with REUSE-compliant license headers. | Apache-2.0 |
| **[Dev-Team-Projects](https://github.com/digivasserver-ai/Dev-Team-Projects)** | USB boot system on Ventoy with an LLM-assisted boot assistant; workstation optimiser. | MIT |

These are public repositories; the audit toolkit also has a live service page. Not every repository
is a deployed application.

## Evidence

Three open pull requests against a live community MCP server
([`chrisjohntapp/suse-mcp`](https://github.com/chrisjohntapp/suse-mcp)), each with fixes **and**
regression tests:

| PR | fix | tests |
|---|---|---|
| [#1](https://github.com/chrisjohntapp/suse-mcp/pull/1) | SUSE paths for `zypper.conf`, merged RPM macro sources with host-arch detection | 4 |
| [#2](https://github.com/chrisjohntapp/suse-mcp/pull/2) | dispatcher-to-signature mapping for the consolidated tools | 16 |
| [#3](https://github.com/chrisjohntapp/suse-mcp/pull/3) | `shutil.which` instead of the external `which` binary | 3 |

In that audit, 3 of 22 advertised tools raised `TypeError` on every call, 6 more degraded to
"command not found" on the target platform, and 2 config readers returned nothing at all. The
server's own health check reported itself healthy throughout. After the fixes: **253 tests passing**.

## Environment

Primary workspace is an **aarch64 openSUSE Tumbleweed proot terminal on Android** — no systemd, no
display server, several coreutils absent. That constraint is useful: it surfaces the exact
assumptions that break on minimal images, which is where most "works on my machine" defects live.

Memory, maps and audit trail are versioned in a private repo mirrored to GitHub and GitLab, with
automated integrity checks — the kind of setup that survives a device wipe.

## Notes

Findings are reported as correctness issues unless they have genuine security impact. A tool that
always throws is a bug; it is not a CVE, and I do not dress it up as one.
