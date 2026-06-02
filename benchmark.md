# Cézanne Period Benchmark
**Model:** Flux.1-dev Q4_K_S (GGUF)  
**Platform:** ComfyUI, M4 Mac 24GB  
**Sampler:** Euler | **CFG:** 1.0 (baseline), 2.0 (post-discovery, Card Players Run 3+) | **Seed:** randomized per run | **Steps:** 10 | **Resolution:** 512x512

---

## Thesis

A painting encodes decisions, every brushstroke is intentional. A photo is just light. Getting a model to understand the intentionality of a Cézanne period is a fundamentally harder task than generating a realistic apple. This benchmark tests whether Flux.1 can distinguish between three philosophically distinct phases of Cézanne's career, not just visually, but structurally.

---

## Paintings Selected

| Period | Painting | Year |
|--------|----------|------|
| Early (1859-1875) | The Murder | 1867 |
| Middle (1875-1890) | The Card Players | 1892 |
| Middle (1875-1890) | Fruit Bowl, Glass and Apples | 1880 |
| Late (1890-1906) | The Forest | 1904 |

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

## Methodology Note: ComfyUI Seed Logging

In ComfyUI's KSampler node with `control_after_generate: randomize`, the seed displayed in the UI after a run completes is the seed queued for the *next* generation, not the seed used for the current one. The accurate seed for any given output must be read from the PNG metadata after generation (`strings <file>.png | grep '"seed"'`) or from ComfyUI's history panel, not from the UI display at queue time. Seeds in this benchmark were corrected via PNG metadata audit; original Murder seeds for Runs 3-5 reflected the off-by-one error before correction.

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
**Seed:** 744762202065314
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

---

#### Run 4
**Seed:** 690343881524155
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
**Seed:** 299643117394964
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

---

#### Run 1
**Seed:** 990040829368474
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 1.0

**Positive Prompt:**
> Paul Cézanne 1892 oil painting, muted earth tone palette, ochre and burnt sienna and dusty blue, structured geometric brushwork, visible directional strokes building planes, matte unvarnished surface, two peasant men seated facing each other at wooden table in profile, playing cards, both wearing heavy work clothes, one in blue smock, one in brown jacket with yellow-tan hat, downcast eyes focused on cards, still wine bottle standing upright between them on table, warm brown tavern interior, simple plain background wall, quiet contemplative mood, no movement, balanced symmetrical composition, Post-Impressionist, thick paint application, blocky simplified forms, faces rendered as planes not detail

**Negative Prompt:**
> photograph, photorealistic, hyperrealistic, smooth skin, detailed faces, sharp focus, Renaissance, Baroque, neoclassical, academic painting, studio lighting, cinematic, film still, Hollywood, digital art, 3D render, illustration, anime, cartoon, polished, decorative, expressive gestures, dramatic lighting, action, movement, multiple figures crowded, standing figures, ornate background, fine detail in faces

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 3 | Ochre background and blue/brown clothing in correct family, but warmer and more saturated than actual painting |
| Brushwork visibility | 1 | Surface is smooth and airbrushed, zero impasto, no directional strokes visible |
| Planarity | 2 | Full 3D modeling on figures - rounded shoulders, dimensional hat brims, atmospheric shadow on back wall |
| Compositional structure | 4 | Genuinely close to Barnes/Met composition - two figures in profile, table between them, bottle centered, cards visible |
| Edge quality | 2 | Edges too soft and photographic, lacking Cézanne's structured edge definition |

**Qualitative Notes:**
- Two-figure composition correctly pulled (vs. three or four figure versions) ✅
- Bottle centered on table between figures ✅
- Profile poses with downcast eyes, contemplative mood ✅
- Quietness landed - no narrative animation, no mid-action energy ✅
- Left figure missing pipe ❌
- Cards sitting on table, not held in hands ❌
- Faces rendered photorealistically with individual features - opposite of Cézanne's planar mask-like faces ❌
- Hats too detailed and costume-specific - reads as Western/frontier rather than French peasant ❌
- Output reads as "two old prospectors" / Deadwood-adjacent rather than French tavern scene
- **Verdict:** Composition and palette caught the reference. Technique (brushwork, planarity, edges) completely missed. Same Murder failure mode - Flux knows what Cézanne paintings look like as reference images, not how Cézanne painted.

**Prompt Changes for Run 2:**
- Added: "smoking a long white clay pipe in his mouth", "both holding playing cards in their hands"
- Added: "French peasant" (counter Western pull)
- Added: "flat planar rendering", "faces simplified into geometric planes not photorealistic"
- Added to negatives: "Western cowboy, American frontier, prospector, Deadwood, gunslinger, saloon, three-dimensional modeling, rounded forms, individual facial features, pores, cards on table not in hands"

---

#### Run 2
**Seed:** 131978995726338
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 1.0

**Positive Prompt:**
> Paul Cézanne 1892 oil painting, muted earth tone palette, ochre and burnt sienna and dusty blue, structured geometric brushwork visible directional strokes building planes, matte unvarnished canvas surface, thick visible impasto, two French peasant men seated facing each other in profile at small wooden table, both holding playing cards in their hands, left man wearing blue smock smoking a long white clay pipe in his mouth, right man wearing brown jacket and yellow-tan hat, both men downcast eyes focused on their cards, dark wine bottle standing upright on table between them, warm ochre wall behind them, plain undetailed background, quiet contemplative still mood, Post-Impressionist painting technique, faces simplified into geometric planes not photorealistic, blocky simplified forms, flat planar rendering, painterly not photographic

**Negative Prompt:**
> photograph, photorealistic, hyperrealistic, smooth skin, detailed faces, individual facial features, pores, sharp focus, Renaissance, Baroque, neoclassical, academic painting, studio lighting, cinematic, film still, Hollywood, digital art, 3D render, illustration, anime, cartoon, polished, decorative, dramatic lighting, action, movement, Western cowboy, American frontier, prospector, Deadwood, gunslinger, saloon, three-dimensional modeling, rounded forms, atmospheric perspective, cards on table not in hands

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 2 | Background saturation cranked up to mustard yellow - lost the muted earthy quality, more Van Gogh than Cézanne |
| Brushwork visibility | 1 | No movement - surface still smooth and airbrushed, zero impasto despite explicit prompting |
| Planarity | 2 | Background flatter than Run 1 (accidental win), but figures remain fully 3D with heavy fabric modeling and dimensional forms |
| Compositional structure | 4 | Still strong - pipe added correctly, two-figure composition holds, bottle centered |
| Edge quality | 2 | No improvement - edges still soft and photographic |

**Qualitative Notes:**
- Pipe successfully added - decent clay pipe shape, not over-detailed ✅
- Left figure's grey cap closer to French peasant headwear ✅
- Background flatter and more painterly (accidental planarity win on background only) ✅
- Cowboy energy partially reduced - right figure's hat less Deadwood, more generic ✅
- Cards still on table, not in hands ❌ - explicit prompt ignored, appears to be model limitation
- Faces still photorealistic - beards rendered hair-by-hair, full dimensional modeling ❌
- Figures still fully 3D - heavy fabric folds on right figure's coat, rounded shoulders ❌
- Wine bottle more photorealistic than Run 1 - visible glass highlight
- Background saturation increased - lost muted quality
- **Verdict:** Flux responds to additive prompt changes (add pipe → get pipe) but resists transformative ones (make faces planar → still photorealistic). Suggests Flux's painterly understanding operates at the level of iconography (what objects appear) rather than technique (how paint is applied).

**Model Limitation Flagged:**
- "Cards in hands" prompt consistently ignored across runs. Flux appears to default to cards-on-table for this composition regardless of explicit instruction. Likely reflects training data distribution where Card Players reference images overwhelmingly show cards on table. Will not continue fighting this in subsequent runs.

**Prompt Changes for Run 3:**
- CFG 1.0 → 2.0 (test whether default CFG is underweighting technique prompts)
- Restructured prompt with more concrete material/process language
- Added: "broken color technique", "small unblended patches of distinct color", "visible canvas weave", "thick palette knife strokes"
- Added: specific hat descriptions ("tall dark bowler", "soft wide-brimmed tan hat")
- Added: "ochre orange tablecloth with visible folds"
- Removed: "Post-Impressionist" (too broad, possibly pulling Van Gogh saturation)
- Removed: "in profile" (OG is 3/4 profile, not pure silhouette)
- Removed: "cards in hands" prompts (model limitation, stop fighting)

---

#### Run 3
**Seed:** 943861662171654
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 2.0

**Positive Prompt:**
> Paul Cézanne 1892 oil painting The Card Players, broken color technique, small unblended patches of distinct color, visible canvas weave, thick palette knife strokes, muted earth tone palette, warm muddy brown and burnt sienna and ochre, two French peasant men seated at small table with heavy ochre orange tablecloth with visible folds, both heads tilted down toward cards on table, left man wearing tall dark bowler hat smoking long white clay pipe, dark jacket, right man wearing soft wide-brimmed tan hat and pale yellow-green jacket, dark wine bottle standing on tablecloth between them, dense painterly background of broken brushwork in mixed browns and greens, structural vertical elements behind figures, faces simplified into geometric planes, blocky simplified forms, flat planar rendering

**Negative Prompt:**
> photograph, photorealistic, hyperrealistic, smooth skin, detailed faces, individual facial features, pores, sharp focus, blended gradients, smooth shading, Renaissance, Baroque, neoclassical, academic painting, cinematic, film still, digital art, 3D render, illustration, anime, cartoon, polished, decorative, Western cowboy, prospector, three-dimensional modeling, rounded forms, atmospheric perspective, plain background, empty background, yellow saturated background, profile silhouette

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 4 | Tablecloth ochre/orange correct, figures in correct earth-tone family, but background went unexpected blue/green/peach color fields |
| Brushwork visibility | 3 | Major improvement - visible painterly brushwork across tablecloth, jackets, figures. First run with real surface texture. Still not impasto-thick |
| Planarity | 2 | Faces moved from photorealistic to painterly (category change), but figure bodies still fully 3D modeled with fabric folds and dimensional shoulders |
| Compositional structure | 4 | Hat specifications landed (tall bowler + wide-brimmed tan), pipe correct, tablecloth with folds correct, bottle centered |
| Edge quality | 3 | Edges now painterly rather than photographic, some softness appropriate to medium, slight CFG-induced sharpening artifacts |

**Qualitative Notes:**
- Faces rendered painterly for first time across all runs - simplified features, visible brushwork, no pore-level detail ✅
- Surface texture present across entire canvas - first run with visible paint application ✅
- Tablecloth correct: ochre orange with visible folds ✅
- Hat specifications landed correctly: tall dark bowler (left), wide-brimmed tan (right) ✅
- Pale yellow-green jacket on right figure landed ✅
- Bottle more painterly, less photorealistic glass highlight ✅
- Background went color-field abstract (Rothko-adjacent vertical blue/green/peach planes) ❌
- "Structural vertical elements behind figures" prompt language pulled color-field interpretation rather than tavern interior
- Removed "plain background" guardrail without sufficient replacement specification - Flux filled prompt gap with training data prior
- Figure bodies still fully 3D - fabric folds, rounded shoulders, dimensional modeling ❌
- Broken color technique not fully landed - surfaces painterly but still mostly blended, not Cézanne's distinct-patches quality ❌
- Minor CFG 2.0 artifacts: oversharpening around figures, fake signature scrawl bottom right
- **Verdict:** First run with category-level breakthrough. Flux moved off photorealistic default for the first time across both Murder and Card Players benchmarks.

**Key Finding (CFG):**
CFG 1.0 (Flux default) appears to underweight painterly technique prompts to the point where the model ignores them and defaults to photorealistic rendering regardless of prompt content. CFG 2.0 produces a category-level shift in how the model engages with technique language. However, the model still has strong priors it pulls toward when prompt regions are underspecified (e.g., background went color-field abstract when "plain wall" guardrail was removed without specific replacement).

Methodological implication: benchmarking Flux's painterly capability at CFG 1.0 may underestimate the model's ceiling. Future Cézanne benchmark runs across all periods should test at minimum CFG 1.0 and 2.0 to separate "model can't" from "model won't at default settings."

**Prompt Changes for Run 4:**
- Keep CFG 2.0
- Fix background specification: replace "structural vertical elements behind figures" (pulled color-field interpretation) with concrete tavern interior language
- Push harder on broken color: more specific patch language, possibly add color-mosaic descriptors
- Push harder on figure planarity: target body modeling specifically, not just faces

---

#### Run 4
**Seed:** 1031563174118991
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 2.0

**Positive Prompt:**
> Paul Cézanne 1892 oil painting The Card Players, broken color technique, mosaic of small distinct unblended color patches sitting next to each other, visible canvas weave, thick palette knife strokes, muted earth tone palette, warm muddy brown and burnt sienna and ochre, two French peasant men seated at small table with heavy ochre orange tablecloth with visible folds, both heads tilted down toward cards on table, left man wearing tall dark bowler hat smoking long white clay pipe, dark jacket simplified into flat geometric color blocks, right man wearing soft wide-brimmed tan hat and pale yellow-green jacket simplified into flat geometric color blocks, dark wine bottle standing on tablecloth between them, dimly lit rustic French tavern interior, dark wooden wall paneling behind figures, chaotic painterly background of broken brushwork in mixed dark browns olive greens and ochres, faces and bodies both rendered as flat geometric planes, blocky simplified forms, no fabric folds, no rounded shoulders, flat planar rendering throughout

**Negative Prompt:**
> photograph, photorealistic, hyperrealistic, smooth skin, detailed faces, individual facial features, pores, sharp focus, blended gradients, smooth shading, gradient shading, Renaissance, Baroque, neoclassical, academic painting, cinematic, film still, digital art, 3D render, illustration, anime, cartoon, polished, decorative, Western cowboy, prospector, three-dimensional modeling, rounded forms, fabric folds, dimensional shoulders, atmospheric perspective, color field abstract, Rothko, vertical color planes, geometric abstraction, plain background, empty background, modern abstract art

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 4 | Best palette across all runs - dark interior, ochre/orange tablecloth, muted figures. Background went cool green/teal instead of warm brown - directional miss but closer than Run 3 |
| Brushwork visibility | 3 | Similar to Run 3 - painterly surface texture present, no impasto, broken color still not landing |
| Planarity | 2 | No improvement on bodies despite explicit "flat geometric color blocks" + "no fabric folds" + "no rounded shoulders" pressure. Faces possibly backslid from Run 3 - more individualized features, dimensional rendering |
| Compositional structure | 4 | Strong overall - hats correct, tablecloth correct, two figures with downcast eyes, bottle centered. Pipe is comically oversized (Flux over-indexed on "long") |
| Edge quality | 3 | Painterly edges held, similar to Run 3, slight CFG sharpening artifacts |

**Qualitative Notes:**
- Rothko background eliminated ✅ - tavern interior anchor language ("rustic French tavern interior, dark wooden wall paneling") successfully replaced color-field abstraction
- Hat specifications held: tall dark bowler (left), wide-brimmed tan (right) ✅
- Tablecloth landed correctly: ochre orange with folds ✅
- Pale yellow jacket on right figure landed, closer to OG than Run 3's brighter green ✅
- Background went cool green/teal instead of warm muddy brown ❌ - "olive greens" in prompt pulled too hard, OG is warm reddish-brown with no green
- Pipe oversized to comedic degree ❌ - "long white clay pipe" prompt over-indexed on length
- Bodies still fully 3D ❌ - explicit "flat geometric color blocks" + "no fabric folds" + "no rounded shoulders" pressure failed to override Flux's representational prior on human bodies. Right figure shows clear fabric folds, dimensional shoulders
- Faces backslid from Run 3 - individual features returned, dimensional modeling on right figure's beard ❌
- Broken color technique still not landing - "mosaic of patches" language did not translate to visible patch-work in output ❌
- Some CFG 2.0 artifacts: slight oversharpening, mild oversaturation
- **Verdict:** Anchoring prompts work (background, tablecloth, hats), but prompts asking Flux to violate representational priors about human bodies do not, even at CFG 2.0 with explicit negatives.

**Key Finding (Representational Priors):**
Flux's prior on rendering human bodies as 3D dimensional objects appears to be effectively non-overridable through prompting alone. Across Runs 2, 3, and 4 — with progressively more aggressive planar language and explicit negatives — figure bodies continued to render with fabric folds, rounded shoulders, and full dimensional modeling. This suggests a possible asymmetry in what Flux can be steered toward: it can render an oversized pipe, an ochre tablecloth, or a tavern interior because these are object-level descriptions matching its training distribution, but it resists rendering humans in non-conventional ways because doing so requires overriding the dominant pattern in its human-figure training data.

This is potentially the central finding of the Card Players benchmark: **Flux can replicate Cézanne's iconography (objects, palette, composition) but not his fundamental challenge to representational seeing (planar reduction of three-dimensional form). The latter is what makes a Cézanne a Cézanne.**

**Prompt Changes for Run 5:**
- Hold CFG at 2.0 (save 2.5/3.0 experiments for still life painting)
- Background: drop "olive greens" entirely, push warm reddish-brown harder, add concrete material language ("warm reddish-brown wooden wall paneling, hanging dark drapery"), add to negatives: "green walls, teal, cool tones in background, dark green"
- Pipe: "long" → "small white clay pipe", add "oversized pipe, large pipe" to negatives
- Faces: restore Run 3 language ("faces simplified into geometric planes") rather than Run 4's combined face+body planar prompt
- Bodies: switch from geometric description to material/process language ("thick paint applied in flat slabs," "bodies built from broad palette knife strokes")
- Broken color: more concrete final attempt ("small visible square brushstrokes in distinct colors, paint not blended together")

---

#### Run 5
**Seed:** 1090061710567620
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 2.0

**Positive Prompt:**
> Paul Cézanne 1892 oil painting The Card Players, thick paint applied in flat slabs, small visible square brushstrokes in distinct colors paint not blended together, bodies built from broad palette knife strokes, visible canvas weave, muted earth tone palette, warm muddy brown and burnt sienna and ochre, two French peasant men seated at small table with heavy ochre orange tablecloth with visible folds, both heads tilted down toward cards on table, left man wearing tall dark bowler hat smoking small white clay pipe, dark jacket, right man wearing soft wide-brimmed tan hat and pale yellow-green jacket, dark wine bottle standing on tablecloth between them, dimly lit rustic French tavern interior, warm reddish-brown wooden wall paneling behind figures, hanging dark drapery, dense painterly background of broken brushwork in warm browns and burnt sienna and ochre, faces simplified into geometric planes, blocky simplified forms, flat planar rendering

**Negative Prompt:**
> photograph, photorealistic, hyperrealistic, smooth skin, detailed faces, individual facial features, pores, sharp focus, blended gradients, smooth shading, gradient shading, Renaissance, Baroque, neoclassical, academic painting, cinematic, film still, digital art, 3D render, illustration, anime, cartoon, polished, decorative, Western cowboy, prospector, three-dimensional modeling, rounded forms, fabric folds, dimensional shoulders, atmospheric perspective, color field abstract, Rothko, vertical color planes, geometric abstraction, plain background, empty background, modern abstract art, green walls, teal, cool tones in background, dark green, oversized pipe, large pipe

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 4 | Best background palette across all runs - warm reddish-brown wall paneling closest to OG's tonal family. Tablecloth slightly oversaturated, hat colors slightly off (right hat reading too white) |
| Brushwork visibility | 3 | Consistent with Runs 3-4 - painterly surface texture, no impasto, broken color technique did not land despite most concrete prompt attempt yet |
| Planarity | 2 | Faces marginally improved over Run 4 (closer to Run 3 quality after restoring face-specific language). Bodies unchanged - full fabric folds, dimensional shoulders, rounded forms persist |
| Compositional structure | 5 | Strongest compositional run - every iconographic element correct: pipe sized correctly, both hats present, bottle centered, cards visible on table, tablecloth folded, two figures with downcast eyes, drapery anchor in background |
| Edge quality | 3 | Consistent painterly edges, slight CFG-induced saturation and sharpening |

**Qualitative Notes:**
- Background warm reddish-brown landed ✅ - "warm reddish-brown wooden wall paneling" + "hanging dark drapery" + "warm browns and burnt sienna and ochre" successfully replaced Run 4's cool green/teal interior. Concrete material + object language worked
- Drapery anchor visible on right side of frame - direct prompt win ✅
- Pipe sized down successfully ✅ - "small white clay pipe" + "oversized pipe, large pipe" in negative corrected Run 4's comedic over-sizing
- Faces softened from Run 4 backslide ✅ - restoring Run 3's face-specific language ("faces simplified into geometric planes" only) helped
- Compositional iconography fully landed - every Cézanne object correct in placement and identification ✅
- Bodies still fully 3D ❌ - "thick paint applied in flat slabs" + "bodies built from broad palette knife strokes" (material/process language) failed to override body-modeling prior. Right figure shows clear fabric folds and dimensional shoulders consistent with Runs 1-4
- Broken color technique still not landing ❌ - "small visible square brushstrokes in distinct colors paint not blended together" produced no visible patch-mosaic effect. Surfaces remain gradient-shaded
- Saturation higher than OG - tablecloth orange louder than Cézanne's muted ochre, wall reds slightly oversaturated. Likely CFG 2.0 effect compounded with warm-color prompt density
- Cards on table, not in hands - consistent model limitation across all runs
- Faces still individualized rather than planar mask-like - faces partially improved but ceiling not broken
- **Verdict:** Strongest compositional run. Confirmed hard Flux limitations at CFG 2.0: body planarity and broken color technique cannot be prompted into.

---

### Painting 3: Fruit Bowl, Glass and Apples (Middle Period, 1879)

Note on session: early still-life attempts were discarded due to environment misconfiguration (an MPS CPU-fallback flag that degraded performance) and a series of prompt-driven non-convergence failures. The five runs below are the clean, scoreable series.

All runs: **Steps:** 10 | **Resolution:** 512x512 | **CFG:** 2.0 | randomized seeds verified via PNG metadata.

---

#### Run 1
**Seed:** 487149180013546
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 2.0

**Positive Prompt:**
> oil painting by Paul Cézanne, 1880, a white footed compote holding apples and green grapes, a clear glass, loose red and green apples on a rumpled white cloth, pale bluish-grey wall, bold dark outlines around the fruit

**Negative Prompt:**
> *(empty)*

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 3 | Reasonable cool/earth tones, hazy. Pale blue-grey ground in correct family |
| Brushwork visibility | 2 | Smooth, blended, no impasto or broken color |
| Planarity | 1 | Fully 3D, rounded volumetric bowl and fruit, honest perspective |
| Compositional structure | 4 | All objects present and correctly placed |
| Edge quality | 2 | Soft/hazy throughout - blurriest of the five |

**Qualitative Notes:**
- Clean-realism baseline. Renders reliably; objects converge for free ✅
- "Bold dark outlines around the fruit" did not produce visible contour outlines ❌
- No movement toward Cézanne technique in any dimension; this is Flux's default still-life register ❌

---

#### Run 2
**Seed:** 743952754383088
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 2.0

**Positive Prompt:**
> oil painting by Paul Cézanne, 1880, a white footed compote holding apples and green grapes, a clear glass, loose red and green apples on a rumpled white cloth, pale bluish-grey wall, bold dark outlines around the fruit, steeply tilted tabletop seen from a high angle, the table surface tipped up toward the viewer

**Negative Prompt:**
> *(empty)*

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 3 | Consistent with Run 1 |
| Brushwork visibility | 2 | Smooth, blended, no broken color |
| Planarity | 1 | Table stayed flat/realist. Tilt instruction largely ignored |
| Compositional structure | 4 | Objects correct; compote rim slightly more head-on than Run 1 |
| Edge quality | 3 | Sharper than Run 1 |

**Qualitative Notes:**
- Single controlled change from Run 1: the tilt clause added, everything else held ✅
- Image rendered cleanly but the tilt itself was dropped, table sits in normal perspective ❌ A marginal flatter-rim shift is visible but within plausible seed variance, not Cézanne's distortion
- Confirms the pattern: concrete geometry instructions are ignored rather than collapsing the image ✅

---

#### Run 3
**Seed:** 623841669068096
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 2.0

**Positive Prompt:**
> A post-impressionist oil painting of Paul Cézanne's Still Life with Fruit Dish. On a dark wooden table draped with a heavy, rumpled white cloth, sits a large white ceramic pedestal fruit bowl filled with red and orange apples and deep green grapes. In the foreground on the crumpled cloth, a cluster of apples in vibrant shades of forest green, ochre yellow, and deep brick red are loosely piled next to a rustic knife with a wooden handle. To the right, a translucent glass chalice partially filled with water stands against a background wallpaper of muted blue, slate gray, and pale green leafy patterns. The style features heavy, deliberate, directional brushstrokes, prominent dark blue and black outline contours around the fruit, shifting geometric planes, thick oil impasto texture, and a matte canvas finish, 1879 classical fine art.

**Negative Prompt:**
> 3D render, photorealistic, smooth gradients, digital art, high-definition, glowing highlights, airbrushed, vibrant modern colors, neon, glossy finish, minimalist, sharp photographic focus.

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 4 | Richest, most period-plausible palette of the five - wallpaper, varied fruit, drapery |
| Brushwork visibility | 2 | Still smooth/blended despite explicit impasto + contour requests |
| Planarity | 1 | Fully 3D, rounded volume, honest perspective |
| Compositional structure | 4 | All objects present, balanced, well placed |
| Edge quality | 3 | Crisper than Runs 1-2 |

**Qualitative Notes:**
- Full natural-language description, technique-heavy. Multi-variable change vs. the controlled Runs 1/2, exploratory not controlled
- Prettiest coherent render to this point ✅ but structurally the most academic: smooth modeled apples with realistic highlights, no broken color, no contour outlines, no flattening, no tilt, despite the prompt explicitly requesting all of them ❌
- "Shifting geometric planes" had no visible effect ❌

---

#### Run 4
**Seed:** 836659545732255
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 2.0

**Positive Prompt:**
> A rough, unfinished post-impressionist palette knife oil painting by Paul Cézanne. Crude oil paint texture, chunky heavy visible brushstrokes, visible coarse canvas weave. Flat primitive geometric shapes, distorted perspective, clunky form. Thick dark structural outline sketch lines drawn around objects. Muddy, muted, earthy tones of ochre, slate blue, and dark green. Raw impasto, broken color patches, deliberate artistic imperfections, 1879 art.

**Negative Prompt:**
> smooth shading, soft gradients, clean lines, perfect symmetry, photorealism, digital illustration, vector art, airbrushed, polished finish, 3D render, glossy, neat tablecloth, sharp details, modern wallpaper

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 4 | Muddy slate-blue/ochre/dark-green earth tones landed exactly as prompted |
| Brushwork visibility | 4 | Coarse canvas weave and impasto texture finally present - the only run where requested texture appeared |
| Planarity | n/a | No representational forms to assess |
| Compositional structure | 1 | No still life - abstraction, no bowl/fruit/table |
| Edge quality | n/a | No object edges |

**Qualitative Notes:**
- The cliff edge. Stacking anti-realist + texture + structural-distortion language past a threshold drove the model to abandon the representational scene entirely. Output is a Rothko-like field of dark green and ochre color blocks ❌
- Texture and palette survived ✅ the subject did not ❌ Same non-convergence failure mode as the discarded blank runs, but now carrying the requested surface qualities
- Boundary case, not a standard scored still life. Logged for the finding it produces: this is the **only** run where broken-color/impasto texture actually rendered ✅ and it required sacrificing the entire subject to get it ❌

---

#### Run 5
**Seed:** 670670667301540
**Steps:** 10 | **Resolution:** 512x512 | **CFG:** 2.0

**Positive Prompt:**
> A post-impressionist oil painting of Paul Cézanne's Still Life with Fruit Dish, 1879. On a dark wooden table draped with a heavy rumpled white cloth sits a white ceramic pedestal fruit bowl filled with red and orange apples and green grapes. In the foreground on the cloth, a loose pile of apples in forest green, ochre yellow, and brick red sits beside a knife with a wooden handle. To the right, a translucent glass of water stands before a wallpaper of muted blue, slate gray, and pale green leafy patterns. Painted with thick visible impasto brushstrokes and patches of broken color, warm earthy muted palette, matte oil-on-canvas finish.

**Negative Prompt:**
> photograph, photorealistic, 3D render, smooth gradients, airbrushed, glossy finish, digital art, sharp photographic focus

| Dimension | Score | Notes |
|-----------|-------------|-------|
| Palette accuracy | 4 | Rich, warm, period-plausible |
| Brushwork visibility | 2 | Smooth and blended despite explicit impasto + broken-color request |
| Planarity | 1 | Fully 3D, flawless rounded bowl, correct perspective |
| Compositional structure | 5 | Strongest composition of the five - every object placed and balanced |
| Edge quality | 4 | Sharpest, cleanest render of the session |

**Qualitative Notes:**
- Closer: Run 3's coherent base kept, only the "safe" texture words added; the structural-distortion language that collapsed Run 4 deliberately omitted; negative trimmed ✅
- Most beautiful render of the session and the most un-Cézanne ✅ Reads as photographic-realist oil: smooth volumetric glossy-highlighted apples, flawless rounded bowl, a crisp modern (not period-appropriate) glass tumbler, conventional lighting, obedient drapery
- Despite explicitly requesting impasto and broken color, the surface is smooth and blended, none present ❌ No flattening, no tilt, no contour outlines ❌
- **Verdict:** The clean bookend to Run 4. Pull the poison out and you get gorgeous academic realism with zero Cézanne technique; push it in and the scene collapses. No middle setting yields a coherent scene and Cézanne's structure simultaneously.

---

### Painting 4: The Forest (Late Period, 1894)
*[TBD - runs to be added]*

---

## Findings

### The Murder (Early Period, 1867): Results

Flux.1 can generate violent figurative scenes. It cannot generate Cezanne's violent figurative scenes.

Across five runs with progressively refined prompts, the model consistently defaulted to cinematic, photorealistic rendering regardless of explicit instructions to the contrary. Run 1 produced a Neoclassical wrestling scene lifted directly from the Romantic tradition. Runs 2 through 4, with increasingly specific negative prompting against Baroque, neoclassical, and photographic styles, produced what can best be described as a Victorian film still. Run 5, which led entirely with medium description rather than subject description, showed marginal improvement in painterly texture but did not escape the fundamental problem.

Flux's training distribution for "violent clothed figures" is overwhelmingly photographic and cinematic. Cezanne's treatment of this subject is essentially absent from that distribution. The model knows what a murder looks like. It does not know what Cezanne's decision to paint a murder crudely, flatly, and without academic finish looks like. That distinction is the entire point of the benchmark.

The Murder results illustrates that every prompt iteration that increased subject specificity pulled the model further toward photorealism, while every iteration that increased medium specificity improved texture but lost compositional accuracy. The model cannot hold both simultaneously.

### The Card Players (Middle Period, 1892): Results

Where the Murder benchmark exposed Flux's photorealism bias for figurative violence, the Card Players benchmark exposes something sharper: Flux can replicate Cézanne's iconography but cannot replicate his technique.

Across five runs, the model successfully converged on every object-level element of the painting — the two figures, the wine bottle centered between them, the ochre tablecloth with visible folds, the tall bowler hat, the wide-brimmed tan hat, the clay pipe, the warm reddish-brown tavern interior with hanging drapery. By Run 5, every iconographic element of Cézanne's composition was present and correctly placed.

What the model could not do, across any of the five runs, was render the figures the way Cézanne rendered them. The bodies in every output are fully three-dimensional — fabric folds, rounded shoulders, atmospheric modeling — despite increasingly aggressive prompting toward planar reduction. Three separate prompt strategies were attempted: explicit geometric description ("flat geometric planes"), negative prompting ("no fabric folds, no dimensional shoulders"), and material/process language ("thick paint applied in flat slabs"). All three failed. The bodies remained 3D.

The same pattern held for broken color, Cézanne's signature technique of placing small unblended patches of distinct color next to each other rather than blending them into gradients. Three runs with progressively concrete prompt language produced no visible patch-mosaic effect in any output. Flux's surfaces remained gradient-shaded throughout.

The Card Players benchmark also produced one methodological discovery: Flux at CFG 1.0 (its default) underweights painterly technique prompts to the point of ignoring them entirely. Bumping CFG to 2.0 in Run 3 produced an immediate category-level shift in how the model engaged with technique language — faces moved from photorealistic to painterly, surface texture appeared for the first time across the entire canvas. The implication is that benchmarking Flux's painterly capability at default CFG underestimates the model's ceiling. Future runs across all periods should test at minimum CFG 1.0 and 2.0 to separate "model can't" from "model won't at default settings."

The deeper finding is structural. Flux can replicate what a Cézanne painting *contains* but not how Cézanne *constructs* it. The model can dress an image up with Cézanne's iconography — the right objects, the right palette, the right composition — but cannot perform Cézanne's structural project, which is the planar reduction of three-dimensional form. That structural project is precisely what makes a Cézanne distinctly Cézanne rather than a generic 19th century genre painting. The benchmark is doing its job: it exposes a limitation that photo-based or generic creative benchmarks would never surface.

### Fruit Bowl, Glass and Apples (Middle Period, 1880): Results

The still life produces the sharpest finding of the benchmark so far. Flux defaults to competent realism and resists Cézanne's anti-realism, and it does so by one of two routes depending on how the prompt is phrased. The clearer the result, the further it sits from Cézanne.

Object convergence was never the constraint. Flux renders the compote, the apples, the grapes, the glass, and the draped cloth reliably, and with a dense enough prompt it renders them beautifully. What it cannot do is execute the instructions that make the painting a Cézanne: the tilted tabletop, the flattened space, the broken color, the dark contour outlines. Those instructions either collapse the generation or are silently dropped.

The collapse and the drop are two forms of the same refusal. Abstract or contradictory geometry ("planes flattened toward the picture surface," "the table seen from two angles at once") drove the model into non-convergence and produced blank canvases. A concrete, physically possible version of the same instruction ("steeply tilted tabletop seen from a high angle") rendered cleanly but with the tilt discarded, the table sitting in honest perspective. Abstract phrasing breaks the image and concrete phrasing is ignored, but neither yields the distortion.

The two extremes make the constraint explicit. Pushed hard with stacked anti-realist and texture language ("crude, flat, distorted, raw impasto, broken color patches"), the model abandoned the scene and resolved to a field of dark green and ochre color blocks: Cézanne's surface qualities present, the still life gone. Stripped back to a clean descriptive prompt, the model produced the most beautiful render of the session, smooth volumetric apples and a flawless rounded bowl in correct perspective, with none of the impasto or broken color the prompt explicitly requested. The first output is texture without a subject. The second is a subject without technique. No setting between them yields a coherent scene and Cézanne's structure at once.

The result holds across all three paintings. Flux is fluent in representational competence and cannot perform Cézanne's anti-representational project. It can give you Cézanne's surface or a coherent scene, but the harder the prompt pushes for the combination of surface and structural distortion that defines the work, the more the model has to discard the scene to comply.

*Results for The Forest to be added in a subsequent session.*

---

## Methodology Notes

- FID score skipped - requires 50+ images per period, overkill for this project
- CLIP score possible but noisy for fine art (trained on web images, not paintings)
- Resolution kept at 512x512 for speed; quality sufficient for rubric scoring
- Seeds verified via PNG metadata (`strings <file>.png | grep '"seed"'`) rather than ComfyUI UI display, which shows the next-queued seed under `randomize` mode rather than the current seed

---

*Generated with ComfyUI + Flux.1-dev Q4_K_S on M4 Mac, March 2026 - June 2026*
