# Acoustics and quantitative design rules for a high-pressure Budrio-style soprano ocarina in C5 (C5–F6)

Labels used below: **[PR]** = peer-reviewed or measured science; **[MK]** = maker or forum experience; **[INF]** = my own inference or calculation (not from a source).
Research limits: the session's web-search budget ran out and WebFetch was later rate-limited. The Ocarina Network (theocarinanetwork.com) sits behind Cloudflare and could not be read directly; I cite only search-result snippets from it, and each one is marked. Reference pitches: C5 = 523.25 Hz, F6 = 1396.9 Hz (A4 = 440 Hz), so F6/C5 = 2.670.

---

## 1. Helmholtz model: formulas, multiple holes, end corrections, wall thickness, window, and where the model fails

### Takeaway
Use the conductance form of the Helmholtz formula: f = (c/2π)·√(ΣK/V), where K = πr²/(t + δ) is the conductance of each opening. For a hole in a thin wall δ ≈ 1.57r–1.70r, so K ≈ 2r (proportional to the diameter, not the area). The makers' "D/V" formula is exactly this thin-wall limit. The lumped model on its own is not accurate enough to build from. The one ocarina CFD study found it predicted about 45% sharp (about 640 cents) for a small ocarina, mainly because the window/jet end correction is unknown. Always calibrate empirically on a prototype.

### Cited findings
- [PR] Helmholtz frequency f = (c/2π)·√(S/(V·L)), where L is the neck length plus end corrections. "The extra length… typically (and very approximately) of 0.6 times the radius at the outside end, and one radius at the inside end"; for a pipe opening into an infinite plane baffle the end correction is 0.85r. The model assumes the wavelength is much longer than the resonator. — [UNSW, Helmholtz Resonance](https://newt.phys.unsw.edu.au/jw/Helmholtz.html)
- [PR] Rayleigh conductivity of a circular aperture in a zero-thickness plate: K_R = 2r, which corresponds to an inertial end correction of πr/2. Rayleigh (1945) bounded the total end correction of a circular aperture between πr/2 ≈ 1.57r and 16r/3π ≈ 1.70r. For a plate of finite thickness, the thickness is added to the end correction. — [Laurens et al., arXiv 1401.1095 (JFM submission)](https://arxiv.org/pdf/1401.1095)
- [PR] Kobayashi, Takami, Miyamoto, Takahashi, Nishida, Aoyagi (Kyushu Univ./Kyushu Inst. Tech.), "3D Calculation with Compressible LES for Sound Vibration of Ocarina" (arXiv 0911.3567, OpenSource CFD Int. Conf. 2009), compressible LES in OpenFOAM 1.5 ("coodles" solver):
  - **2D model:** aperture 5 mm, cavity area 1.635 cm², maximum length 21.5 mm, jet velocities 20/30/40 m/s. At 20 m/s the oscillation was weak and unstable; at 30 and 40 m/s it was fully grown with "almost no higher harmonics". "As the velocity becomes larger, the frequency slightly increases." Resonance was about 2.5 kHz. Fitting the formula required an end-correction factor α ≈ 2.87, "large in comparison with α ≈ 16/3π in three-dimension". The authors attribute part of the gap to the jet over the aperture changing the open-end correction.
  - **3D model:** 5 × 5 mm² aperture, V = 9.425 cm³, jet at 10 m/s. The formula f ≈ (c/2π)·√(1.85a/V) predicts 1273 Hz; the LES gave 880 Hz, matching the real instrument the model was copied from (lowest note A5 = 880 Hz). The pressure oscillation "is synchronized over the whole cavity". The authors state that the textbook formula "contains various uncertain factors on the open-end correction around the edge hole". They also claim that "the placement of each hole on an ocarina is almost irrelevant". — [arXiv 0911.3567 (PDF)](https://arxiv.org/pdf/0911.3567)
- [PR] Follow-up Japanese conference abstracts by the same group: "3次元LESによるオカリナの発音機構の解明" (JPS 2010) and "オカリナの流体音響解析" / "…解析2" (Okada, Iwagami, Kobayashi, Takahashi; JPS 2018 and 2019). I could read only the titles and authors, not the abstracts. — [J-STAGE 2010](https://www.jstage.jst.go.jp/article/jpsgaiyo/65.1.2/0/65.1.2_297_1/_article/-char/ja/), [J-STAGE 2018](https://www.jstage.jst.go.jp/article/jpsgaiyo/73.2/0/73.2_2478/_article/-char/ja/), [J-STAGE 2019](https://www.jstage.jst.go.jp/article/jpsgaiyo/74.1/0/74.1_2931/_article/-char/ja/)
- [PR] A jet-whistled Helmholtz resonator (a beer bottle) gave 210 Hz against a lumped prediction of 208 Hz, using a fitted equivalent neck length of 47 mm. The first higher cavity mode was around 1550 Hz and carried negligible energy. So the lumped model is accurate when the neck is well defined and the effective length is fitted. — [Boujo et al., arXiv 1808.02677](https://arxiv.org/pdf/1808.02677)
- [PR] Printone (Umetani, Panotopoulou, Schmidt, Whiting; ACM TOG 2016 and ISMA 2017) used a boundary-element solver instead of the lumped formula to size finger holes on 3D-printed free-form fipple vessel instruments. Measured pitch was recorded as a range from softest to hardest clean blowing, because "higher speed produces higher frequencies". In 53 of 56 cases the target frequency fell inside the measured range. — [ISMA 2017 paper](https://isma2017.cirmmt.mcgill.ca/proceedings/pdf/ISMA_2017_paper_47.pdf); [ACM DL](https://dl.acm.org/doi/10.1145/2980179.2980250)
- [MK] Pure Ocarinas (Robert Hickman): "The pitch produced is determined by the area of all of the open holes combined", and "the exact locations of the finger holes on an ocarina does not matter that much". — [pureocarinas.com/how-ocarinas-work](https://pureocarinas.com/how-ocarinas-work)
- [MK] Euphonics: the pitch depends on "the chamber volume and the combined area and 'neck length' of the open holes", and "it doesn't matter which particular holes you cover". — [euphonics.org 4.2](https://euphonics.org/4-2-acoustic-resonators/)
- [MK] Wikipedia (citing Hickman): pitch is also affected by "the thickness of the material the holes are cut in". — [Wikipedia: Vessel flute](https://en.wikipedia.org/wiki/Vessel_flute)
- [MK, search snippet only] The Ocarina Network tutorial "Making an Ocarina in a Predetermined Key" gives V = 1/(((F/2148.14)²)/D), i.e. F = 2148.14·√(D/V), with D the hole diameter. — [TON t10093](https://theocarinanetwork.com/tutorial-making-an-ocarina-in-a-predetermined-key-t10093.html)

### Inferences
- [INF] The constant 2148.14 = c/2π with c in inches per second (2148.14 × 2π = 13,497 in/s = 342.8 m/s). The formula therefore uses inches and cubic inches and is exactly Rayleigh's thin-plate result K = 2r = D. In SI units: f = (c/2π)·√(ΣD_i/V) with c/2π ≈ 54.6 m/s. In workshop units this is f ≈ 1726·√(ΣD[mm]/V[cm³]) Hz, valid for the thin-wall limit only.
- [INF] Two consequences of K ≈ 2r:
  - In thin walls, pitch scales with the *sum of diameters*, not the sum of areas. Two 5 mm holes (ΣD = 10 mm) raise pitch more than one 7.07 mm hole of the same total area.
  - In thick walls (t comparable to r), K ≈ πr²/(t + 1.6r) tends toward being area-driven. A thicker wall lowers every hole's conductance, so holes must be larger. Terracotta walls of 4–6 mm with 4–10 mm holes sit squarely in the transition regime, so neither the "area" nor the "diameter" rule is exact.
- [INF] Required conductance range for C5–F6: f² ∝ ΣK, so (1396.9/523.25)² = 7.13. With all holes closed, the window/embouchure alone must supply the C5 conductance K_w. With all holes open, the total must reach about 7.1·K_w, so the ten finger/thumb holes together must add about 6.1·K_w. Window conductance is also what the jet perturbs most (the α ≈ 2.87 vs 1.70 finding), so determine K_w empirically. The practical recipe:
  1. Build the prototype chamber and voicing.
  2. Measure the all-closed pitch; this fixes K_w/V.
  3. Size the holes progressively.
- [INF] Worked estimate of where the model fails: the 3D LES gave 880 Hz against 1273 Hz predicted, a ratio of 1.447, about +640 cents of error. For a vessel with a jet-loaded window, treat the textbook formula only as a starting estimate that tends to predict too sharp. A finger resting near an open hole adds effective length and flattens it further.
- [INF] Upper validity limit: the lumped model needs the chamber to be much smaller than a wavelength. For a chamber of internal length L, the first longitudinal cavity mode is about c/2L. At L = 100 mm that is about 1.7 kHz, only about 4 semitones above F6. Keep the soprano chamber compact (roughly ≤ 80–90 mm internal length) so that this mode stays well above F6. This bound comes from theory only; I found no measured source for ocarinas.

### Gaps
- No published measured end correction exists for a jet-driven ocarina window, and none for holes in curved terracotta walls with a finger nearby.
- Fletcher & Rossing's vessel-flute section and Benade (pp. 473–476) could not be accessed online.
- The Kyushu group's 2018–2019 ocarina results (abstracts) could not be read.

---

## 2. What the scientific literature says (papers found)

### Takeaway
Ocarina-specific peer-reviewed acoustics is very thin. Beyond the Kyushu CFD work (arXiv 0911.3567 and its JPS abstracts) and Printone (BEM design of 3D-printed vessel flutes), I found no JASA, Acta Acustica or Applied Acoustics paper, and no Korean KCI/KSNVE paper, specifically on ocarinas. The usable quantitative science comes from recorder and flue-pipe studies (Fabre, Verge, Hirschberg, Ségoufin, Auvray, Terrien, Price).

### Cited findings
- [PR] Kobayashi et al. 2009 (see section 1). — [arXiv 0911.3567](https://arxiv.org/abs/0911.3567)
- [PR] Miyamoto et al. (same group), "Numerical study on sound vibration of an air-reed instrument with compressible LES" (a pipe, not an ocarina):
  - At low jet speed (V ≤ 8 m/s) the frequency rises in proportion to V, like an edge tone.
  - At higher speeds it locks to the resonator.
  - Uses Brown's edge-tone law ν = 0.466 j (100V − 40)(1/(100l) − 0.07), with l the flue-to-edge distance and j = 1, 2.3, 3.8, 5.4; the jumps between stages are hysteretic.
  - [arXiv 1005.3413](https://arxiv.org/pdf/1005.3413)
- [PR] Printone (Umetani et al. 2016/2017): see section 1. — [ISMA 2017](https://isma2017.cirmmt.mcgill.ca/proceedings/pdf/ISMA_2017_paper_47.pdf)
- [PR] Recorder and flue literature:
  - Ségoufin, Fabre, Verge, Hirschberg, Wijnands 2000, Acustica 86:649–661 (windway length and chamfers). — [TU/e portal](https://research.tue.nl/en/publications/experimental-study-of-the-influence-of-the-mouth-geometry-on-soun/)
  - Fabre, Gilbert, Hirschberg, Pelorson 2012, "Aeroacoustics of Musical Instruments", Annu. Rev. Fluid Mech. 44:1–25. — [Annual Reviews](https://www.annualreviews.org/content/journals/10.1146/annurev-fluid-120710-101031)
  - Terrien et al. — [arXiv 1207.7136](https://arxiv.org/pdf/1207.7136), [arXiv 1403.7487](https://arxiv.org/pdf/1403.7487)
  - Auvray et al. — [arXiv 1601.05545](https://arxiv.org/pdf/1601.05545)
  - Price et al., JASA 138:3282 (2015). — [arXiv 1502.02170](https://arxiv.org/pdf/1502.02170)
  - Details are in sections 3–4.
- [PR] Korean: searches returned only general Helmholtz-resonator papers, for example a KSME paper noting that the traditional Helmholtz formula lacks cavity and neck shape information and deriving correction relations. I found no ocarina-specific acoustics paper; the Korean ocarina theses located were music-education theses. — [KCI ART001863402](https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART001863402); [Busan thesis 2006](http://cfile201.uf.daum.net/attach/1660003A504C6E07187704)
- [PR] Brazil: "Confecção de ocarina para educação musical" (Unicamp PIBIC abstract, 2019); not read. — [DOI 10.20396/revpibic2720192052](https://doi.org/10.20396/revpibic2720192052)

### Inferences
- [INF] For a Budrio-style design, no scientific paper supplies dimensions. Design rules must be transferred from recorder and flue-pipe physics plus maker practice, then validated by prototype measurement.

### Gaps
- No thesis or dissertation specifically on ocarina acoustics was found.
- No J-STAGE Acoustical Society of Japan journal paper was found (only JPS abstracts).
- I could not verify whether a Chaigne & Kergomard "Flute-like instruments" (Springer 2016) section covers vessel flutes.

---

## 3. Windway and labium geometry: rules and effects

### Takeaway
The key dimensionless ratio is the cut-up W (windway exit to edge) against windway exit height h. Recorders use W/h ≈ 4; flue organ pipes go up to about 12. Jet waves travel at about 0.4 of the jet velocity, so the jet velocity that best drives a note scales with f·W, and the blowing pressure scales with (f·W)².
- A longer window (larger W) means higher pressure, a steeper curve, and louder high notes.
- A short, wide window means flatter pressure, balanced volume, and a smaller range.
- Chamfers on a long windway stabilise the tone and widen the dynamic range.
- A shorter windway gives a brighter sound but overblows at lower pressure.
- The edge offset y0 relative to the jet axis controls harmonic content.

### Cited findings
- [PR] Jet-drive model: jet disturbances convect at c_p ≈ 0.4u₀ and grow as e^(αx) with α ≈ 0.3/h (h = slot height). Delay τ = w/c_p. Oscillation requires the phase condition arg(Y) + π/2 − ωτ = 2mπ. The playing frequency rises with the inverse Strouhal number u₀/(ωw). — [Euphonics 11.8.1](https://euphonics.org/11-8-1-the-jet-drive-model-for-a-recorder-or-flute/)
- [PR] "c_v ≈ 0.4U_j… τ = W/c_v." — [Terrien et al., arXiv 1403.7487](https://arxiv.org/pdf/1403.7487)
- [PR] The ratio W/h "is close to 4 in recorder-like instruments whereas it can reach 12 in flue organ pipes". A small W/h is why recorders do not operate on the 2nd hydrodynamic jet mode. — [Terrien, Vergez, Fabre, arXiv 1207.7136](https://arxiv.org/pdf/1207.7136)
- [PR] Measured recorder mouth (Yamaha YRT-304B II tenor):
  - Windway length 7.20 cm, width 1.47 cm.
  - Height tapers from 1.95 mm at the inlet to 1.09 mm at the exit, so the windway is convergent.
  - Two 45° chamfers extend 0.7 mm; the labium sits W = 4.83 mm from the outlet, giving W/h ≈ 4.4.
  - With 45° chamfers the jet disturbance per unit acoustic cross-flow is "about a factor of two smaller" than for a square exit.
  - Edge-tone experiments showed that "the threshold for oscillation moves to lower jet velocities when chamfers are added".
  - [Price, Johnston, McKinnon, arXiv 1502.02170 / JASA 138:3282](https://arxiv.org/pdf/1502.02170)
- [PR] Recorder-like laboratory model: W = 4 mm, h = 1 mm, labium offset y0 = 0.1 mm. "Another parameter that has a great impact on the spectral content is the offset y0 between the channel axis and the labium as shown by Fletcher." — [Auvray et al., arXiv 1601.05545](https://arxiv.org/pdf/1601.05545)
- [PR] Ségoufin et al. 2000: "Shortening the channel seems to allow a better control of the instrument at low blowing pressures and makes the sound spectrum richer in high harmonics, but it also reduces considerably the pressure at which the instrument overblows. Adding chamfers to a long windway greatly stabilizes the system and gives the instrumentalist a wider dynamical playing range on a given mode… Adding chamfers to a short windway doesn't help." — [TU/e](https://research.tue.nl/en/publications/experimental-study-of-the-influence-of-the-mouth-geometry-on-soun/)
- [PR] Flue-pipe voicing uses Ising's dimensionless intonation number, which relates jet velocity V = √(2P/ρ), jet (flue) thickness D, cut-up height H and frequency F. "When I=2 the jet has optimal conditions to drive the pipe fundamental"; I should be "more than 2 but less than 3". I could not open the page with the exact formula (fonema.se and mmdigest failed), so the formula is not reproduced here. — [search summary of fonema.se/mmdigest pages](https://www.mmdigest.com/Tech/isingform.html); [fonema.se](http://www.fonema.se/ising/isint.htm)
- [PR] Organ-pipe practice defines the Strouhal number Sr = f₀H/U (H = cut-up) as "decisive"; the dimensionless jet velocity is θ = U/(fW). — [search summary of ResearchGate figure / Archives of Acoustics](https://acoustics.ippt.pan.pl/index.php/aa/article/view/2651)
- [MK] Pure Ocarinas on the sound hole (window):
  - "Long narrow sound holes require the player to blow harder as higher notes are played. The high notes tend to be louder than the low."
  - "Wide and short sound holes play with an almost constant blowing pressure… balanced volume, and tend to produce a smaller total range."
  - Large sound holes "generally sound more breathy… louder overall, and need more air".
  - Shape: teardrop gives a "very pure" timbre; rectangular a "strongly textured, 'reedy'" one; round is "moderately 'buzzy'".
  - [Pure Ocarinas: playing characteristics & timbre](https://pureocarinas.com/ocarina-playing-characteristics-timbre)
- [MK] Breath-curve determinants: chamber volume relative to pitch, sound-hole size, "the distance between the windway exit and labium", number of holes, "how restricted the windway is", and the tuning. — [Pure Ocarinas: breath curve](https://pureocarinas.com/ocarina-breath-curves)
- [MK] Typical sound-hole size: 12-hole alto C about 7–9 mm; 10-hole alto C about 8–10 mm (search-snippet summary of Pure Ocarinas). — [Pure Ocarinas](https://pureocarinas.com/identifying-playable-ocarinas)

### Inferences
- [INF] Pressure scaling. If the player keeps the jet near an optimal Strouhal number, u ∝ f·W and p = ½ρu² ∝ ρ(f·W)².
  - Two consequences follow: at fixed pitch, doubling the cut-up W needs about 4× the pressure, and across C5→F6 at fixed W the ideal pressure rises by up to 2.67² ≈ 7×.
  - This is the physical root of the "long window = high pressure, steep curve" maker rule. For a Budrio-style high-pressure, high-projection soprano: use a relatively long cut-up (larger W) with h chosen so that W/h stays in the recorder-like range of about 3–5.
  - This numeric window is an inference from recorder data, not ocarina data.
  - A W/h far above about 5–6 moves toward organ-pipe behaviour, where higher jet modes and "aeolian" squeaks become possible.
- [INF] Higher pressure means a faster jet, more jet kinetic power (∝ p^1.5 × slot area), and therefore more acoustic power. That is consistent with Pure Ocarinas' "larger chamber and sound hole → higher pressure and louder".
- [INF] Chamfers and a long, gently convergent windway (like the Yamaha 1.95 → 1.09 mm taper) favour stability at high pressure, which a high-pressure design needs. Place the edge nearly on the jet axis; a small offset y0 changes the even/odd harmonic balance, i.e. timbre.

### Gaps
- No source gives ocarina-specific windway height or cut-up values; Budrio windway dimensions were not found.
- The exact Ising formula could not be verified.
- No quantitative data on edge sharpness or edge angle for ocarinas was found.

---

## 4. Blowing-curve physics and pressure ranges

### Takeaway
Pitch rises with pressure because the jet transit delay τ = W/(0.4u) shrinks as u grows. To keep the loop phase satisfied, the oscillation moves up the resonator's phase curve. A broad, low-Q Helmholtz resonance lets this shift reach several semitones. The only quantitative ocarina pressure data I found (Pure Ocarinas, arbitrary units, 10-hole C instrument C–F) shows the high F needing about 2.3× the pressure of low C at 0 cents, and being about 10× less pitch-sensitive to pressure.

### Cited findings
- [PR] Phase condition and frequency rising with u₀/(ωw): see section 3. — [Euphonics 11.8.1](https://euphonics.org/11-8-1-the-jet-drive-model-for-a-recorder-or-flute/)
- [PR] In LES the ocarina frequency "slightly increases" with jet velocity, which the authors describe as the "broad resonance which is often observed in ocarina". — [arXiv 0911.3567](https://arxiv.org/pdf/0911.3567)
- [MK] "Breath force can change the pitch by several semitones", but only about a third of a semitone (about 30 cents) is practically usable in complex music. — [Wikipedia: Vessel flute](https://en.wikipedia.org/wiki/Vessel_flute)
- [MK/measured, arbitrary units] A Pure Ocarinas study measured a 10-hole C ocarina (low C to high F) with a pressure transducer tapped beside the windway (Arduino, uncalibrated "units"), at 20 °C, pre-warmed:

  | cents vs A440 | C | D | E | F | G | A | B | C' | D' | E' | F' |
  |---|---|---|---|---|---|---|---|---|---|---|---|
  | −40 | 30 | 31 | 33 | 32 | 33 | 33 | 35 | 37 | 41 | 50 | 56 |
  | −20 | 34 | 35 | 39 | 42 | 43 | 43 | 46 | 49 | 55 | 63 | 68 |
  | 0 | 36 | 39 | 44 | 46 | 48 | 51 | 54 | 61 | 69 | 75 | 83 |
  | +20 | 39 | 43 | 48 | 51 | 57 | 61 | 69 | 78 | 85 | 103 | 121 |

  "Raising from zero cents to plus 20 required a change of 3 units on the low end (36 to 39), but 38 units on the high end (83 to 121)." — [Pure Ocarinas study](https://pureocarinas.com/study-ocarina-breath-curves-temperature)
- [MK] The curve is "approximately exponential… as you play higher notes, a larger pressure change is required from one note to the next". "The low notes are much more sensitive to pressure changes." — [Pure Ocarinas: breath curve](https://pureocarinas.com/ocarina-breath-curves)
- [MK] Measuring a breath curve: hold a note in tune, lift the next finger without changing pressure, and read how flat the new note is. A well-tuned example shows about 18–21 cents per step, regular across the range. Errors of 5–10 cents are "not normally noticeable"; 30 or more are hard to compensate. — [Pure Ocarinas: measure breath curve](https://pureocarinas.com/measure-ocarina-breath-curve)
- [MK] 10-hole ocarinas (C5–F6 type) can be made to "play at high pressure, sounding very loud throughout the entire range" or with increasing pressure; 12-hole ocarinas "play with a steep pressure curve". A smaller range allows "a strong, clean sound through the whole range". — [Pure Ocarinas: types](https://pureocarinas.com/types-of-ocarina); [10 vs 12 hole](https://pureocarinas.com/differance-10-hole-12-hole-ocarina)

### Inferences
- [INF] Local sensitivity from the table around 0 cents: low C gives about 20 cents per 3 units, high F about 20 cents per 38 units, a ratio of roughly 13×. The high notes of a Budrio C5–F6 are therefore pressure-stable but need much more air. The low notes are "pressure-sensitive" and determine how fine the pitch control has to be.
- [INF] How designers set curve steepness: the maker chooses the tuning pressure for each note by sizing its hole. A slightly smaller hole means a flatter note at a given pressure, so the player must blow harder to bring it up to pitch. Tuning the upper holes smaller relative to "Helmholtz-ideal" steepens the curve; tuning them larger flattens it. Window length W sets the baseline via p ∝ (fW)². This agrees with Pure Ocarinas listing "how the maker tuned the ocarina" as a factor.
- [INF] Absolute pressures in Pa or mmH₂O for low-pressure (Asian) versus high-pressure (Italian) ocarinas were **not found in any source**. As a physics-only order of magnitude: a 10 m/s jet corresponds to ½ρu² ≈ 60 Pa (about 6 mmH₂O), and 30 m/s to about 540 Pa (about 55 mmH₂O). The CFD model sounded at 10–40 m/s. These are calculations, not measurements. A cheap U-tube water manometer or an MPX-type sensor tapped beside the windway (as in the Pure Ocarinas study) would let the builder calibrate their own curve.

### Gaps
- No calibrated measurement of ocarina mouth pressure (Pa) exists in the sources found.
- No source compares the pressure of Budrio or Italian ocarinas with Asian ones numerically.

---

## 5. Holes: position, size versus wall thickness, timbre, sub-holes, tuning holes

### Takeaway
Hole position matters little for pitch, which depends only on total conductance. It does matter for high-note tone, and holes cannot exceed the chamber's internal diameter. Small holes in thick walls act as longer necks and need larger diameters. In a soprano, a high-aspect-ratio chamber is used so that the fingers fit.

### Cited findings
- [MK] "The size of a finger hole can never exceed the internal diameter of the chamber"; beyond that, "the chamber itself becomes the limiting factor and the pitch cannot rise".
  - On high notes, "the air oscillating in the chamber seems to enter/exit via the hole, effectively bypassing the air in the section of chamber downstream of the hole… reducing the mass of air in oscillation… resulting in the cleaner tone".
  - Soprano ocarinas therefore need "a high aspect ratio chamber".
  - [Pure Ocarinas: chamber shape & range](https://pureocarinas.com/ocarina-chamber-shape-range-chamber-volume-bypassing)
- [MK] "hole size also depends on chamber shape and wall thickness"; small sound holes are much louder on high notes. — [Pure Ocarinas: timbre](https://pureocarinas.com/ocarina-playing-characteristics-timbre)
- [MK] Split or sub-holes: in Dietrich's patent, "the smaller of the holes that make up the split tonehole… is sized to alter the pitch… by one semitone". — [US7816595B1](https://patents.google.com/patent/US7816595)
- [PR] Hole-conductance physics (K = 2r thin; thickness adds to the end correction): see section 1. — [arXiv 1401.1095](https://arxiv.org/pdf/1401.1095)

### Inferences
- [INF] With f² ∝ K_w + ΣK_open, successive chromatic notes need conductance increments that grow geometrically. Each semitone needs 2^(2/12) = 1.122× the total conductance, so ΔK grows about 12% per semitone. On a 10-hole C5–F6, holes opened later in the sequence are therefore generally larger. Thumb holes are usually the largest because they open last.
- [INF] Tuning practice: tune flat before firing, as the brief states. Enlarging a hole in a 5 mm terracotta wall changes K roughly between ∝ r (thin limit) and ∝ r² (thick limit). Make small steps, and bevel or undercut the inside edge: this shortens the effective neck and raises pitch without enlarging the visible hole.
- [INF] Keep finger holes away from the window/jet region, where they could disturb the jet. I found no measured source on this.

### Gaps
- No published hole-diameter progressions for Budrio or Mignani instruments were found; the TON thread "Hole size differences between different ocarina brands" was inaccessible.
- No Hickman book formulas were verified (the book was not accessible).

---

## 6. Chamber shape, wall thickness, material, moisture

### Takeaway
The walls barely vibrate, so the material matters mainly through porosity (damping, moisture absorption) and through wall thickness as neck length. Unglazed terracotta absorbs condensation, which is an advantage for the windway.

### Cited findings
- [MK] "only the air is vibrating. The material of the instrument is just acting as a container and has very little impact on the sound." — [Pure Ocarinas: how ocarinas work](https://pureocarinas.com/how-ocarinas-work)
- [MK] Porous materials "can act to damp oscillations", and "non-porous vitrified ceramic [ocarinas] do sound different from more common earthenware". "Earthenware ocarinas never suffer from condensation or moisture build up as condensation soaks into the porosity." Plastic ocarinas accumulate moisture "including inside the windway". — [Pure Ocarinas: materials](https://pureocarinas.com/ocarina-materials-finish-differences)
- [PR] Helmholtz output is almost free of harmonics (LES spectra: "almost no higher harmonics"). The pressure is uniform across the cavity, so the fundamental does not depend on cavity shape. — [arXiv 0911.3567](https://arxiv.org/pdf/0911.3567)
- [MK] "overtones are many octaves above the keynote scale" because of the egg shape. — [Wikipedia: Vessel flute](https://en.wikipedia.org/wiki/Vessel_flute)

### Inferences
- [INF] For the press-mould workflow: keep the inside surface of the windway and labium smooth. Leave the chamber interior unglazed and porous for moisture absorption. Keep wall thickness at the finger holes consistent between the two halves, because thickness changes K and so pitch.

### Gaps
- No measured data on how wall thickness affects timbre or projection.

---

## 7. Typical numbers for a C5 soprano

### Takeaway
I found no published chamber volume, hole-area total or windway cross-section for C5 soprano or Budrio ocarinas. The only hard vessel numbers are from the CFD model: an A5 (880 Hz) instrument of about 9.4 cm³ with a 5 × 5 mm window.

### Cited findings
- [PR] A5 ocarina model: V = 9.425 cm³, aperture 25 mm², jet 10 m/s, sounding 880 Hz. — [arXiv 0911.3567](https://arxiv.org/pdf/0911.3567)
- [MK] Alto C sound holes of about 7–10 mm (search summary). — [Pure Ocarinas](https://pureocarinas.com/identifying-playable-ocarinas)

### Inferences
- [INF] Scaling with a similar window: f² ∝ K_w/V. Going from A5 (880 Hz) down to C5 (523 Hz) at the same window needs V × (880/523)² ≈ 2.83×, i.e. about 27 cm³.
  - This is only a scaling estimate: a high-pressure design uses a *larger* window, so V would be larger still. Following Pure Ocarinas, "larger chamber and sound hole → higher pressure, louder".
  - Treat 25–40 cm³ as an order-of-magnitude starting range, to be checked by prototype.
- [INF] Measure the chamber volume of the reference Mignani Do 3 directly: weigh it dry, fill it with water or fine dry sand through the window with holes taped, then weigh again. Also measure the window length × width, the windway exit height and the hole diameters. These are the only reliable numbers for a Budrio clone.

### Gaps
- No Budrio, Mignani or Menaglio dimensions were found in the scientific or maker sources I accessed.

---

## 8. Temperature, humidity and CO₂ during playing

### Takeaway
Theory gives about 2.9 cents/°C (f ∝ √T). But the air inside a played ocarina is a mix of breath and ambient air, so the measured ambient-temperature sensitivity is smaller: about 1–1.9 cents/°C. Breath CO₂ lowers pitch, while breath heat and water vapour raise it.

### Cited findings
- [PR] Δf/f ≈ ΔT/600 K − 0.30ΔC + 0.16ΔH, with ΔC and ΔH the molar fractions of CO₂ and H₂O.
  - A 1% rise in frequency needs ΔT ≈ +6 °C, or ΔC ≈ −3%, or ΔH ≈ +6%.
  - Exhaled CO₂ is about 4%, which alone gives a little more than 1% lower sound speed.
  - On a trombone, resonances first fall (from CO₂), then return to near or above ambient.
  - Oboe and bassoon fall about 10 cents in the 10 s after inhalation.
  - Brass: 1.2–2.6 cents/°C.
  - [Boutin, Smith, Wolfe, JASA 148:1817 (2020)](https://www.phys.unsw.edu.au/jw/reprints/warming.pdf)
- [MK] Ocarina pitch "changes linearly at about 1 cent per degree Celsius" of ambient air. The voicing mixes breath with ambient air. About ±15 °C from the tuning temperature is tolerable. — [Pure Ocarinas: air temperature](https://pureocarinas.com/ocarina-air-temperature-pitch)
- [MK/measured] High F measured at "best sound" pressure, cold instrument, first breath: 2.5 °C → −39 cents, 10 → −25, 14 → −19, 20 → −7, 22 → −3. The author states "approximately 9 cents per 10 degrees", **but his own data span 36 cents over 19.5 °C, about 1.8 cents/°C**; the text and the table conflict. — [Pure Ocarinas study](https://pureocarinas.com/study-ocarina-breath-curves-temperature)

### Inferences
- [INF] For Goiânia (typically warm): tune at a temperature close to the expected playing conditions, for example about 25 °C. With the Budrio design, the pressure-stable high notes show temperature error most clearly, because the player cannot bend them back without large pressure changes.

### Gaps
- No ocarina-specific measurement of CO₂ or humidity inside the chamber was found.

---

## 9. Maker calculators versus physics

### Takeaway
The maker formula F = 2148.14·√(D/V) is Rayleigh's thin-wall Helmholtz conductance in inch units. It ignores wall thickness, the window's jet-modified end correction, and blowing-pressure pitch shift, so it serves only as a first-pass estimate.

### Cited findings
- [MK, snippet] V = 1/(((F/2148.14)²)/D). — [TON tutorial](https://theocarinanetwork.com/tutorial-making-an-ocarina-in-a-predetermined-key-t10093.html)
- [MK] A thread titled "Testing the Helmholtz formula" exists but was inaccessible. — [TON t13419](https://theocarinanetwork.com/testing-the-helmholtz-formula-t13419.html)
- [MK] Robert Hickman's book *The Art of Ocarina Making* covers voicing and tuning of 10/11/12/4-hole ocarinas; its content was not accessible. — [Google Books](https://books.google.com/books/about/The_Art_Of_Ocarina_Making.html?id=JsGJDwAAQBAJ)
- [PR] BEM (Printone) outperforms lumped estimates for free-form shapes, and its hole-size "AutoTune" optimisation works for 3D-printed instruments. — [ISMA 2017](https://isma2017.cirmmt.mcgill.ca/proceedings/pdf/ISMA_2017_paper_47.pdf)

### Inferences
- [INF] The formula ignores the window: its output is the finger-hole-only resonance and needs an empirical correction of possibly hundreds of cents (see the +640-cent CFD example). The practical design loop:
  1. 3D-print a PLA acoustic prototype with the same internal volume and wall thickness as the fired target. Scale for shrinkage only in the mould master.
  2. Voice it and measure the all-closed pitch and the breath curve.
  3. Iterate hole sizes on the print.
  4. Transfer to the master, with holes left undersize for post-firing enlargement.
