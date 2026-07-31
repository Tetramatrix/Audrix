# Plan: Fix Audrix Docs Wording

## Context
The current docs undersell Audrix's actual capabilities. The hero stat says "10+ Backends" but the real count of selectable transcription models is 17–18+ (11 WhisperLive + ~6–7 Lemonade).

## Changes Required

### 1. Hero Stats
- Change `10+ Backends` → `17+ Models`
- Keep `100% Offline` as-is (refers to transcription)

### 2. Hero/Overview Copy
- Add: "Live transcript analysis with 15 providers including OpenAI, Anthropic, StepFun, Groq, OpenRouter, and local Ollama/LM Studio"
- Clarify: "Transcription runs 100% offline. Live AI analysis can run locally or via your preferred cloud provider."

### 3. Providers Section
- Add note: "Transcription engines: WhisperLive (11 models), Lemonade NPU (dynamic), External WebSocket"
- Add cloud provider chips: OpenAI, Anthropic, Groq, StepFun, OpenRouter, NVIDIA, Mistral, Gemini, DeepSeek, XiaomiMiMo, CommandCode
- Keep existing local chips: Ollama, LM Studio, Lemonade

### 4. FAQ
- Add: "Does transcript text leave my machine?" → "Only if you choose a cloud LLM provider for analysis. Transcription itself is 100% local."

### 5. Meta/JSON-LD
- Update description to mention cloud provider support

## Out of Scope
- Do not change code/config defaults
- Docs-only wording fix
