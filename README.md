# Digivas Development

**AI memory systems · Kotlin/Android · reliable developer tooling**
Building in the open as **Digivasconnect PTY (LTD)** — South Africa.

**[digivasserver-ai.github.io](https://digivasserver-ai.github.io/)** · [X](https://x.com/DIGIvasCoNNeCt) · [digivas.server@gmail.com](mailto:digivas.server@gmail.com)

## Intention

I build things that remember, that survive hostile environments, and that can be
verified by anyone who clones them. Three commitments:

1. **Durable agent memory.** An AI that only exists during a conversation is a
   tool. One that observes its own state, corrects itself, and persists across
   sessions is infrastructure. I am building that layer in the open.
2. **Evidence over claims.** Every line in my docs is tagged `VERIFIED`,
   `RECORDED`, or `DEFECT`. I write down what I could not verify, and I separate
   working prototypes from shipped features.
3. **Community first.** Everything here is MIT/Apache-2.0 unless a repo says
   otherwise. I am looking for funding and collaborators who want durable,
   testable open-source tooling — reach me by email.

## Start here

- **[Self-maintaining AI memory layer](https://digivasserver-ai.github.io/ai-memory-layer.html)** — an AI that reads its own state, writes observations with confidence scores, evaluates past predictions, forms reasoning chains, and commits itself to git. Runs autonomously as a supervised service on a phone. Guardrails (scope, rate, decency, audit, kill switch) are built in, not retrofitted.
- **[durable-sh](https://github.com/digivasserver-ai/durable-sh)** — shell primitives for environments that kill short-lived processes: inherited signal immunity, atomic writes, parent-shell retries, git lock recovery. MIT, 18/18 tests, [tagged releases](https://github.com/digivasserver-ai/durable-sh/releases).
- **[Signal 36: the Android profiler that kills your shell scripts](https://digivasserver-ai.github.io/signal-36.html)** — why `git`, `python3` and `rpm` randomly exit 164, with the measured kill rates and the one-line fix.
- **[mcp-audit-toolkit](https://github.com/digivasserver-ai/mcp-audit-toolkit)** — audits MCP servers the way a client talks to them: credential-fingerprint leak scanning and stdio health probes.

## AI systems

- **Self-maintaining memory layer (v2)** — 10 observation types, a reasoning layer that connects observations into causal/trend/context chains, a goals system, external input ingestion, and self-evaluation that writes corrections when a prediction fails. Open write-up above; the code lives in my lab and is being prepared for a public release.
- **[PROXY-JOURNAL](https://github.com/digivasserver-ai/PROXY-JOURNAL)** — a portable JavaScript CLI for agent identity, memory, progress logs and context packs across LLM sessions, with integrity and audit features.
- **[Memanto security fix](https://github.com/moorcheh-ai/memanto/pull/1911)** — merged upstream change protecting browser-cookie memory and UI routes from attacker-origin Host headers, with regression tests. The agent's memory is part of its security boundary.
- **[Puter AI chat example](https://github.com/digivasserver-ai/puter-lab/blob/main/site/src/examples/aiChat.tsx)** — a React/TypeScript example calling `puter.ai.chat` in a [hosted integration lab](https://github.com/digivasserver-ai/puter-lab) that also deploys a serverless worker from CI.

I also run a private Android/Termux assistant lab with versioned state, audit logs and device integrations. It is an ongoing workspace, not a public product.

## Kotlin & Android

- **[microG remote DroidGuard experiment](https://github.com/microg/GmsCore/pull/3750)** — Kotlin-side multi-step session work and a reference server. A [mirror CI run](https://github.com/digivasserver-ai/ci-repro/actions/runs/33248919469) passed Debug and Release builds. The upstream PR closed unmerged; an on-device Play Integrity verdict was **not** verified.
- **[UpgradeAll ARM64 build investigation](https://github.com/DUpdateSystem/UpgradeAll/pull/529)** — compiled a Kotlin module on an Android ARM64 phone using Termux's native `aapt2`. The build-guide PR is open; a full APK/Rust build has **not** passed on this host.
- **[demo-emulator](https://github.com/digivasserver-ai/demo-emulator)** — headless Android emulator workflow on GitHub Actions for microG demonstrations without KVM.

My daily test environment is Android 16 with an aarch64 openSUSE Tumbleweed proot terminal, ADB and Shizuku. It exposes platform assumptions that desktop-only builds can miss.

## Prototyping

Local simulators for exploring how payment and messaging flows behave — test
harnesses only, they never touch a live gateway or bypass any authorization:

- **Checkout-flow simulator** — reproduces a real Peach Payments hosted checkout
  (validated against a live R360.00 checkout captured from a WebView) for
  working out UI and error-path behaviour offline.
- **NFC / wallet terminal simulators** — model tap-to-pay and stored-balance
  flows so the interface and state machine can be exercised without hardware.
- **MCP read loop** — measures MCP tool-call caching (~100x amplification on a
  repeated read pattern).

## Writing

- **[Self-Maintaining AI Memory Layer](https://digivasserver-ai.github.io/ai-memory-layer.html)** — architecture, the ten observation types, guardrails, and what the system has and has not proven so far.
- **[Signal 36: the Android profiler that kills your shell scripts](https://digivasserver-ai.github.io/signal-36.html)** — root cause, measurements, fix, and the four things still unexplained.
- **[Building Android apps on an ARM64 phone](https://digivasserver-ai.github.io/arm64.html)** — the `aapt2` override, the compileSdk 37 hand-install, and the Gradle traps that cost the most time.

## Upstream

- **[SUSE MCP fixes](https://github.com/chrisjohntapp/suse-mcp/pulls?q=is%3Apr+author%3Adigivasserver-ai)** — three proposed changes to the SUSE MCP server: command detection via `shutil.which` instead of the external `which` binary, wiring the consolidated tools to their real function signatures, and reading the actual RPM macro sources. Open, not merged.

## A note on older pull requests

Some pull requests from August–September 2026 were bounty work against small repositories. Several are still open, and one target repository has since been deleted. That phase is over: current work is security and build fixes in projects I actually use — memanto, microG, UpgradeAll and suse-mcp — plus the repositories above.

## Contact

Email [digivas.server@gmail.com](mailto:digivas.server@gmail.com) for funding conversations, security reports or collaboration. Vulnerabilities should go there rather than into a public issue; see each repository's `SECURITY.md`.
