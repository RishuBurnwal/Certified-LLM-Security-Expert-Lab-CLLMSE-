# CLLMSE Practical Lab — CTF Walkthrough (Master Index)

Complete walkthrough of the **cllmse-lab** LLM-security CTF, mapped to the OWASP Top 10 for LLM Applications (2025). This is the **master document**: it explains how to spawn the lab, how the challenges work, and links to a dedicated writeup for every exam question. Each writeup lives in [`writeups/`](writeups/) and contains the scenario, the exact payload, how it was submitted, the console result, a screenshot, and the flag.

- **Lab server:** `http://127.0.0.1:8090`
- **Flag format:** `RTL{...}` — paste exactly, including the wrapper. Hex is case-insensitive; do not truncate.
- **Structure:** 5 challenges × 2 questions each (one EXPLOIT flag + one GUARDRAIL flag) = 10 questions.

---

## Table of Contents

1. [How to Spawn the Lab](#how-to-spawn-the-lab)
2. [How the Challenges Work](#how-the-challenges-work)
3. [Challenge & OWASP Map](#challenge--owasp-map)
4. [Question Index (per-question writeups)](#question-index)
5. [Flags Collected](#flags-collected)
6. [Repo Layout](#repo-layout)

---

## How to Spawn the Lab

The exam ships `cllmse-lab.zip` with 5 pre-built binaries (one per OS/arch) plus a `README.txt`. It listens on `127.0.0.1` only — no internet, no install.

### Windows (PowerShell)

```powershell
# 1) Extract
Expand-Archive cllmse-lab.zip -DestinationPath cllmse-lab

# 2) Run the binary for your platform
cd cllmse-lab
.\cllmse-lab-windows-amd64.exe
```

### macOS / Linux

```bash
unzip cllmse-lab.zip -d cllmse-lab/
cd cllmse-lab/
chmod +x cllmse-lab-darwin-arm64      # pick your platform's file
./cllmse-lab-darwin-arm64
```

Pick the file matching your platform:

| Platform | Binary |
|----------|--------|
| Apple Silicon (M1–M4) | `cllmse-lab-darwin-arm64` |
| Intel Mac | `cllmse-lab-darwin-amd64` |
| Linux x86_64 | `cllmse-lab-linux-amd64` |
| Linux ARM64 | `cllmse-lab-linux-arm64` |
| Windows x86_64 | `cllmse-lab-windows-amd64.exe` |

When it prints `listening at http://127.0.0.1:8090`, open that URL in a browser.

**Port already in use?** Set `PORT` before launching and adjust the URLs accordingly:

```bash
PORT=9090 ./cllmse-lab-darwin-arm64        # macOS/Linux
```
```powershell
$env:PORT=9090; .\cllmse-lab-windows-amd64.exe   # Windows PowerShell
```

Other troubleshooting: macOS Gatekeeper → `xattr -d com.apple.quarantine <binary>`; Windows SmartScreen → More info → Run anyway; Linux `chmod +x` first.

---

## How the Challenges Work

Each challenge page at `http://127.0.0.1:8090/challenge/<n>` (n = 1–5) gives a scenario and an input box. This is **not** a click-through demo — you write the actual payload and the server checks whether it truly triggers the flaw.

1. **Read the scenario, write a payload, Submit.** If it doesn't trigger, the console gives a hint — adjust and resubmit. On success you get an **EXPLOIT flag**.
2. **Click "Enable Guardrail"** — turns on the specific control named on the page (unlocks only after a successful exploit).
3. **Submit again** — the same payload (any phrasing) is now blocked, revealing a **GUARDRAIL flag**.

---

## Challenge & OWASP Map

| # | Challenge | OWASP mapping |
|---|-----------|---------------|
| 1 | Indirect Prompt Injection | LLM01:2025 |
| 2 | RAG Knowledge-Base Poisoning | LLM04:2025 |
| 3 | SSRF via Unvalidated LLM-Generated URL | LLM05:2025 |
| 4 | Excessive Agency (Tool-Calling Agent) | LLM06:2025 |
| 5 | MCP Plugin Supply-Chain Rug Pull | LLM03:2025 |

---

## Question Index

Each of the 10 exam questions has its own writeup. Two questions per challenge (EXPLOIT + GUARDRAIL).

| Q | Challenge | Type | Writeup | Status |
|---|-----------|------|---------|--------|
| 1 | C1 Indirect Prompt Injection | EXPLOIT | [Q1 writeup](writeups/Q1-challenge1-indirect-prompt-injection-exploit.md) | ✅ Solved |
| 2 | C1 Indirect Prompt Injection | GUARDRAIL | [Q2 writeup](writeups/Q2-challenge1-indirect-prompt-injection-guardrail.md) | ✅ Solved |
| 3 | C2 RAG Knowledge-Base Poisoning | EXPLOIT | [Q3 writeup](writeups/Q3-challenge2-rag-poisoning-exploit.md) | ✅ Solved |
| 4 | C2 RAG Knowledge-Base Poisoning | GUARDRAIL | [Q4 writeup](writeups/Q4-challenge2-rag-poisoning-guardrail.md) | ✅ Solved |
| 5 | C3 SSRF via LLM-Generated URL | EXPLOIT | [Q5 writeup](writeups/Q5-challenge3-ssrf-exploit.md) | ✅ Solved |
| 6 | C3 SSRF via LLM-Generated URL | GUARDRAIL | [Q6 writeup](writeups/Q6-challenge3-ssrf-guardrail.md) | ✅ Solved |
| 7 | C4 Excessive Agency | EXPLOIT | [Q7 writeup](writeups/Q7-challenge4-excessive-agency-exploit.md) | ✅ Solved |
| 8 | C4 Excessive Agency | GUARDRAIL | [Q8 writeup](writeups/Q8-challenge4-excessive-agency-guardrail.md) | ✅ Solved |
| 9 | C5 MCP Supply-Chain Rug Pull | EXPLOIT | [Q9 writeup](writeups/Q9-challenge5-mcp-rug-pull-exploit.md) | ✅ Solved |
| 10 | C5 MCP Supply-Chain Rug Pull | GUARDRAIL | [Q10 writeup](writeups/Q10-challenge5-mcp-rug-pull-guardrail.md) | ✅ Solved |

---

## Flags Collected

| Q | Challenge | Type | Flag |
|---|-----------|------|------|
| 1 | C1 Indirect Prompt Injection | EXPLOIT | `RTL{164ac1f27fe5d1407da567642c92df42c268d3b88ee222ac6ce26ac9e25f7828}` |
| 2 | C1 Indirect Prompt Injection | GUARDRAIL | `RTL{4daac7e5097c4bda6d70f860f5e11bac32c351f3c921c4589e3786df1df20d0f}` |
| 3 | C2 RAG Knowledge-Base Poisoning | EXPLOIT | `RTL{085faf1f7cf11e75ceddd11c928c3013bf1ab87ac7f1cf096a7472e57551a8f8}` |
| 4 | C2 RAG Knowledge-Base Poisoning | GUARDRAIL | `RTL{941283d7cb96fb22521a003ff5737954624c150b0d95b3584cdfa76d4e49efe0}` |
| 5 | C3 SSRF via LLM-Generated URL | EXPLOIT | `RTL{eb9202a4b553f211c8362e9c28d2d82a99d030bd631f60e0981ce72fdfa587b3}` |
| 6 | C3 SSRF via LLM-Generated URL | GUARDRAIL | `RTL{caea2a67fde010c911953a81ff51c907792a58fb816a56e9c21ea8454eab9abd}` |
| 7 | C4 Excessive Agency | EXPLOIT | `RTL{dc105b0c7605e7b00479aa6db96eec950867dd85d38c00af7f857ef00b3e5fd9}` |
| 8 | C4 Excessive Agency | GUARDRAIL | `RTL{34272633f0eb5c0adc8f18a819c1e994b2036a640ac904b79185a7e7a91708f6}` |
| 9 | C5 MCP Supply-Chain Rug Pull | EXPLOIT | `RTL{6580a3df76a49ab85d2254c22cb0efeebd1eb91b46fc2a981558d73b0a89c654}` |
| 10 | C5 MCP Supply-Chain Rug Pull | GUARDRAIL | `RTL{892a2ac8678d5413bd36e23e51296d49f0a01148287fccf2ced1a9529737cc30}` |

**All 10 questions solved. ✅**

---

## Repo Layout

```
CTF AI/
├── README.md                      # this master index
├── Instruction.txt                # original exam instructions
├── cllmse-lab.zip                 # lab package
├── cllmse-lab/                    # extracted binaries + README.txt
├── screenshots/                   # proof screenshots per challenge
│   ├── challenge1_exploit.png
│   ├── challenge1_guardrail.png
│   ├── challenge2_exploit.png
│   ├── challenge2_guardrail.png
│   ├── challenge3_exploit.png
│   ├── challenge3_guardrail.png
│   ├── challenge4_exploit.png
│   ├── challenge4_guardrail.png
│   ├── challenge5_exploit.png
│   └── challenge5_guardrail.png
└── writeups/                      # one markdown file per exam question
    ├── Q1-challenge1-indirect-prompt-injection-exploit.md
    ├── Q2-challenge1-indirect-prompt-injection-guardrail.md
    ├── Q3-challenge2-rag-poisoning-exploit.md
    ├── Q4-challenge2-rag-poisoning-guardrail.md
    ├── Q5-challenge3-ssrf-exploit.md
    ├── Q6-challenge3-ssrf-guardrail.md
    ├── Q7-challenge4-excessive-agency-exploit.md
    ├── Q8-challenge4-excessive-agency-guardrail.md
    ├── Q9-challenge5-mcp-rug-pull-exploit.md
    └── Q10-challenge5-mcp-rug-pull-guardrail.md
```
