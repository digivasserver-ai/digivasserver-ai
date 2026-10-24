# Digivas Development

**AI systems · Kotlin/Android · reliable developer tooling**

**[digivasserver-ai.github.io](https://digivasserver-ai.github.io/)** · [X](https://x.com/DIGIvasCoNNeCt) · [divivas.server@gmail.com](mailto:divivas.server@gmail.com)

I work on practical tools for AI-assisted development and Android. My focus is on durable agent memory, clear security boundaries, reproducible builds, and small fixes backed by tests. I separate working prototypes from shipped features — and I write down what I could not verify.

## Start here

- **[durable-sh](https://github.com/digivasserver-ai/durable-sh)** — shell primitives for environments that kill short-lived processes: inherited signal immunity, atomic writes, parent-shell retries, git lock recovery. MIT, 18/18 tests, [tagged releases](https://github.com/digivasserver-ai/durable-sh/releases).
- **[Signal 36: the Android profiler that kills your shell scripts](https://digivasserver-ai.github.io/signal-36.html)** — why `git`, `python3` and `rpm` randomly exit 164, with the measured kill rates and the one-line fix.
- **[mcp-audit-toolkit](https://github.com/digivasserver-ai/mcp-audit-toolkit)** — audits MCP servers the way a client talks to them: credential-fingerprint leak scanning and stdio health probes.

## AI systems

- **[PROXY-JOURNAL](https://github.com/digivasserver-ai/PROXY-JOURNAL)** — a portable JavaScript CLI for agent identity, memory, progress logs and context packs across LLM sessions, with integrity and audit features.
- **[Memanto security fix](https://github.com/moorcheh-ai/memanto/pull/1911)** — merged upstream change protecting browser-cookie memory and UI routes from attacker-origin Host headers, with regression tests. The agent's memory is part of its security boundary.
- **[Puter AI chat example](https://github.com/digivasserver-ai/puter-lab/blob/main/site/src/examples/aiChat.tsx)** — a React/TypeScript example calling `puter.ai.chat` in a [hosted integration lab](https://github.com/digivasserver-ai/puter-lab) that also deploys a serverless worker from CI.

I also run a private Android/Termux assistant lab with versioned state, audit logs and device integrations. It is an ongoing workspace, not a public product.

## Kotlin & Android

- **[microG remote DroidGuard experiment](https://github.com/microg/GmsCore/pull/3750)** — Kotlin-side multi-step session work and a reference server. A [mirror CI run](https://github.com/digivasserver-ai/ci-repro/actions/runs/33248919469) passed Debug and Release builds. The upstream PR closed unmerged; an on-device Play Integrity verdict was **not** verified.
- **[UpgradeAll ARM64 build investigation](https://github.com/DUpdateSystem/UpgradeAll/pull/529)** — compiled a Kotlin module on an Android ARM64 phone using Termux's native `aapt2`. The build-guide PR is open; a full APK/Rust build has **not** passed on this host.
- **[demo-emulator](https://github.com/digivasserver-ai/demo-emulator)** — headless Android emulator workflow on GitHub Actions for microG demonstrations without KVM.

My daily test environment is Android 16 with an aarch64 openSUSE Tumbleweed proot terminal, ADB and Shizuku. It exposes platform assumptions that desktop-only builds can miss.

## Writing

- **[Signal 36: the Android profiler that kills your shell scripts](https://digivasserver-ai.github.io/signal-36.html)** — root cause, measurements, fix, and the four things still unexplained.
- **[Building Android apps on an ARM64 phone](https://digivasserver-ai.github.io/arm64.html)** — the `aapt2` override, the compileSdk 37 hand-install, and the Gradle traps that cost the most time.

## Upstream

- **[SUSE MCP fixes](https://github.com/chrisjohntapp/suse-mcp/pulls?q=is%3Apr+author%3Adigivasserver-ai)** — three proposed changes to the SUSE MCP server: command detection via `shutil.which` instead of the external `which` binary, wiring the consolidated tools to their real function signatures, and reading the actual RPM macro sources. Open, not merged.

## A note on older pull requests

Some pull requests from August–September 2026 were bounty work against small repositories. Several are still open, and one target repository has since been deleted. That phase is over: current work is security and build fixes in projects I actually use — memanto, microG, UpgradeAll and suse-mcp — plus the repositories above.

## Contact

Email [divivas.server@gmail.com](mailto:divivas.server@gmail.com) for security reports or collaboration. Vulnerabilities should go there rather than into a public issue; see each repository's `SECURITY.md`.
