# Digivas Development

**AI systems · Kotlin/Android · reliable developer tooling**

I work on practical tools for AI-assisted development and Android. My focus is on durable agent memory, clear security boundaries, reproducible builds, and small fixes backed by tests. I separate working prototypes from shipped features.

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

## Other tooling

- **[durable-sh](https://github.com/digivasserver-ai/durable-sh)** — shell primitives for atomic writes, retries, Git recovery and process supervision; 18/18 local tests pass.
- **[MCP audit toolkit](https://github.com/digivasserver-ai/mcp-audit-toolkit)** — a leak scanner and MCP health probe. Related [SUSE MCP fixes](https://github.com/chrisjohntapp/suse-mcp/pulls?q=is%3Apr+author%3Adigivasserver-ai) are proposed upstream, not merged.
