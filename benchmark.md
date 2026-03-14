# Cézanne Period Benchmark
**Model:** Flux.1-dev Q4_K_S (GGUF)  
**Platform:** ComfyUI, M4 Mac 24GB  
**Sampler:** Euler | **CFG:** 1.0 | **Seed:** randomized per run | **Steps:** 10 | **Resolution:** 512x512

---

## Thesis

A painting encodes decisions, every brushstroke is intentional. A photo is just light. Getting a model to understand the intentionality of a Cézanne period is a fundamentally harder task than generating a realistic apple. This benchmark tests whether Flux.1 can distinguish between three philosophically distinct phases of Cézanne's career, not just visually, but structurally.

---

## Paintings Selected

| Period | Painting | Year | Why |
|--------|----------|------|-----|
| Early (1859–1875) | The Murder | Dark romantic, violent, Delacroix influence - unambiguously Early |
| Middle (1875–1890) | The Card Players | Geometric figure composition, muted palette - peak Cézanne the theorist |
| Middle (1875–1890) | Fruit Bowl, Glass and Apples | Still life with intentional geometric distortion - proto-Cubism hiding in plain sight |
| Late (1890–1906) | The Forest | Near-total abstraction, flattened planes, dissolved edges - maximum stress test |

---

## Rubric (1–5 per dimension)

### Quantitative Dimensions
| Dimension | Description | Score (1–5) |
|-----------|-------------|-------------|
| **Palette accuracy** | Earth tones, warmth/coolness, saturation match for period | - |
| **Brushwork visibility** | Impasto texture, stroke character, paint handling | - |
| **Planarity** | How flat/abstracted are the forms (low = 3D realistic, high = Cézanne flat) | - |
| **Compositional structure** | Geometric blocking, horizon placement, spatial logic | - |
| **Edge quality** | Hard (Early) → structured (Middle) → dissolved (Late) | - |

### Qualitative Dimensions
| Dimension | Description | Notes |
|-----------|-------------|-------|
| **Period attribution** | Would a blind rater place this in the correct period? | - |
| **Mood/atmosphere** | Does the emotional register match? | - |
| **Distinctive feature presence** | Is the most period-specific quality present? | - |

---

## Runs

---

### Painting 1: The Murder (Early Period, 1867)

---

#### Run 1
**Seed:** 42
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 1.0

**Positive Prompt:**
> oil painting by Paul Cézanne, The Murder 1867, early period, three figures in violent struggle, murderer raising hand for final blow, collaborator pinning victim down, victim contorted in pain, faceless murderers, anonymous violence, threatening dark sky, riverbank setting, heavy impasto brushwork, dark earth tones, deep chiaroscuro, elongated distorted figures, Géricault influence, somber dramatic palette, 19th century French painting

**Negative Prompt:**
> photograph, digital art, modern, bright colors, impressionist, watercolor, sketch, flat, decorative, cheerful, portrait, landscape, still life, faces on attackers, realistic proportion

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 2 | Dark earth tones present but too warm/golden - more Neoclassical than Early Cézanne |
| Brushwork visibility | 2 | Smooth and polished - opposite of Cézanne's raw impasto |
| Planarity | 1 | Fully 3D, academic anatomy - no flattening whatsoever |
| Compositional structure | 3 | Three figures in struggle, triangular composition, but too classical |
| Edge quality | 2 | Hard defined edges - more Baroque than Early Cézanne |

**Qualitative Notes:**
- Three figures in violent struggle captured ✅
- Faceless murderers NOT achieved - faces visible ❌
- Threatening sky/riverbank missing ❌
- Output reads as Géricault/Neoclassical wrestling scene, not Cézanne
- Caravaggio/Goya Baroque energy - dark chiaroscuro but wrong tradition
- Prompt error: "Géricault influence" and "Old Masters" language pulled model toward Romantic/Neoclassical tradition
- "Realistic anatomy" in negative prompt needed - figures too polished and academic
- **Verdict:** Prompt calibration failure. Model understood violent struggle but wrong stylistic tradition entirely.

**Prompt Changes for Run 2:**
- Removed: "Géricault influence", "Old Masters"  
- Added: "Post-Impressionist", "raw unfinished quality"
- Added to negatives: "Renaissance, Baroque, Caravaggio, Goya, Géricault, neoclassical, polished, realistic anatomy, academic painting"

---

#### Run 2
**Seed:** 741638556860966
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 1.0

**Positive Prompt:**
> oil painting by Paul Cézanne, The Murder 1867, Post-Impressionist early period, three figures in violent struggle, murderer raising hand for final blow, collaborator pinning victim down, victim contorted in pain, faceless murderers, threatening dark stormy sky, riverbank setting, heavy impasto brushwork, dark earth tones, deep shadows, raw unfinished quality, expressive distorted figures, somber dramatic palette, 19th century French painting

**Negative Prompt:**
> photograph, digital art, modern, bright colors, watercolor, sketch, flat, decorative, cheerful, Renaissance, Baroque, Caravaggio, Goya, Géricault, neoclassical, polished, realistic anatomy, academic painting

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 2 | Dark stormy sky improved but figures still too warm/golden |
| Brushwork visibility | 2 | Still smooth and polished, no Cézanne impasto |
| Planarity | 1 | Fully 3D, anatomically correct, no flattening |
| Compositional structure | 3 | Three figures correct, riverbank present, dynamic improved |
| Edge quality | 2 | Hard academic edges, still Baroque tradition |

**Qualitative Notes:**
- Threatening dark stormy sky achieved ✅
- Riverbank/outdoor setting present ✅
- Three figures in violent struggle, murderer raising hand ✅
- Faces still visible ❌
- Figures still naked ❌ - clothing never specified in prompt
- Still reading Neoclassical despite removing Géricault from prompt
- Model deeply biased: violent struggle = Greek wrestling = nude figures
- **Verdict:** Sky/setting improved but naked figure bias dominates. Need explicit clothing descriptions and nude/naked in negatives.

**Prompt Changes for Run 3:**
- Added: clothing descriptions (man in white shirt/dark trousers, woman collaborator in dark clothing, female victim)
- Added to negatives: "nude figures, naked, muscular"
- Strengthened Cézanne-specific language

---

#### Run 3
**Seed:** 565278852310445
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 1.0

**Positive Prompt:**
> Paul Cézanne oil painting 1867, The Murder, Post-Impressionist early period, man in white shirt and dark trousers raising fist, woman collaborator in dark clothing pinning female victim to ground, victim nearly invisible beneath attackers, anonymous faceless figures, near-black dark background, heavy crude impasto brushwork, flat distorted figures, raw urgent paint handling, dark earth tones, almost no sky visible, thick dark paint

**Negative Prompt:**
> photograph, digital art, modern, bright colors, watercolor, sketch, decorative, cheerful, Renaissance, Baroque, Caravaggio, Goya, Géricault, neoclassical, polished, realistic anatomy, academic painting, nude figures, naked, muscular

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 2 | Dark background achieved but figures too warm, no stormy sky |
| Brushwork visibility | 1 | Photorealistic render - no painterly quality whatsoever |
| Planarity | 1 | Fully 3D, photographic depth - no flattening |
| Compositional structure | 3 | Correct figure count and roles, victim on ground, attacker raised fist |
| Edge quality | 1 | Sharp photographic edges - no painterly treatment |

**Qualitative Notes:**
- Clothing prompt worked: man in white shirt present ✅
- Female victim on ground present ✅
- Victim still partially unclothed ❌ - prompt specified clothed figures
- Faces fully visible and detailed ❌
- Output reads as photorealistic Victorian scene, not painting
- Storm clouds and riverbank completely absent ❌
- Figure in dark clothing reads as black robe, not yellow dress ❌
- Blue denim jeans and shoes from original painting absent ❌
- Lighting/shimmer on murderer's shirt from original absent ❌
- **Verdict:** Specifying clothing improved figure role accuracy - man/woman/victim distinction clearer than previous runs but model defaulted to photorealism entirely. Painterly quality collapsed. Need to lead much harder with medium and style before subject matter.

**Prompt Changes for Run 4:**
- Lead with medium/style: "thick impasto oil paint, rough crude brushwork" before any subject description
- Restored clothing specifics with corrections: man in white shirt/blue trousers, woman collaborator in yellow sleeveless dress with bare arms
- Added knife - victim is being stabbed, not punched
- Added victim details: mouth open in agony, blonde hair splayed bottom right
- Added "faceless attackers" specifically
- Added turbulent blue-grey storm clouds for sky specificity
- Victim described as "nearly invisible merged with dark ground"
- Added to negatives: portrait, indoor scene, bright background, standing poses, studio lighting, three equally visible figures, upright standing figures, dark robe

#### Run 4
**Seed:** 299643117394964
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 1.0

**Positive Prompt:**
> thick impasto oil paint, rough crude brushwork, Paul Cézanne 1867, Post-Impressionist, The Murder, man in glowing white shirt and blue trousers lunging diagonally raising fist with knife, woman collaborator in yellow sleeveless dress with bare arms crouching over victim, female victim nearly invisible merged with dark ground, victim mouth open in agony, blonde hair splayed bottom right, anonymous faceless attackers, near-black dark background, turbulent blue-grey storm clouds, raw urgent brushwork, heavy dark paint, flat distorted figures, muted dark palette

**Negative Prompt:**
> photograph, photorealistic, smooth, polished, detailed faces, realistic skin, academic, Renaissance, Baroque, neoclassical, nude, naked, sharp focus, three equally visible figures, upright standing figures, dark robe, portrait, indoor scene, bright background, standing poses, studio lighting

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 2 | Stormy sky improved, blue jeans correct, but overall too warm and Hollywood-lit |
| Brushwork visibility | 1 | Fully hyperrealistic, no painterly quality whatsoever |
| Planarity | 1 | Fully 3D photographic depth, no flattening |
| Compositional structure | 2 | Victim present but rendered as giant dark blob under collaborator, riverbank absent |
| Edge quality | 1 | Sharp photographic edges throughout |

**Qualitative Notes:**
- Blue jeans on male attacker correct ✅
- Stormy sky marginally better than previous runs ✅
- Output reads as cinematic film still, highly polished rendering ❌
- All faces fully visible despite "anonymous faceless attackers" in prompt ❌
- Victim rendered as dark mass continuous with collaborator's yellow dress, no distinction between figures ❌
- Riverbank completely absent again ❌
- Hyperrealistic rendering persists despite heavy negative prompting ❌
- **Verdict:** Flux deeply resistant to departing from photorealism for figurative violence. Clothing specificity anchors model in cinematic tradition regardless of negative prompting strength.

**Prompt Changes for Run 5:**
- Strategy shift: lead entirely with paint medium, minimize subject description
- Added: "thick black and dark brown impasto, rough gestural brushstrokes, crude unfinished marks, heavy paint texture, somber near-black palette"
- Added: victim in indigo blue/black dress nearly dissolved into ground
- Added: "thick black ink impasto storm clouds swirling above"
- Added: "riverbank in middle background mix of grey and black brushstrokes"
- Added to negatives: Hollywood, cinematic, film still, clear sky, calm sky

---

#### Run 5
**Seed:** 990040829368474
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 1.0

**Positive Prompt:**
> Paul Cézanne 1867 oil painting, thick black and dark brown impasto, rough gestural brushstrokes, three barely visible dark figures, crude unfinished marks, heavy paint texture, somber near-black palette, early Post-Impressionist technique, The Murder, man in white shirt lunging diagonally with raised fist, woman in yellow sleeveless dress crouching, female victim wearing indigo blue black dress nearly dissolved into dark ground, blonde hair visible bottom right, victim mouth open, anonymous figures without faces, thick black ink impasto storm clouds swirling above, riverbank in middle background mix of grey and black brushstrokes, figures flat and distorted, paint applied in thick urgent slabs, dark earth tones, raw emotional violence rendered in paint not light

**Negative Prompt:**
> photograph, photorealistic, hyperrealistic, smooth skin, detailed faces, sharp focus, Renaissance, Baroque, neoclassical, Caravaggio, Goya, Géricault, academic painting, nude, naked, muscular, studio lighting, bright background, indoor scene, portrait, cinematic, film still, Hollywood, digital art, 3D render, illustration, anime, cartoon, standing upright, three equally visible figures, polished, decorative, clear sky, calm sky, clear sky, calm sky

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | - | - |
| Brushwork visibility | - | - |
| Planarity | - | - |
| Compositional structure | - | - |
| Edge quality | - | - |

**Qualitative Notes:**
- Sky and cloud composition noticeably improved - closest to original across all 5 runs ✅
- Yellow dress on collaborator present ✅
- Diagonal energy in male figure improved ✅
- Figure roles reversed - collaborator rendered on ground in distress rather than victim ❌
- Female victim in indigo dress completely absent ❌
- Unidentified dark figure present in background with no correspondence to original ❌
- Riverbank absent entirely ❌
- All faces fully visible and detailed ❌
- Output remains fully photorealistic despite medium-first prompting strategy ❌
- **Verdict:** Best sky/atmosphere result across all 5 runs but compositional accuracy regressed. Medium-first prompting marginally improved texture signal but did not break photorealism bias. Flux consistently cannot reconcile painterly medium with figurative violence subject matter across any prompt strategy tested.

---

### Painting 2: The Card Players (Middle Period, 1892)
*[TBD - runs to be added]*

---

### Painting 3: Fruit Bowl, Glass and Apples (Middle Period, 1879)
*[TBD - runs to be added]*

---

### Painting 4: The Forest (Late Period, 1894)
*[TBD - runs to be added]*

---

## Findings

### The Murder (Early Period, 1867): Preliminary Results

Flux.1 can generate violent figurative scenes. It cannot generate Cezanne's violent figurative scenes.

Across five runs with progressively refined prompts, the model consistently defaulted to cinematic, photorealistic rendering regardless of explicit instructions to the contrary. Run 1 produced a Neoclassical wrestling scene lifted directly from the Romantic tradition. Runs 2 through 4, with increasingly specific negative prompting against Baroque, neoclassical, and photographic styles, produced what can best be described as a Victorian film still. Run 5, which led entirely with medium description rather than subject description, showed marginal improvement in painterly texture but did not escape the fundamental problem.

The structural issue is a training data problem, not a prompting problem. Flux's training distribution for "violent clothed figures" is overwhelmingly photographic and cinematic. Cezanne's treatment of this subject is essentially absent from that distribution. The model knows what a murder looks like. It does not know what Cezanne's decision to paint a murder crudely, flatly, and without academic finish looks like. That distinction is the entire point of the benchmark.

A painting encodes decisions. A photo is just light. Getting a model to understand the intentionality of a Cezanne period is a fundamentally harder task than generating a realistic apple. The Murder results illustrate this tension precisely: every prompt iteration that increased subject specificity pulled the model further toward photorealism, while every iteration that increased medium specificity improved texture but lost compositional accuracy. The model cannot hold both simultaneously.

*Results for The Card Players, Fruit Bowl, Glass and Apples, and The Forest to be added in subsequent sessions.*



## Methodology Notes

- FID score skipped - requires 50+ images per period, overkill for this project
- CLIP score possible but noisy for fine art (trained on web images, not paintings)
- Cohen's Kappa used for inter-rater reliability with two raters (human + AI)
- Resolution kept at 512x512 for speed; quality sufficient for rubric scoring

---

*Generated with ComfyUI + Flux.1-dev Q4_K_S on M4 Mac, March 2026*
