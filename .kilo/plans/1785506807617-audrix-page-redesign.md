# Audrix docs/index.html Redesign

## Goal
Rewrite `D:\Benutzer\github\Audrix\docs\index.html` to match Sorana's page look, structure, ads, and interaction patterns, with a different color scheme and Audrix-specific content.

## Decisions (locked)
- **Color scheme**: Cyan/Electric blue — primary `#06b6d4`, dark bg `#0b0f14`, surface `#111820`, surface-2 `#19222d`, surface-3 `#202a37`, primary hover `#22d3ee`, primary dim `rgba(6,182,212,0.12)`, primary glow `rgba(6,182,212,0.06)`. Light theme overrides: bg `#f6f9fb`, surface `#ffffff`, primary `#0891b2`, primary hover `#0e7490`.
- **Images**: Use existing Audrix images only (`Audrix_Main.png`, `Audrix_Settings.png`, `Audrix_Models.png`, `logo-3.png`, `softpedia.png`, `ms-store.svg`, `qrcode.png`, `bch_qrcode.png`, `AlternativeTo.png`, `Aicono.png`, `sorana.png`, `tabneuron.png`, `RyzenZPilot_3.1.3.png`). Drop any references to images that don't exist in `docs/`.
- **Content sections**: Keep every Audrix content section. Map onto Sorana's structural patterns: nav, hero with eyebrow + stats + showcase + floating badges, how-it-works steps, testimonials, ad spot, overview grid, why-audrix problem cards, core features grid with ad-card in-feed + show-more toggle, chat examples, backends + models preview (providers-style), audio deep dive, vision & OCR, comparison table, who-uses grid, setup cards, support cards, pricing, discover grid, FAQ, ad spot, footer CTA, footer.
- **AdSense slots**: Same pattern as Sorana — head script only, then body slots: banner after testimonials (728×90), smaller banner after overview (468×60), in-feed fluid ad in features grid, 300×250 after examples, 728×90 after comparison, 336×280 after who-uses, 728×90 after pricing, 728×90 before footer.
- **Theme toggle**: Dark/light toggle with localStorage persistence, same nav button pattern as Sorana, applied to cyan palette.

## Sorana Structure Map → Audrix Mapping
| Sorana section | Audrix replacement |
|---|---|
| Hero eyebrow "Personal AI Workspace / PKM" | "Real-Time Local Intelligence Engine" |
| Hero stats | System Audio, Noise Suppression, 10+ Backends, 100% Offline, 0ms Cloud |
| Hero showcase | `Audrix_Main.png` screenshot |
| How it works (3 steps) | 1. Choose Backend → 2. Capture Audio → 3. Get Transcripts |
| Testimonials | Existing Softpedia quote (Softpedia logo image) |
| Why Sorana → Why Audrix | Problem/solution cards mapped to Audrix pain points |
| Core features → Core Features | Feature cards for transcription, audio capture, noise/crosstalk, backends, OCR/vision, offline, multi-stream, configurable |
| Chat examples → Capability examples | Example prompts for transcription, audio routing, crosstalk, system audio, OCR |
| Comparison → How Audrix compares | Table: Audrix vs Cloud STT vs generic offline tools |
| Who uses → Who uses | Researchers, meetings, coders, journalists, privacy users |
| Providers → Backends & Models | Provider-style chips: Whisper, Lemonade, External/WebSocket, plus local model chips |
| Model preview → Model preview | Lemonade Qwen3.6-35B, Whisper, etc. |
| Setup → Setup | Download, Choose backend, Start transcribing |
| Support → Support | Discord, GitHub, Softpedia feedback, AlternativeTo |
| Pricing → Pricing | Free + optional future paid |
| Discover → Discover | Sorana, TabNeuron, RyzenZPilot, Aicono (same cards as current Audrix page) |
| FAQ → FAQ | Audrix-specific questions |

## CSS Architecture
- Inline `<style>` block in `<head>` (drop external `main.css` dependency).
- CSS custom properties for dark/light themes.
- All Sorana component classes reused: `.hero`, `.hero-eyebrow`, `.hero-stats`, `.stat`, `.showcase`, `.screenshot-wrap`, `.floating-badges`, `.badge`, `.badge-dot`, `.section`, `.section-alt`, `.section-header`, `.steps`, `.step`, `.step-number`, `.testimonials-grid`, `.testimonial-card`, `.ad-container`, `.ad-label`, `.overview-grid`, `.overview-video`, `.problem-grid`, `.problem-card`, `.features-grid`, `.feature-card`, `.feature-card.large`, `.feature-icon`, `.feature-card.ad-card`, `.examples-grid`, `.example-card`, `.comparison-table`, `.providers-section`, `.provider-chip`, `.model-preview`, `.model-row`, `.setup-grid`, `.setup-card`, `.pricing-grid`, `.pricing-card`, `.pricing-card--accent`, `.discover-grid`, `.discover-card`, `.faq-item`, `.cta-section`, `.cta-actions`, footer, `#backToTop`, `.reveal`, `.screenshot-card`, `.screenshot-strip`.
- Cyan-primary variants: `--color-primary`, `--color-primary-hover`, `--color-primary-dim`, `--color-primary-glow`, `--color-free`, `--color-cloud`, `--color-local` mapped to cyan-compatible hues (free=`#4ade80`, cloud=`#60a5fa`, local=`#f59e0b` kept as-is from Sorana since they're semantic).
- Nav logo: inline SVG with cyan stroke/fill.

## JS Behavior (preserved from Sorana)
- Theme toggle with `localStorage('theme')` and `prefers-color-scheme` fallback.
- `#toggleFeatures` show-more/less toggle for features grid.
- Nav scroll shadow (`.scrolled`).
- Active nav link highlight via `IntersectionObserver`.
- Section reveal on scroll (`.reveal` → `.revealed`).
- Back-to-top button visibility on scroll.
- Stat counter animation for numeric `.stat-number` elements.

## Ads (same client, same slots)
```html
<!-- A: after testimonials -->
<ins style="display:inline-block;width:728px;height:90px" data-ad-slot="8924662119"></ins>
<!-- B: after overview -->
<ins style="display:inline-block;width:468px;height:60px" data-ad-slot="6119369521"></ins>
<!-- C: in-feed fluid inside features grid -->
<ins style="display:block" data-ad-format="fluid" data-ad-layout-key="-7g+ex-1i-2s+ay" data-ad-slot="9713451440"></ins>
<!-- D: after examples -->
<ins style="display:inline-block;width:300px;height:250px" data-ad-slot="3798779788"></ins>
<!-- E: after comparison -->
<ins style="display:inline-block;width:728px;height:90px" data-ad-slot="8476391393"></ins>
<!-- F: after who-uses -->
<ins style="display:inline-block;width:336px;height:280px" data-ad-slot="8429838091"></ins>
<!-- G: after pricing -->
<ins style="display:inline-block;width:728px;height:90px" data-ad-slot="3783483244"></ins>
<!-- H: before footer -->
<ins style="display:inline-block;width:728px;height:90px" data-ad-slot="9816026248"></ins>
```

## Content Drafts (high-level)
- **Hero h1**: "Real-time intelligence. No cloud required."
- **Hero sub**: Audrix captures live audio + screen, transcribes with noise suppression and crosstalk detection, runs OCR/Vision locally. Offline. Private.
- **Why cards**: AI can't hear your system audio / Audrix captures loopback + mic; Transcription locks you to cloud / Audrix runs fully offline with multiple backends; Overlapping speech ruins transcripts / Dual-stream crosstalk suppression; Screen text stays locked in images / Built-in local OCR; Switching engines means reinstalling / Hot-swappable backends at runtime.
- **Features**: Real-Time Transcription, System Audio + Mic, Noise & Crosstalk, Flexible Backends (Whisper/Lemonade/External), Local OCR & Vision, 100% Offline, Dual-Stream Mode, Configurable Pipeline.
- **Backends chips**: Whisper, Lemonade, External WebSocket/HTTP, Ollama-compatible, LM Studio-compatible.
- **Comparison**: Audrix vs Cloud STT APIs vs Generic offline STT — rows: offline, system audio, crosstalk, OCR, privacy, cost, NPU acceleration, portable.
- **Discover cards**: Sorana, TabNeuron, RyzenZPilot, Aicono (keep existing copy from current Audrix page).

## Implementation Order
1. Replace `<!DOCTYPE html>` through `</head>` with new meta block, OG/Twitter tags, canonical, JSON-LD `SoftwareApplication` + `FAQPage`, inline `<style>` block (full Sorana CSS adapted to cyan palette), Google Ads script.
2. Build `<body>`: skip-link, nav (logo SVG + links + download btn + theme toggle + mobile menu toggle), hero, how-it-works, testimonials, ad A.
3. Overview section + ad B.
4. Why-audrix problem cards.
5. Core features grid + in-feed ad C + show-more toggle + screenshot strip.
6. Examples/capabilities grid + ad D.
7. Comparison table + ad E.
8. Who-uses grid + ad F.
9. Backends/providers + model preview.
10. Audio deep dive, vision & OCR.
11. Setup, support, pricing, discover, FAQ.
12. Ad G, ad H, footer CTA, footer, back-to-top button.
13. Inline JS block (theme toggle, menu toggle, toggleFeatures, nav shadow, active link observer, reveal observer, back-to-top, stat counters).

## Validation
- Open in browser: dark and light themes render correctly, toggle persists.
- All 8 AdSense slots render containers without JS errors.
- Nav mobile menu opens/closes.
- All 3 hero screenshots load from `docs/` (verify paths).
- All internal anchor links scroll smoothly to correct section.
- No references to missing image files.
- Collapsible/expandable sections in Why/Core Features use `<details>` or equivalent JS; verify no orphaned `toggleSectionFromH2` references from old design.
- Compare final line count ~2500-2700 lines (matches Sorana scope).

## Out of Scope
- main.css removal from linked files — external CSS is dropped entirely; no migration needed.
- Backend/content copy finalization — implementer fills exact paragraph text from existing Audrix docs content.
- Favicon update — leave `assets/favicon.ico` reference as-is.
