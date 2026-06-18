# Process Report — Building the "Agentic AI" Presentation

**Deliverable:** `Agentic_AI_Overview.pptx` (12 slides)
**Source material:** Auto-generated Hindi/Urdu transcript of the introductory Agent Factory lecture
**Date:** Prepared for course submission

---

## 1. Overview of the workflow

The presentation was produced from a single source: the auto-generated caption transcript of the lecture video. The transcript was in Hindi/Urdu (Roman/Devanagari mix) and contained the usual artifacts of machine captioning — run-on sentences, repeated filler, and phonetic spellings of technical terms (e.g., "जेडीकेआई"/"जेडीसीआई" for *Agentic AI*, "एफटीई" for *FTE*).

The end-to-end process was:

1. **Ingest and read** the full transcript.
2. **Translate and de-noise** the content from spoken Hindi/Urdu into structured English concepts.
3. **Extract the conceptual spine** of the lecture and decide what belonged on slides versus what was conversational filler (introductions, Q&A, portal navigation, Eid greetings).
4. **Outline** a 12-slide arc that follows the lecture's own logical progression.
5. **Generate** the deck programmatically (PptxGenJS), applying a single consistent visual system.
6. **Quality-assure** each slide visually, then fix the defects found.

---

## 2. The AI tools / models used

| Tool / model | Role in the process |
|---|---|
| Claude (Anthropic) | Translation of the Hindi/Urdu transcript, concept extraction, slide outlining, and all slide-generation code |
| PptxGenJS (Node.js library) | Programmatic creation of the `.pptx` file |
| react-icons + sharp | Rendering vector icons (Font Awesome set) to PNG for use as a repeated visual motif |
| LibreOffice + pdftoppm | Converting slides to images for visual QA |

No video tool was used — the video itself cannot be processed, so the **transcript was the entire input**.

---

## 3. The prompts used, and how they evolved

Because the deck was built through a working session rather than a single prompt, the "prompts" below are the actual instructions and refinements that drove the result. They are grouped by stage.

### Stage 1 — Getting usable text out of the video

- **First instinct (did NOT work):** trying to use the video link directly. A video URL yields no usable content — no transcript, no audio, nothing the model can read. This was a dead end and was abandoned immediately.
- **Refinement that worked:** switching the input to the **text transcript**. Specifically, pasting the auto-generated captions. This is the single most important pivot in the whole process — *the deliverable is only as good as the text you feed in.*
- **Language complication:** the transcript came out in Hindi/Urdu. The effective instruction here was *"translate the Hindi transcript yourself and build the slides in English."* This worked better than relying on YouTube's own auto-translation, which tends to be clunky on technical vocabulary.

### Stage 2 — Defining the deliverable precisely

- **Vague prompt (worked poorly):** *"make slides from this video."* This is under-specified — it leaves audience, length, language, and depth unresolved, and produces a generic result.
- **Refined prompt (worked well):** specifying four things up front — *both files (slides + report), English, ~10–12 slides, concise.* Tightening these four parameters removed all the guesswork and is the difference between a usable deck and a shapeless one.

**Lesson:** the most effective prompts named concrete constraints (count, language, tone, output format). The least effective ones left those open.

### Stage 3 — Content extraction

The instruction that worked was framing the task as *"extract the conceptual spine, not a transcript dump."* The lecture is ~2 hours and roughly 40% of it is introductions, student Q&A, and platform/portal walkthroughs. A prompt that said "summarize the video" would have pulled in that filler. The prompt that worked explicitly **separated teaching content from logistics** and kept only the former.

### Stage 4 — Slide generation

- **What worked:** asking for a *consistent visual system* — one color palette, one icon motif repeated on every slide, a fixed type hierarchy — rather than styling slides one at a time. Defining the system once and applying it everywhere is what makes the deck look intentional instead of templated.
- **What did NOT work (and had to be refined):** the first render had two real defects — a card on the "Seven Golden Rules" slide sat too close to the bottom edge (below the safe margin), and a callout card's text was slightly cramped. These were caught in visual QA and fixed by tightening the grid spacing and enlarging the cramped container. *The first generation is rarely final; the QA pass is not optional.*

---

## 4. What worked vs. what did not

### Worked well
- **Transcript as input** (instead of the video link).
- **Naming constraints up front** (count, language, tone).
- **Translating in-model** rather than relying on the platform's auto-translate.
- **Extracting the conceptual arc** and dropping ~40% of the runtime (intros, Q&A, portal tour).
- **A single, reusable visual system** applied across all 12 slides.
- **A visual QA pass** that rendered every slide to an image and inspected it.

### Did not work / had to be refined
- Pointing at the **video link** — produced nothing usable.
- The **un-translated Hindi captions** carried transcription errors on technical terms; these had to be corrected by inferring the intended term from context (e.g., recognizing "जेडीकेआई" as *Agentic AI*).
- A **vague "make slides" instruction** would have produced a generic, overlong deck; it had to be narrowed.
- The **first slide render** had margin/overflow defects that required a fix-and-re-verify cycle.

---

## 5. The conceptual structure that was extracted

The lecture's own logical progression became the slide order:

1. **Title / orientation**
2. **What is AI?** (the microwave analogy: perceive → decide → act)
3. **The three levels of AI** (Predictive → Generative → Agentic)
4. **How an agent works** (Plan → Research → Build → Test → Fix & deliver)
5. **AI as a Tool vs. AI as a Worker** (the factory-owner email example)
6. **The Agent Factory** (Design → Train → Ship → Verify)
7. **The AI-Native Company** (the 200→10 customer-support example)
8. **Your AI Delegate / "Identical AI"** (the CEO → delegate → workers chain)
9. **The 10–80–10 Rule** (the film-director analogy)
10. **Promoted, not replaced** (typist→editor, coder→architect, worker→director)
11. **The Seven Golden Rules** (the non-negotiables)
12. **Key takeaways + the self-study assignment**

---

## 6. Honest note on authorship

This report documents the genuine process that produced the attached deck. The "prompts" described are the real instructions and refinements used in this session. If your course expects the report to reflect *your own* experimentation, you should run your own prompts against the transcript, record what you actually tried, and adjust this document so it describes your process rather than this one. The structure above is a faithful template you can edit to match your own work.
