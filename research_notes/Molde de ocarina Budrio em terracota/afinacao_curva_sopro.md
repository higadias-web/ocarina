# Afinação de ocarinas e curva de sopro (breath curve): como replicar a afinação e a voz de uma Budrio Do 3 (Mignani, C5–F6, 10 furos)

Notes by research subagent, 2026-09-28. Labels used: **[FATO]** measured or technical fact, **[MAKER]** maker or player experience, **[INFERÊNCIA]** my own derivation, which should be checked. Limits on access: the Ocarina Network forum (Cloudflare), Reddit and MIMF blocked automated access, and my web-search budget ran out partway through. Some maker claims are therefore marked "via search snippet". I could not verify them in full.

---

## 1. Maker tuning workflows (order of operations, how much to enlarge, drying and firing, tolerances)

### Takeaway
Published maker practice has four parts. First, set the chamber and voicing so the all-closed note sounds well. Next, open the finger holes **one at a time, from small, in fingering order from low to high**, checking each with a tuner. Aim flat, by an amount set by the shrinkage still to come. Finally, finish after firing by enlarging holes. No published source gives "mm per cent". This can be derived from Helmholtz scaling (see the inferences below). About 5–10 cents of error between adjacent notes is not noticeable. About 30 cents or more is a real problem.

### Cited Findings
- [MAKER] "Cut and tune one hole at a time. Enlarging a hole raises its pitch, so start small and enlarge each hole until you achieve the pitch you want." (Barry Hall) — [Ceramic Arts Network](https://ceramicartsnetwork.org/daily/article/Making-Music-with-Clay-How-to-Make-a-Ceramic-Ocarina)
- [MAKER] Order matters: "follow the order of the holes from lowest to highest, because if you adjust a hole's diameter after the higher-note holes are already finished, you'll also change their pitch". The same article says the base note is set by the size of the sound hole/outlet. It is written by a retailer's blog editor, not a maker. — [Instruments du Monde](https://instruments-du-monde.com/en-us/blogs/ocarina/how-to-tune-ocarina)
- [MAKER] Robert Hickman (Pure Ocarinas / ocarinamaking.com) gives this procedure for vessel flutes, shown on a xun:
  - Mark the hole positions with a light drill mark while holding the instrument.
  - Find the lowest note with a tuner.
  - Open the holes "one at a time using a chromatic tuner", in fingering order, keeping earlier holes in the pattern closed where the fingering requires it.
  - For voicing, start the sound hole small (~6 mm) and enlarge it "until you get a strong sound". As a guideline, 8–11 mm suits an alto C.
  - A plaster mould is "the easiest way" to reach concert keys repeatably.
  — [ocarinamaking.com, How to make a Xun](https://ocarinamaking.com/page/how_to_make_a_xun)
- [MAKER] The breath curve is **built during tuning**: "The pressure curve is created when an ocarina is made by tuning sequential notes slightly flat, requiring you to raise your pressure to compensate." — [Pure Ocarinas, measure breath curve](https://pureocarinas.com/measure-ocarina-breath-curve)
- [MAKER] Pure Ocarinas tunes each instrument's holes individually, "twice to catch errors". It wipes glaze out of the finger holes because glaze in the holes changes the tuning. — [Pure Ocarinas (search summary of shop/about pages)](https://pureocarinas.com/about-pure-ocarinas)
- [MAKER, via search snippet; the page is behind Cloudflare and I did not read it in full] From Ocarina Network threads:
  - "Most makers do major tuning a little before the leather hard state", with the tuner set to allow for later shrinkage.
  - Tune flat, because pitch rises "usually significantly" by the end of firing, depending on the clay.
  - One maker reports a rise of ~15–20 cents; another experienced maker reports only ~5 cents.
  - For an alto C, one maker says shrinkage raises pitch by about a half-step.
  - Some makers (e.g., Jade Everett) tune after firing with a Dremel and a dust mask.
  - Makers aim for every piece to leave the kiln slightly flat, then file holes.
  — [Ocarina Network: Tuning an occarina](https://theocarinanetwork.com/tuning-an-occarina-t22633.html); [Ocarina Network: Your homemade ocarinas p.19](https://theocarinanetwork.com/your-homemade-ocarinas-t8314-s180.html)
- [FATO / MAKER] Pure Ocarinas' tolerances for the step between adjacent notes: "5 to 10 cents is not normally noticeable"; "30 or more will be difficult to compensate for when playing at a moderate tempo". — [Pure Ocarinas](https://pureocarinas.com/measure-ocarina-breath-curve)
- [MAKER] Visual check: hole sizes should follow the scale pattern, with larger holes for whole steps and smaller ones for semitones. "Any ocarina with all holes the same size has not been tuned". "Larger holes indicat[e] a higher pressure instrument." — [Pure Ocarinas, identifying playable ocarinas](https://pureocarinas.com/identifying-playable-ocarinas)
- [MAKER] Quality tests:
  - Each note should overblow "at least a semitone" above its named pitch without screeching.
  - Response should be even across the range.
  - Nothing should screech on tongued high notes.
  — [Pure Ocarinas](https://pureocarinas.com/identifying-playable-ocarinas)

### Inferences
- **[INFERÊNCIA] Shrinkage sets the pre-firing offset.** A Helmholtz resonator scaled uniformly by a linear factor (1−s) has its frequency multiplied by 1/(1−s). This follows from f = (c/2π)·√(A/(V·L_eq)) ([Wikipedia, Helmholtz resonance](https://en.wikipedia.org/wiki/Helmholtz_resonance)), with A ∝ L², V ∝ L³ and L_eq ∝ L.
  - Pitch rise ≈ **20.8 cents per 1% of linear shrinkage still to happen** after you tune.
  - About 5% remaining shrinkage gives ~89 cents (≈ the reported "half tone"). About 1% gives ~17 cents (≈ the reported "15–20 cents").
  - Rule: offset (cents) = 1200·log2(1/(1−s_rest)), where s_rest is the linear shrinkage from the clay state at tuning to the fired state. Measure s_rest on test bars of the *same* clay, fired in the *same* kiln and cone.
  - To first order the shift is equal in cents for every note, so the *shape* of the breath curve survives firing. Warping, and scaling of the windway and labium distance, may break this. That point is unverified.
- **[INFERÊNCIA] Tuning order.** Opening a hole adds its conductance to every higher note that also has it open. Tune in fingering order upward:
  1. All-closed C5, set by chamber and voicing.
  2. Right hand: pinky (D), ring (E), middle (F), index (G).
  3. Left hand: ring (A), middle (B), index (C6).
  4. Left thumb (D6), left pinky (E6), right thumb (F6).
  5. Then check the chromatic cross-fingerings. On a 10-hole with no subholes, "thumbs first" has no advantage.
- **[INFERÊNCIA] How much to enlarge (idealized Helmholtz, same blowing pressure).** Frequency goes as √(ΣK), where K is each opening's acoustic conductance. Raising a note by c cents therefore needs its total K raised by (2^(c/600) − 1): **≈1.16% per 10 cents**.
  - Put onto the hole just opened: +10 cents needs its conductance up ≈5.6% if that hole makes a whole-tone step, or ≈10.7% if it makes a semitone step.
  - For thin-walled holes, conductance scales roughly with **diameter** rather than area (next section). So +10 cents ≈ +5–6% in diameter on a whole-tone hole (≈0.4 mm on a 7 mm hole). A semitone hole needs roughly twice that in percentage terms.
  - These are starting estimates. Always measure.
- **[INFERÊNCIA] Moisture while tuning.** Clay tuned wetter has more shrinkage left, so it needs a larger flat offset. It also changes faster as it dries, so readings drift. Tune at one consistent state and do test pieces with the same clay. No source quantified pitch against moisture content. Note too that a leather-hard chamber exchanges humid air, and humidity has a small effect: 0→100% RH is less than a 2 °C temperature change ([Wikipedia, Vessel flute](https://en.wikipedia.org/wiki/Vessel_flute)).

### Gaps
- No verifiable maker source gives specific numbers for undercutting holes. Undercutting reduces effective wall thickness, so it raises conductance and pitch, but this is unquantified.
- No source gives a cents-vs-% moisture relation.
- I could not read the Ocarina Network threads in full.
- No source says whether Budrio makers tune at leather-hard or after firing.

---

## 2. Breath curve: definition, measurement, design; high vs low pressure

### Takeaway
The breath curve is the blowing pressure needed to play each note in tune, plotted across the range. Naturally it is roughly exponential. The maker shapes it by leaving each successive note slightly flat at constant pressure. Chamber volume, sound-hole size and labium distance set whether the instrument is high or low pressure. For a loud Budrio-type instrument, published design logic points to a larger chamber and sound hole, larger finger holes, and a steeper curve.

### Cited Findings
- [FATO / MAKER] Definition: "how your blowing pressure must change over an ocarina's range to produce a clean tone and play in tune". The natural curve is "approximately exponential". Its shape depends on:
  - chamber volume relative to pitch,
  - sound-hole size,
  - distance from windway exit to labium,
  - number of holes,
  - windway restriction,
  - the maker's tuning.
  — [Pure Ocarinas, breath curve](https://pureocarinas.com/ocarina-breath-curves)
- [MAKER] "Ocarinas that have a larger chamber volume and sound hole play with a higher pressure and are louder. Ocarinas with a smaller chamber volume and sound hole play at a lower blowing pressure and are quieter." Long, narrow sound holes need rising pressure. Wider sound holes with the labium closer to the windway exit play at almost constant pressure. — [Pure Ocarinas, playing characteristics](https://pureocarinas.com/ocarina-playing-characteristics-timbre)
- [MAKER] Ten-hole ocarinas leave freedom to design any of three behaviours:
  - low pressure with balanced volume,
  - "high pressure, with the instrument sounding very loud throughout the entire range",
  - rising pressure, with quiet lows and loud highs.
  Twelve-hole ocarinas are forced into a steep curve. — [Pure Ocarinas, 10 vs 12 hole](https://pureocarinas.com/differance-10-hole-12-hole-ocarina)
- [MAKER] Sound-hole sizes: a 12-hole alto C is about 7–9 mm; a 10-hole alto C about 8–10 mm. Louder ocarinas have larger sound holes and need more air. — [Pure Ocarinas](https://pureocarinas.com/identifying-playable-ocarinas)
- [MAKER] Fabio Menaglio's Budrio ocarinas are "airy by design … designed to fill large music halls and have a large voicing to achieve a high volume". — [Pure Ocarinas, airy high notes](https://pureocarinas.com/why-ocarina-airy-high-notes)
- [MAKER] Measurement method without a manometer:
  1. Finger a note and hold it in tune.
  2. Without changing pressure, and **without tonguing**, lift the finger for the next note of the primary major scale.
  3. Read how many cents flat it sounds "at the exact moment you lift your finger".
  4. Start at the lowest note, repeat, and average.
  - Good example: steps about equal (C:20, D:21, E:19 … cents). Steps that shrink gradually (20, 19, 18 … 13) make the curve more linear.
  - Irregular jumps (0, 40, 60, 10, −10 …) are tuning errors.
  - Traps: subconscious pressure compensation (which reads as a false flat curve) and tuners with needle damping, low sampling rate or high latency. The author recommends a software tuner with a numeric cents readout (e.g., APTuner) and belly breathing.
  — [Pure Ocarinas](https://pureocarinas.com/measure-ocarina-breath-curve)
- [FATO, amateur-grade] Pressure-vs-pitch data from one ocarina, measured with a transducer "from a tube alongside the instrument's windway" plus an Arduino, in **uncalibrated** units (ADC minus zero offset), at 20±1 °C:
  - Low C needs 30/34/36/39 units at −40/−20/0/+20 cents.
  - High F needs 56/68/83/121.
  - In-tune (0 cents) row, C→F: 36, 39, 44, 46, 48, 51, 54, 61, 69, 75, 83.
  - The author notes quantization error on the low notes.
  — [Pure Ocarinas, temperature study](https://pureocarinas.com/study-ocarina-breath-curves-temperature)
- [MAKER] The pitch of high notes is "much less sensitive to pressure variation than the low notes". This limits how much you can compensate. Adding holes makes the top notes even less pressure-sensitive. — [Pure Ocarinas, temperature](https://pureocarinas.com/ocarina-air-temperature-pitch); [Pure Ocarinas, warm/cold](https://pureocarinas.com/ocarina-tutorial/playing-ocarinas-in-warm-or-cold-environments)
- [MAKER] A steep curve limits speed: "if you need to blow an ocarina very hard, it is difficult to play at high tempo". You should keep pressure headroom for vibrato and bends. — [Pure Ocarinas, warm/cold](https://pureocarinas.com/ocarina-tutorial/playing-ocarinas-in-warm-or-cold-environments)
- [MAKER] Breath force can move pitch "by several semitones", and "high notes tend to go sharp; the low notes, flat". Campin says pitch varies by about a tone with blowing. The Italian ocarina is "most pressure-sensitive at the top end", and on some instruments "the top two notes are so out of tune or whispery as to be useless". — [Wikipedia, Vessel flute](https://en.wikipedia.org/wiki/Vessel_flute); [Campin, The Italian Ocarina](http://www.campin.me.uk/Music/Ocarina/)
  - Conflict: Pure Ocarinas says the top notes are *less* pressure-sensitive in pitch. Campin's "pressure-sensitive" plausibly refers to tone breaking up.
- [MAKER] Andy Cormier's blog classifies curves qualitatively as linear, flat or concave and states it has no measurements. — [Andy Cormier](https://andycormier.blog/2024/02/10/what-is-the-breath-curve-of-an-ocarina/)

### Inferences
- **[INFERÊNCIA] Relative pressure sensitivity from Pure Ocarinas' table.**
  - Near 0 cents, low C moves about 40 cents for a ~14% pressure change, i.e. ~29 cents per +10% pressure.
  - High F needs ~64% more pressure for the same 40 cents, i.e. ~6 cents per +10%.
  - So the low notes are ~4–5× more pitch-sensitive to relative pressure. This is valid only if the zero offset was removed correctly, and it comes from one instrument.
  - Consequence: the flat step you read at constant pressure mostly reflects hole tuning at the low end, but it maps to large pressure changes at the top.
- **[INFERÊNCIA] Target for "steep curve, high projection".** Copy the reference's cents-flat-per-step profile, measured by the same method in the same conditions. A larger total (the sum of steps across the range) means a steeper curve. Cheap Asian instruments are no good as a numerical benchmark.
- **[INFERÊNCIA] Curve vs holes vs windway.**
  - Hole sizes set *where* each note sits relative to the one before (the step size).
  - Windway cross-section and height, sound-hole size, and labium distance set the absolute pressure level and loudness, and how far the top notes can be pushed before screeching.
  - To copy, reproduce the voicing geometry exactly first (from the master), then tune the holes to the reference's step profile.

### Gaps
- I found **no published calibrated per-note pressures (Pa, mmH2O) for any Budrio ocarina**, nor any Italian vs Asian pressure comparison with numbers.
- The only absolute number found is "the highest pressure I've ever observed was 19 centimetres of water, about 0.27 PSI" (≈1.86 kPa), for Pure Ocarinas instruments measured with a U-tube — [Pure Ocarinas](https://pureocarinas.com/study-ocarina-breath-curves-temperature). A high-pressure Budrio may exceed this, which is unverified.
- I found no STL, Focalink, Songbird or Mountain pages quantifying curves (search budget exhausted).

---

## 3. Measuring pressure: without a manometer, and cheap options

### Cited Findings
- [MAKER] A water U-tube manometer works, but "the water takes several seconds to stop moving after pressure is applied". Common dial and digital gauges are useless at these pressures. The author instead used a low-range pressure transducer plus Arduino ADC, tapping "a tube alongside the instrument's windway". He then learned that lower-range transducers would give better resolution. He does not name the part. — [Pure Ocarinas](https://pureocarinas.com/study-ocarina-breath-curves-temperature)
- [FATO] Bosch BMP280 is an *absolute* barometer:
  - range 300–1100 hPa;
  - relative accuracy ±0.12 hPa (±12 Pa);
  - RMS noise down to 1.3 Pa and resolution 0.16 Pa in ultra-high-resolution mode;
  - temperature coefficient 1.5 Pa/K;
  - output data rate up to 157 Hz, in low-resolution settings.
  — [Bosch BMP280 datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bmp280-ds001.pdf)
- [FATO] Sensirion SDP810-500Pa is a differential sensor:
  - range ±500 Pa;
  - accuracy 3% of measured value;
  - zero-point accuracy 0.1 Pa;
  - I²C output, up to 2 kHz.
  — [Sensirion SDP810-500Pa](https://sensirion.com/products/catalog/SDP810-500Pa)
- [FATO] pYIN (librosa.pyin) uses Viterbi decoding over YIN candidates. `resolution` is the pitch-bin size in semitones: default 0.1, and "0.01 corresponds to cents". Frame length defaults to 2048. Reference: Mauch & Dixon, ICASSP 2014. — [librosa.pyin docs](https://librosa.org/doc/0.11.0/generated/librosa.pyin.html)

### Inferences
- **[INFERÊNCIA] Sensor choice.**
  - ±500 Pa (≈5 cmH2O) would probably **saturate** on a high-pressure ocarina if players reach ~19 cmH2O ≈ 1.9 kPa.
  - A ±2 kPa differential part (e.g., the MPXV7002DP family, often used with Arduino) is a better fit for range. I could not retrieve its datasheet, so check the specs.
  - A BMP280 in a sealed tube can measure gauge pressure as the reading minus an ambient baseline. It has range to spare, but it is slow for fast transitions.
  - A water U-tube reading mm of water is fine for *static* per-note checks: 1 mmH2O ≈ 9.8 Pa.
  - Tap the mouth pressure with a thin tube at the corner of the mouth or beside the windway, as Pure Ocarinas did.
- **[INFERÊNCIA] Why the no-manometer method still copies the curve.** Relative data (cents-flat per step at constant pressure) captures the *shape* of the curve. Absolute pressure matters only for checking that the copy is a "high-pressure" instrument. That can be done later by playing both instruments against the same U-tube.

---

## 4. Published breath-pressure numbers

### Takeaway
Almost none exist. The only figures found are Pure Ocarinas' maximum of about 19 cmH2O and its uncalibrated relative table, and a CFD paper that uses jet speeds rather than pressures.

### Cited Findings
- [FATO] ~19 cmH2O maximum observed (U-tube), on Pure Ocarinas instruments. — [Pure Ocarinas](https://pureocarinas.com/study-ocarina-breath-curves-temperature)
- [FATO] A 2D/3D compressible LES simulation of an ocarina used jet velocities of 20–40 m/s. The frequency changes with jet velocity. — [arXiv 0911.3567](https://arxiv.org/pdf/0911.3567)

### Inferences
- **[INFERÊNCIA]** By Bernoulli, jet speed v = √(2p/ρ). So 20–40 m/s corresponds to roughly 240–960 Pa (≈2.5–10 cmH2O) at the windway, before losses. This is the same order of magnitude as the U-tube figure.

### Gaps
- No Budrio or Italian numbers were found. No Asian maker pressure figures were verified.

---

## 5. Italian/Budrio 10-hole fingering, compared with the Asian 12-hole; pitch standard

### Takeaway
The Budrio Do 3 has 8 finger holes on top, 2 thumb holes, and no subholes. Its range is C5–F6. Lifting fingers from the right pinky up to the left index gives C5→C6. Then the left thumb gives D6, the **left pinky gives E6**, and the right thumb gives F6. The Asian system reverses E6 and F6 (right thumb first). I found no documented pitch standard (A440 vs 442) for Budrio makers.

### Cited Findings
- [FATO] Jack Campin's chart for a C ocarina, Italian system.
  - Notation: T = left thumb, t = right thumb; 1–4 = index…little finger; "-" = open; "/" = half-hole. Left hand is written first.
  - Chart:
    - C `T1234 t1234`
    - C♯ `T1234 t1234/` (half-hole)
    - D `T1234 t123-`
    - E♭ `T1234 t12-4`
    - E `T1234 t12--`
    - F `T1234 t1---`
    - F♯ `T1234 t--3-`
    - G `T1234 t----`
    - G♯ `T12-4 t--3-`
    - A `T12-4 t----`
    - B♭ `T1--4 t--3-`
    - B `T1--4 t----`
    - c `T---4 t----`
    - c♯ `-1--4 t----`
    - d `----4 t----`
    - e♭ `----4 -----` (Italian)
    - e `----- t----` (Italian)
    - f `----- -----`
  - The Austrian system swaps e♭ and e: e♭ = `----- t----`, e = `----4 -----`.
  - In the Italian system "the left-hand little finger hole is larger than the right thumbhole", and the other way round in the Austrian one.
  - Some instruments have a split right-pinky hole for low C♯.
  - The top notes are the most pressure-sensitive, and on some instruments they are unusable.
  — [Campin, The Italian Ocarina](http://www.campin.me.uk/Music/Ocarina/) (Italian version: [PDF](http://www.campin.me.uk/Music/Ocarina/Italiano.pdf))
- [FATO] Pure Ocarinas describes the same systems. On the left hand, the ring finger lifts first while the pinky stays down. The Asian high register is left thumb → D, right thumb → E. The Italian system "reverses the ordering of two notes" and "allows one more note to be played without moving the right thumb". "E is played on the pinky and F on the thumb." — [Pure Ocarinas, fingering system](https://pureocarinas.com/ocarina-fingering-system); [Pure Ocarinas, high notes](https://pureocarinas.com/ocarina-tutorial/play-hold-ocarina-high-notes)
- [FATO] A 12-hole is the same 10-hole layout plus two subholes, which extend the range down three semitones (a 12-hole C runs A–F). — [Pure Ocarinas, 10 vs 12](https://pureocarinas.com/differance-10-hole-12-hole-ocarina)
- [FATO] Fabio Menaglio (Budrio) Do 3: "chromatic (C5–F6) – 10 fori – cm 17,5 x 8,5 – 215 gr". The left pinky "deve chiudere un foro ovale largo 9 mm" (must close an oval hole 9 mm wide). Other left-pinky hole widths: Do 1 6 mm, Sol 2 8 mm, Sol 4 11 mm. — [ocarina.it (Menaglio), acquista](https://www.ocarina.it/acquista.html)
- [FATO] Donati's consort naming, low to high: C7, G6, C5, G4, C3, G2, C1. The instrument's pitch is named after the note with all holes closed. — [Campin](http://www.campin.me.uk/Music/Ocarina/)
- [FATO] Pitch depends essentially on the total open hole area (more precisely, conductance), not on which holes are open. This allows alternative and microtonal fingerings. — [Campin](http://www.campin.me.uk/Music/Ocarina/); [Pure Ocarinas, how ocarinas work](https://pureocarinas.com/how-ocarinas-work)

### Inferences
- **[INFERÊNCIA] The theory explains the hole sizes.** In the ideal model, cumulative conductance K_n = K_0·2^(semitones/6).
  - Conductance each hole adds, relative to the sound hole's K_0:
    - right pinky 0.26
    - right ring 0.33
    - right middle 0.19
    - right index 0.46
    - left ring 0.58
    - left middle 0.74
    - left index 0.44
    - left thumb 1.04
    - **left pinky 1.31**
    - right thumb 0.78
  - This matches Campin (in the Italian system the left pinky hole is bigger than the right thumb hole) and Menaglio (the left pinky is the big 9 mm oval).
  - With everything open at F6, the total is ≈7.1 × K_0.
  - Real holes will be somewhat smaller than this, because each note is left slightly flat to build the curve.
- **[INFERÊNCIA] Pitch standard.** A = 442 Hz is +7.85 cents relative to 440. If your analysis of the reference shows a consistent offset of about +8 cents across all notes, at the tuning pressure and a normal temperature, that suggests 442. Report results against 440 and let the data decide.

### Gaps
- No source for Mignani-specific hole sizes, or for the pitch standard Budrio makers use.
- No chromatic fingering chart specific to Mignani.

---

## 6. Copying the reference: per-note pressure profile, hole areas, back-calculating the Helmholtz volume

### Takeaway
The breath-curve recording already contains a fingerprint of each hole. At constant pressure, f_{n+1}² − f_n² is proportional to the conductance k_i/V that hole adds. Measure the hole diameters and wall thickness with calipers, and you can back-calculate V and check your master. Then tune the copy to reproduce the same cents-flat-per-step list.

### Cited Findings
- [FATO] Helmholtz: f = (c/2π)·√(A/(V·L_eq)), with L_eq the neck length plus end correction. — [Wikipedia, Helmholtz resonance](https://en.wikipedia.org/wiki/Helmholtz_resonance)
  - End corrections are "very approximately" 0.6 r at the outside end and 1 r at the inside end. — [UNSW, J. Wolfe, Helmholtz](https://newt.phys.unsw.edu.au/jw/Helmholtz.html)
  - Wikipedia's vessel-flute article gives f ∝ A/V **without the square root**. This conflicts with the standard formula, so treat it as an error. — [Wikipedia, Vessel flute](https://en.wikipedia.org/wiki/Vessel_flute)
- [FATO] No closed-form formula for multiple necks was offered on Physics Forums (thread unresolved). — [Physics Forums](https://www.physicsforums.com/threads/helmholtz-resonator-with-multiple-necks-formula.948401/)
- [FATO] One open-source calculator assumes the total open *area* sets pitch and was unvalidated when checked. — [GitHub ocarina-calculator](https://github.com/Phauxelate/ocarina-calculator)
- [FATO] Location of the holes matters little. The whole chamber oscillates. — [Pure Ocarinas, how ocarinas work](https://pureocarinas.com/how-ocarinas-work)

### Inferences (worked procedure)
- **[INFERÊNCIA] Conductance of each hole.** Holes act in parallel, so their conductances k = A/L_eq add: f = (c/2π)·√(Σk/V).
  - For a round hole of radius r in a wall of thickness t: k ≈ πr²/(t + ~1.6r), using Wolfe's end corrections.
  - When t is much smaller than r, k ≈ 2r. So it scales with **diameter, not area**. This is why the "total area" rule is only approximate.
  - For ovals, use the equivalent-area radius (approximate).
- **[INFERÊNCIA] Back-calculating V.** Take consecutive notes n and n+1 from the constant-pressure segments of the breath-curve recording: V ≈ (c/2π)²·k_i/(f_{n+1}² − f_n²).
  - Use c = 331.3·√(1 + T/273.15) m/s with T = the chamber air temperature. Chamber temperature is not the room temperature, so there is uncertainty here.
  - Average over several holes and use the median. Outliers point to a hole whose effective k differs, e.g. because of undercutting or finger shading.
  - Compare with the internal volume of your 3D master, scaled by the clay shrinkage.
- **[INFERÊNCIA] What to replicate.**
  1. The voicing geometry exactly: windway section and height, sound-hole length × width, labium distance and angle. These set the pressure level and projection.
  2. The chamber volume, corrected for shrinkage.
  3. The **list of cents-flat-per-step** from the reference, within about ±5 cents.
  4. The all-closed pitch at a stated temperature.
  - Since the constant-pressure method gives cents directly, you can tune the copy by playing *both* instruments with the same routine: tune hole i of the copy until its step matches the reference's step i.

### Gaps
- No maker's or acoustician's worked example back-calculating ocarina volume was found.
- The jet also shifts frequency with pressure, so the passive Helmholtz values are approximate. That is why pairs taken at the same pressure are preferred.

---

## 7. Recording and analysis best practice for pitch in cents

### Cited Findings
- [MAKER] Microphone placement:
  - "somewhat above the ocarina and slightly to the left or right";
  - avoid the air stream in front of the voicing, or use a pop filter;
  - closer placement captures less room sound;
  - cardioid or shotgun pickup rejects the room;
  - small-diaphragm condenser or ribbon microphones work well.
  — [Pure Ocarinas, recording](https://pureocarinas.com/how-to-record-an-ocarina)
- [MAKER] The pure timbre makes ocarinas prone to comb filtering from room reflections. — [Pure Ocarinas](https://pureocarinas.com/why-ocarina-airy-high-notes)
- [MAKER] Tuner pitfalls: needle damping, low sampling rate, latency, and no numeric cents display. — [Pure Ocarinas](https://pureocarinas.com/measure-ocarina-breath-curve)
- [FATO] pYIN bins pitch with `resolution` (default 0.1 semitone; 0.01 = cents). — [librosa.pyin](https://librosa.org/doc/0.11.0/generated/librosa.pyin.html)
- [FATO] Barometric pressure does not affect pitch. The effect of humidity is less than a 2 °C change. — [Wikipedia, Vessel flute](https://en.wikipedia.org/wiki/Vessel_flute)
  - For Goiânia, altitude is irrelevant; temperature matters.

### Inferences
- **[INFERÊNCIA] Recording.** 48 kHz mono WAV, mic at ~30–50 cm, above and to the side, outside the jet. Record notes of 2–4 s held steady.
- **[INFERÊNCIA] Extraction.**
  - Use librosa.pyin with `resolution=0.01`, or YIN with interpolation. Frames of ~2048 samples at 48 kHz (~43 ms).
  - Drop ~80–100 ms of transient after each onset or finger change.
  - Take the **median** frequency over the steady segment.
  - Cents vs ET = 1200·log2(f/f_ref), with f_ref from A4 = 440.
- **[INFERÊNCIA] Breath-curve segments.**
  - Reference = the median over the last ~200–300 ms before the finger lift.
  - Measured = the median over ~50–250 ms after the lift, before the player compensates.
  - Step flatness = (expected ET interval) − (measured interval).
  - Average the 3 cycles and report the spread. A spread above ~5 cents means the player's pressure stability, not the algorithm, is limiting accuracy.
  - On a near-sinusoidal signal the algorithm error should be well below 1 cent. The human is the main source of error.
- **[INFERÊNCIA] Temperature.** Log room temperature. Pre-warm the instrument with 5 long breaths, as Pure Ocarinas did.

### Gaps
- No verified accuracy spec for tuner apps.

---

## 8. Temperature (beyond "2.9 cents/°C")

### Cited Findings
- [FATO / MAKER] For ambient temperature changes, a played ocarina shifts about **1 cent/°C**. Pure Ocarinas also gives 0.9 cents/°C and "9 cents per 10 degrees". The reason is that the voicing mixes breath with ambient air, so the internal temperature settles between the two. — [Pure Ocarinas, temperature](https://pureocarinas.com/ocarina-air-temperature-pitch); [Pure Ocarinas, warm/cold](https://pureocarinas.com/ocarina-tutorial/playing-ocarinas-in-warm-or-cold-environments)
- **Discrepancy:** the author's own table (high F at 2.5→22 °C: −39→−3 cents) gives a least-squares slope of **≈1.8 cents/°C** (my calculation). That is double the stated rate but still below the theoretical ~2.95 cents/°C. — [Pure Ocarinas study](https://pureocarinas.com/study-ocarina-breath-curves-temperature)
- [MAKER] Temperature changes the *shape* of the curve.
  - Cold makes the curve steeper at the top; high notes screech before reaching pitch.
  - Warm makes it shallower.
  - The usable compensation is about ±5 °C (5–10 cents) for fast music and up to ±20 °C (30 cents) for easy music.
  - Makers "should always specify the temperature an ocarina was tuned" at.
  - An instrument already tuned high-pressure has less room to compensate for cold.
  — [Pure Ocarinas, warm/cold](https://pureocarinas.com/ocarina-tutorial/playing-ocarinas-in-warm-or-cold-environments); [Pure Ocarinas study](https://pureocarinas.com/study-ocarina-breath-curves-temperature)

### Inferences
- **[INFERÊNCIA]** An Italian reference was probably voiced for around 20 °C (unverified). Goiânia runs warmer. Measure the reference and the copy at the same room temperature, and state the tuning temperature for the copy.

---

## 9. Common problems and fixes

### Cited Findings
- [MAKER] Flat, airy high notes are usually underblowing, dirt in the windway, fingers shading the holes, or the airstream hitting the palm. In a badly made instrument the cause is a sound hole that is too large for the chamber volume. — [Pure Ocarinas, high notes flat](https://pureocarinas.com/why-ocarina-high-notes-flat); [Pure Ocarinas, airy](https://pureocarinas.com/why-ocarina-airy-high-notes); [Pure Ocarinas, playable](https://pureocarinas.com/identifying-playable-ocarinas)
- [MAKER] Screeching high notes come from overblowing, a cold environment, or a poor instrument ("poorly tuned, its chamber volume and voicing mismatched, or a poor chamber shape"). — [Pure Ocarinas, screech](https://pureocarinas.com/why-ocarina-screech-high-notes)
- [MAKER] The low C is less stable than the higher notes. — [Campin](http://www.campin.me.uk/Music/Ocarina/)
- [MAKER] "Acute bend" is an illusion; a well-made instrument should not need it. — [Pure Ocarinas](https://pureocarinas.com/identifying-playable-ocarinas)
- [MAKER] Tuning slides changed pitch by only about a quarter-tone and are rarely made now. Plungers mostly affect the high notes. — [Campin](http://www.campin.me.uk/Music/Ocarina/); [Pure Ocarinas](https://pureocarinas.com/ocarina-tutorial/playing-ocarinas-in-warm-or-cold-environments)
- [MAKER] If there is no whistle, clear the airway and check the sharpness of the labium bevel. — [Ceramic Arts Network](https://ceramicartsnetwork.org/daily/article/Making-Music-with-Clay-How-to-Make-a-Ceramic-Ocarina)

### Inferences
- **[INFERÊNCIA] Fixes by symptom.**
  - A note too sharp after firing can't be corrected by enlarging its hole. Only partial covering, or tape or glue to shrink the hole, will work. So always aim flat.
  - An irregular step in the curve: adjust that single hole. Enlarge it if the step is too big, i.e. the note is too flat at constant pressure.
  - The top screeches before reaching pitch: the curve is too steep or the voicing is too small for the chamber. Don't enlarge the top holes further; check voicing and temperature.

### Gaps
- No quantitative voicing adjustments (windway height in mm vs pressure) were found in accessible sources.
