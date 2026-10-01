# DigiVas Development

SRE / platform engineering. I audit and repair the tools that automation depends on — especially MCP servers, where a mis-wired tool fails silently instead of loudly.

## What I do

**MCP server audits.** I connect to an MCP server the way a real client does, call every read-only tool, and cross-check each answer against independent ground truth (`rpm -ql`, `/proc/uptime`, `df`). Then I compare each tool's advertised schema against the signature its dispatcher actually calls.

Two defect classes show up repeatedly:

| class | symptom | detection |
|---|---|---|
| **Dispatcher drift** | schema advertises arguments the function never accepted — `TypeError` on every call | static schema-vs-signature diff |
| **Platform path drift** | paths hard-coded to the wrong distribution (e.g. `/etc/zypper/zypper.conf` where openSUSE ships `/etc/zypp/zypper.conf`) | run it on the real platform, verify the answer |
| **Shell-dependency drift** | detects binaries with `which` or `shutil` in ways minimal images do not support | run it in a container |

Findings ship as **PRs with fixes and regression tests written red first** — not as issue dumps.

## Current work

- **[mcp-audit-toolkit](https://github.com/digivasserver-ai/mcp-audit-toolkit)** — fingerprint-based credential leak scanner (`PUBLISHED` / `LOCAL` / `CLEAN` classification), stdio health probe for MCP servers, plus the audit methodology. MIT licensed.
- **[suse-mcp](https://github.com/chrisjohntapp/suse-mcp/pull/1)** contributions — three open PRs against a community SUSE/openSUSE MCP server: correct distro paths, merged RPM macro sources with host-arch detection, dispatcher argument mapping, and `shutil.which` command detection. 23 new tests. Suite: 253 passing.

## Environment

Primary workspace is an **aarch64 openSUSE Tumbleweed proot terminal on Android** — no systemd, no display server, several coreutils absent. That constraint is useful: it surfaces the exact assumptions that break on minimal images, which is where most "works on my machine" defects live.

Memory, maps and audit trail are versioned in a private repo mirrored to GitHub and GitLab, with automated integrity checks — the kind of setup that survives a device wipe.

## Notes

Findings are reported as correctness issues unless they have genuine security impact. A tool that always throws is a bug; it is not a CVE, and I do not dress it up as one.
