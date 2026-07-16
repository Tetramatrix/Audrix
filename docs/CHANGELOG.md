# 📋 Changelog 📋
📅 July 16, 2026 — Version 1.0.2
🆕 loopback_gain_db / mic_gain_db implemented — config fields existed in AudioConfig, settings UI, and JSON but were never wired to `audio_capture`. VB-Audio Virtual Cable captures at ~0.000009 RMS, below noise gate. Gain now applied before AEC processing.
🆕 Send loop silent audio drop fixed — `_can_send()` writability check moved before `queue.get()` to prevent chunks being permanently lost on spurious `select.select` failures on Windows.
🐛 LLM model routing collision — `stepfun` vs `stepfun_plan` share model names but have different base URLs. LLMClient now always uses provider's resolved URL when `llm_provider` is explicit, ignoring stale `chat_url` in config.
🐛 Lemonade factory crash — `config.server.overlap_buffers` → `config.server.lemonade_overlap_buffers` (AttributeError on Lemonade backend startup).
🐛 Tooltip overlap fixed — multiple tooltips stacking on hover; now destroys previous tooltip before creating new one.
🔄 Settings UI labels rewritten — DSP jargon replaced with plain language: "AEC filter length (taps)" → "AEC echo memory", "NLMS adaptation rate" → "AEC adaptation speed", etc.
🆕 Mic/Loopback gain sliders — new controls (-20 to +40 dB) added to Audio Source settings.
🆕 Multi-line tooltips — all audio controls now explain what each setting does.
🔄 Crosstalk defaults tuned — echo sensitivity 0.45 → 0.30 (more aggressive), detection window 4000 → 6000 ms.
🔄 Default configs updated — mic_gain=5 dB, loopback_gain=15 dB, echo_sensitivity=0.30, echo_window=6000 ms, noise_gate=0.01 (hard cap 0.05).
🆕 Noise gate logging for whisperlive backend.
🆕 Model capability detection for portaudio_stt stack.
🐛 Start/stop button race condition and slow stop blocking UI fixed.
🐛 `_on_start()` re-entrancy race — `_starting` flag set before `self.update()`.
🐛 Remote transcription regression — synchronous `stop_server()` re-added.
🐛 `mic_gain_db`/`loopback_gain_db` added to `config_from_sdk_config`.
🐛 Post-stop WS error leak suppressed; OS messages English-translated.
🐛 Late transcript events dropped after Stop instead of wiping widget.
🐛 Server C++ subprocess wait reduced from 3s to 1s.
🐛 Redundant `bridge_thread.join` removed from server cleanup.
🐛 Bare `except Exception:pass` replaced in community cooldown check.
🐛 Loopback gain + logging performance — low RMS in dual-stream capture.
🔄 Context menu submenu logic for active models and model manager selection.
🔄 Synchronous `stop_server()` before clearing `_runtime` to prevent zombie processes.
🔄 `_nullctx()` replaced with `contextlib.nullcontext()`.
🔄 Analysis tab toolbar consolidated with font size slider.
🔄 Config import/access logic consolidated in `StreamCoordinator`.
🔄 Unused logging imports and duplicate logger definitions cleaned up.
⚡ orjson drop-in for WhisperLive wire format / native-UTF-8 round-trip.
🧹 Diagnostic and import logs downgraded from INFO to DEBUG.
🧹 Default `mic_gain_db` changed from 5.0 to 10.0.
🧹 Start/Stop banner logging added for easier debugging.