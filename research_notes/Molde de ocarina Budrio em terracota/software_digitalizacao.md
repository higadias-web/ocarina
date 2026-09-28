# Software and digitization for a Budrio "Do 3" ocarina mould master (CAD, digitization, acoustics, audio, print prep)

Scope note: this research ran on 2026-09-28. I checked version numbers directly against PyPI JSON, GitHub git tags (`git ls-remote`), the Fedora 44 package metadata API (mdapi) and the Flathub API on that date. The URL on each row is the endpoint or page I checked. Several vendor and forum pages (Thingiverse, The Ocarina Network, MIMF, PubMed, The Strad, ScienceDirect) refused automated fetches (403/405/captcha). Claims that rest only on a search-engine snippet of those pages are marked "(snippet only)". The web-search budget ran out before the last few planned queries: CBCT voxel sizes, scanner rental in Brazil, Scaniverse/Polycam on Android, and numeric photogrammetry accuracy. Those items are listed under Gaps.

Reference pitches, calculated rather than sourced (12-TET, A4 = 440 Hz): C5 = 523.25 Hz, F6 = 1396.91 Hz.

---

## 1. CAD for organic ocarina shapes: CadQuery vs build123d vs OpenSCAD vs FreeCAD (lofts, splines, shelling, splitting into halves, registration keys, viewers, STL/STEP export)

### Takeaway
CadQuery and build123d both use the same OpenCASCADE (OCCT) B-rep kernel and are both a good fit for this project. Both provide spline/loft solids, shelling that leaves chosen faces open, plane splitting and STEP/STL export. build123d (0.13.0, 2026-09-21) has the more explicit API for this workflow: `loft`, `offset(openings=…)` and `split(bisect_by=Plane, keep=Keep.TOP/BOTTOM/BOTH)`. CadQuery (2.8.0, 2026-06-21) is the tool already chosen and remains fully adequate. OpenSCAD is mesh/CSG-based and a poor fit for a smooth lofted shell. FreeCAD 1.1.x is the best GUI for inspecting or hand-editing the STEP output.

### Cited Findings
- CadQuery and build123d are both Python libraries wrapping OpenCASCADE, the same B-rep kernel used under FreeCAD — [GrandpaCAD blog (snippet only)](https://grandpacad.com/en/blog/openscad-vs-cadquery-vs-build123d); build123d "is derived from portions of CadQuery, but is extensively refactored and restructured into an independent framework over Open Cascade" — [build123d GitHub](https://github.com/gumyr/build123d).
- build123d swaps CadQuery's fluent method-chaining API for stateful context managers (`with` blocks), so ordinary Python loops, object references and sorting/filtering work naturally — [build123d GitHub (search summary)](https://github.com/gumyr/build123d); a Hacker News discussion carries the same opinion — [HN](https://news.ycombinator.com/item?id=40563489).
- build123d operation signatures, from the docs:
  - `loft(sections…, ruled=False, clean=True)`
  - `sweep(sections, path, multisection=False, is_frenet=False, transition=…)`
  - `offset(objects, amount, openings=Face|list[Face], kind=Kind.ARC, side=…)`, where `openings` gives a hollow shell with open faces
  - `split(objects, bisect_by=Plane|Face|Shell, keep=Keep.TOP|BOTTOM|BOTH)`
  - `section(obj, section_by=Plane…)`, which gives 2-D slices
  - `fillet(...)` and `make_face(edges)`
  - Source: [build123d operations docs](https://build123d.readthedocs.io/en/latest/operations.html)
- The CadQuery API includes `Workplane.loft()`, `Workplane.split()`, `Workplane.shell()`, `Workplane.interpPlate()`, `Workplane.parametricSurface()`, `Workplane.parametricCurve()`, `Sketch.spline()`, `Shape.exportStep()`, `Shape.exportStl()` and `Assembly.export()` — [CadQuery class reference](https://cadquery.readthedocs.io/en/latest/classreference.html).
- Versions and licences on PyPI:
  - cadquery 2.8.0: uploaded 2026-06-21, Apache-2.0, Python ≥ 3.11 — [PyPI](https://pypi.org/pypi/cadquery/json)
  - cadquery-ocp (OCCT bindings) 8.0.1.0.0 — [PyPI](https://pypi.org/pypi/cadquery-ocp/json)
  - build123d 0.13.0: 2026-09-21, Apache-2.0, Python ≥ 3.11 and < 3.15 — [PyPI](https://pypi.org/pypi/build123d/json)
- Viewers:
  - CQ-editor 0.7.0 (2026-04-08) is a PyQt GUI for CadQuery that runs on Linux, Windows and Mac. Python ≥ 3.10 and ≤ 3.14 — [PyPI](https://pypi.org/pypi/cq-editor/json), [CQ-editor README](https://github.com/CadQuery/CQ-editor).
  - OCP CAD Viewer for VS Code 4.1.0 (`ocp_vscode`, 2026-09-16, Apache-2.0) shows both CadQuery and build123d objects. Its "Quickstart build123d" button pip-installs OCP, build123d, ocp_tessellate and ocp_vscode. On VSCodium the extension is not in the marketplace, so the `.vsix` has to be installed by hand — [README](https://github.com/bernhard-42/vscode-ocp-cad-viewer), [PyPI](https://pypi.org/pypi/ocp-vscode/json).
  - "Yet Another CAD Viewer" (`yacv-server` 0.12.1, MIT, 2026-09-21) is a browser-based viewer for OCP models (CadQuery/build123d) — [PyPI](https://pypi.org/pypi/yacv-server/json), [GitHub topic list](https://github.com/topics/build123d).
  - `ocp-action` builds CadQuery/build123d models on GitHub Actions, renders them and publishes a model viewer on GitHub Pages — [ocp-action](https://github.com/yeicor-3d/ocp-action).
- OpenSCAD: Fedora 44 ships `openscad` 2021.01 — [mdapi f44](https://mdapi.fedoraproject.org/f44/pkg/openscad), as does Flathub `org.openscad.OpenSCAD` 2021.01 under GPL-3.0+ — [Flathub API](https://flathub.org/api/v2/appstream/org.openscad.OpenSCAD). The newest git tag is `openscad-2026.01.01-TEST2`, which points to a pending new release; 2021.01 is still the last stable tag — [openscad tags](https://github.com/openscad/openscad/tags).
- FreeCAD: Flathub `org.freecad.FreeCAD` 1.1.3, LGPL-2.1 — [Flathub API](https://flathub.org/api/v2/appstream/org.freecad.FreeCAD). The latest git release tag is 1.1.4, alongside weekly builds up to `weekly-2026.09.23` — [FreeCAD tags](https://github.com/FreeCAD/FreeCAD/tags). A query of Fedora 44 mdapi for `freecad` returned "not found". That may be an mdapi naming quirk, so treat it as unconfirmed rather than a sign the package is absent.

### Inferences
- **Recommendation: keep CadQuery, or move to build123d. Do not use OpenSCAD for the body.** The ocarina body is best built as a loft or sweep through 5–9 elliptical or spline cross-sections along a curved spine. Both OCCT libraries give B-rep solids that shell and split cleanly. OpenSCAD has only `hull()`/`minkowski()`/polyhedron workarounds and no true shelling.
- **Two-half master.** Build the outer solid, then `split` it on the parting plane, which is normally the plane containing the long axis and the widest outline, so the plaster mould releases. Keep `Keep.TOP` and `Keep.BOTTOM` as separate STLs.
- **Registration keys.** For keys that are cast into the plaster, add hemispherical or truncated-cone bosses and sockets to the flange or mould-box surface rather than to the ocarina surface, since the ocarina surface becomes the clay. Model them in CAD with a 0.2–0.3 mm clearance. PrusaSlicer's cut connectors (see §8) are a quick fallback for joining PLA halves but do not replace keys in the plaster.
- **The master is solid for press-moulding.** For press moulds the master is the *outer* surface. The internal chamber and wall thickness only matter for the prototype-playable variant and for predicting fired volume. Keep the shelled version as a separate STL so the fired chamber volume can be computed with `solid.volume`/`Volume()` for the Helmholtz budget.
- **Clay shrinkage changes the pitch strongly.** In a lumped Helmholtz model the pitch scales approximately as 1/(1−s) for linear shrinkage s (volume ∝ L³, hole term ∝ L). By my calculation that is about +89 cents at 5 %, +144 cents at 8 % and +182 cents at 10 % shrinkage. Scale the master by 1/(1−s_total) using a measured shrink bar of the actual terracotta body (drying plus firing).
- **FreeCAD's role.** FreeCAD 1.1 (Flatpak) is useful to open the exported STEP files and check them: measure, section and verify the parting plane.

### Gaps
- I did not benchmark OCCT robustness (loft plus shell failures on tight curvature) for this specific shape. OCCT `shell`/`offset` can fail on high-curvature lofts. Only a prototype script can show whether a thin-wall shell of a Budrio profile works first time.
- I did not verify whether a CadQuery or build123d package exists in Fedora 44 repos; mdapi returned nothing for `python3-cadquery`. pip in a venv or conda appears to be the install path.

---

## 2. Existing open-source / parametric ocarina models and generators (Printables, Thingiverse, GitHub); encoded rules; licences

### Takeaway
There are many printable *fixed* STL ocarinas, mostly under non-commercial Creative Commons licences. I found **no open-source parametric ocarina generator** (CadQuery, build123d, OpenSCAD or FreeCAD) on GitHub. GitHub searches for "ocarina generator"/"parametric" return mainly Zelda "Ocarina of Time" randomizers. The closest reference design to this project is E.C.3D's "10 Hole Ocarina V0N3 C5–F6" (CC-BY-NC), which has the same range as the Mignani Do 3. Its notes are some of the few published print-geometry rules (airway height, wall ordering, print orientation).

### Cited Findings
- A GitHub search for "parametric ocarina generator" returned only Ocarina-of-Time randomizers, a tab editor (`dzoba/ocarina-tabs`) and a web synth (`jasonhibbs/ocarina`) — [search results incl. github.com/dzoba/ocarina-tabs](https://github.com/dzoba/ocarina-tabs), [jasonhibbs/ocarina](https://github.com/jasonhibbs/ocarina). Searches pairing ocarina with CadQuery, build123d, OpenSCAD or FreeCAD found no ocarina project — [awesome-cadquery](https://github.com/CadQuery/awesome-cadquery), [awesome-build123d](https://github.com/phillipthelen/awesome-build123d).
- Printables models, from its GraphQL API on 2026-09-28 (name, author, licence, downloads):
  - "12-hole playable Ocarina", Mikolas Zuza, **CC-BY-NC-SA**, 77,210 downloads. It is a collection of remixes: the original by Nimaid, remixed "to play better" by RobSoundtrack; licence kept from Nimaid's CC-BY-NC-SA. The author says printing pointy-end-down may be better — [Printables 65399](https://www.printables.com/model/65399-12-hole-playable-ocarina); the Thingiverse original remix is [thing:2755765](https://www.thingiverse.com/thing:2755765) (page not fetchable).
  - **"10 Hole Ocarina V0N3 C5 - F6"**, E.C.3D, **CC-BY-NC**, published 2025-05-09.
    - Tuned C5–F6 and printed standing on the mouthpiece without supports.
    - "The internal design helps to reduce airy high notes… inspired by an idea from Robert Hickman – Ocarina volume bypass."
    - Settings: 0.4 mm nozzle, 0.8 mm walls, "Wall ordering: Outside To Inside"; "Bigger or smaller nozzles may change the tune"; "The soundhole and the airway have to be printed clean."
    - The author now publishes new ocarinas only on MakerWorld.
    - Source: [Printables 412936](https://www.printables.com/model/412936)
  - "Ocarina of Time – 12 hole Alto C", E.C.3D, CC-BY-NC, tuned A4–F6. Changelog v3: "Reduced Airway height, 1mm instead of 1,2mm… Less airy, Better breath curve." Also: "For A4 the required air pressure is low, more opened holes need more air pressure" — [Printables 474058](https://www.printables.com/model/474058).
  - "Single Print Ocarina", Julius3E8, CC-BY-SA, 311–846 Hz in its latest version; after many iterations the author says "no gluing parts together or tuning – just print and play" — [Printables 249011](https://www.printables.com/model/249011).
  - "Soprano Ocarina", Jona32u4, **CC0**, a copy of [Thingiverse 2846575](https://www.thingiverse.com/thing:2846575) — [Printables 211559](https://www.printables.com/model/211559).
  - "Double Chamber Ocarina", sthompson, CC-BY-NC-SA — [Printables 70705](https://www.printables.com/model/70705).
  - Others: "Ocarina SC" (E.C.3D, CC-BY-NC-ND), "Pendant ocarina – 4 hole" (madgrant, CC-BY), "Easy Print 9-Hole Inline" (Julius3E8, CC-BY-NC) — [Printables API search "ocarina"](https://api.printables.com/graphql/).
- Pure Ocarinas (Robert Hickman) had an SLS (Shapeways) print made from his Pure Alto C, reduced to 10 holes.
  - The rough layered windway caused "turbulence and left the ocarina with a noisy, edgy and harsh tone". Hand-polishing improved it.
  - Holes had to be enlarged by hand to tune it, and it "pales in comparison to the ceramic ocarina it was based on".
  - It cost about £50 to produce.
  - No design files are published.
  - Source: [pureocarinas.com](https://pureocarinas.com/playable-3d-printed-ocarina)
- Robert Hickman sells a paid e-book, "The Art of Ocarina Making" (£17.99 PDF). It covers the windway, labium and sound hole, tuning 4/10/11/12-hole ocarinas, ergonomics, "choosing your ocarina's breath curve", plaster mould-making and finishing — [ocarinamaking.com](https://ocarinamaking.com).
- A commercial STL is also sold: "Ocarina in C5 by BRAS" — [instrumentsbybras.com](https://instrumentsbybras.com/products/ocarina-in-c-by-bras-digital-file-for-3d-printing-stl) (not inspected).
- Mould-specific material:
  - An Ocarina Network thread says slip casting in two pieces and joining them "helps achieve consistent chamber size and pitch" — [The Ocarina Network (snippet only)](https://theocarinanetwork.com/molds-and-ocarina-making-t6656.html).
  - A fully 3D-printed system for a 3-part slip-cast plaster mould — [Old Forge Creations](https://www.oldforgecreations.co.uk/blog/3-part-mould-for-slipcasting-from-fully-3d-printed-system).
  - Forum threads on PLA masters for plaster moulds — [Ceramic Arts Daily](https://community.ceramicartsdaily.org/topic/37386-3d-printing-for-plaster-molds/).

### Inferences
- No existing model can be adopted directly. Nearly all the good ones are NC or NC-SA, which is acceptable for a hobby copy, but none is parametric and none is a Budrio transverse shape. The E.C.3D C5–F6 design is the best *acoustic sanity reference*: the same range, and a printable airway of 1.0–1.2 mm height. Its airway/labium numbers are worth comparing with rubbings and caliper readings from the Mignani.
- Several independent makers say FDM windways are the weak point (layer lines, blobs, wall ordering). For this project the windway is formed in clay or with the separate windway blade, not printed, so the PLA master's surface quality matters mainly for mould release.

### Gaps
- Thingiverse pages could not be fetched, so the licences and notes of the Nimaid and RobSoundtrack originals are unconfirmed beyond Mikolas Zuza's statement.
- MakerWorld, where E.C.3D now publishes, was not searched.
- I found no published 3D-printed *press-mould master* for an ocarina specifically, only generic slip-cast mould workflows.

---

## 3. Ocarina hole-size / Helmholtz calculators: what exists, formulas, reliability

### Takeaway
Free ocarina-specific calculators are scarce and unvalidated: one AGPL Visual Basic program from 2019, plus forum formulas. They all rest on the Helmholtz relation f = (c/2π)·√(A/(V·L′)), with the empirical rule that pitch depends on open-hole area (or, in practice, the sum of hole diameters) and not on hole position. Experienced makers say the plain formula does not predict an ocarina exactly (the voicing and window shift the pitch), so any calculator should be treated as a starting point that must be calibrated against the reference instrument's recorded pitches.

### Cited Findings
- Phauxelate/ocarina-calculator is written in Visual Basic under AGPL-3.0, last updated 2019-08-30.
  - Inputs: fipple (window) diameter, the all-closed base frequency and target note frequencies. Outputs: hole diameters in inches, based on "the total area of open holes".
  - The exact formula is not documented in the README, and a wrong entry means restarting from scratch because the holes are linked.
  - The author says it is "mathematically and visually proven" but asks others to build a physical prototype, so it has **no physical validation**.
  - Source: [GitHub](https://github.com/Phauxelate/ocarina-calculator)
- Forum formula: "V = 1/(((F/2148.14)^2)/D)", with F in Hz and D the diameter; "the first fingerhole … approximately 2 mm … one an octave above … 8–9 mm or more"; "the position of fingerholes is fairly unimportant – it is the cross-section of each hole that is crucial" — [The Ocarina Network tutorial (snippet only)](https://theocarinanetwork.com/tutorial-making-an-ocarina-in-a-predetermined-key-t10093.html), related threads [hole size](https://theocarinanetwork.com/ocarina-hole-size-t1085.html), [window size](https://theocarinanetwork.com/how-to-calculate-the-perfect-window-size-t22621.html), [hole-size differences between brands](https://theocarinanetwork.com/hole-size-differences-between-different-ocarina-br-t20409.html).
- Makers note that the standard Helmholtz formula "doesn't give the correct answer for ocarinas because the ocarina is an active resonator with air blown over the fipple opening and has multiple finger holes" — [The Ocarina Network "helmholtz calculation" (snippet only)](https://theocarinanetwork.com/helmholtz-calculation-t20435.html).
- Wikipedia: ocarina tone "is dependent on the ratio of the total surface area of opened holes to the total cubic volume"; "the placement of the holes on an ocarina is largely irrelevant – their size is the most important factor", although holes near the voicing should be avoided. The 10-hole Budrio design is credited to Giuseppe Donati (1853) — [Wikipedia: Ocarina](https://en.wikipedia.org/wiki/Ocarina).
- There are generic Helmholtz resonator calculators, for example FIRGELLI's, which solves for f, V, neck area, length or diameter — [FIRGELLI](https://www.firgelliauto.com/blogs/engineering-calculators/helmholtz-resonator-calculator). A Physics Forums thread discusses the multiple-neck extension — [Physics Forums](https://www.physicsforums.com/threads/helmholtz-resonator-with-multiple-necks-formula.948401/).
- A US patent on ocarina design exists — [US7799980B1](https://patents.google.com/patent/US7799980) (not read in detail).

### Inferences
- **What the 2148.14 constant means (my own unit analysis).** From f² = c²·D/(16π·k·V), with a round hole and an effective neck length L′ = k·D, you get V = D/(f/K)² where K = c/√(16πk). K = 2148.14 is consistent with **inch units** (c ≈ 13,504 in/s) and k ≈ 0.79, meaning an effective neck of about 0.79·D. That is a plausible thin-wall end correction. In mm units the same constant gives an absurd k (~507). So the formula is probably V in in³ and D in inches. Verify this before using it.
- **For thin walls, pitch follows the sum of hole diameters.** With A ∝ D² and L′ ∝ D, each hole adds ∝ D to the resonance term, so f ∝ √(ΣD_i / V). This matches the makers' focus on hole size over position. With a wall of about 4–6 mm terracotta, the wall thickness adds to L′ and the dependence shifts back toward area/length.
- **Practical recommendation:** write the calculator inside the CadQuery project as a lumped model f = (c/2π)·√(Σ A_i/L′_i / V), with L′_i = t + α·D_i. Fit V_eff and α (and a window term) to the reference ocarina's measured note frequencies (§7) and its caliper/rubbing hole diameters. That makes it a *calibrated* model rather than a first-principles one. The ~2 mm smallest hole and 8–9 mm largest hole quoted on the forum are a quick plausibility check.

### Gaps
- I could not access The Ocarina Network pages (403) to confirm the full derivation, the units or the author of the 2148.14 formula.
- I found no peer-reviewed validation of any ocarina hole calculator against measured instruments.
- I did not find a spreadsheet calculator with a public URL.

---

## 4. Non-destructive digitization of the reference ocarina (photogrammetry, structured light, CT, DICOM→STL; access and costs in Brazil)

### Takeaway
Photogrammetry (Meshroom, COLMAP/OpenMVS, or RealityScan Mobile on Android) gives the **outer** shape. Scaling it with a printed scale bar or calipers is essential because photogrammetry has no inherent scale and can drift. CT is the **only** non-destructive way to capture the internal chamber, windway and labium geometry. Museums routinely CT-scan wind instruments for exactly this reason, and a Chinese ocarina has been CT-scanned on a hospital CT for 3D-printed replication. In Brazil, industrial micro-CT is available at CTI Renato Archer, MZUSP/USP, UFPE and other university multi-user labs, and commercially from MiDS (SP); prices are on request. The DICOM or TIFF stack can be turned into STL with InVesalius (Brazilian, GPL-2.0, Flatpak) or 3D Slicer. Be careful with "vanishing" matting sprays on an antique varnished instrument: a 2024 conservation study found that AESUB sprays leave residues.

### Cited Findings
**Photogrammetry**
- Meshroom is licensed MPL-2.0 — [Meshroom GitHub](https://github.com/alicevision/Meshroom). The latest tag is v2025.1.8 — [tags](https://github.com/alicevision/Meshroom/tags). AliceVision needs CUDA ≥ 11.0 "for feature extraction and depth map computation" (build option `ALICEVISION_USE_CUDA`, default ON) — [AliceVision INSTALL.md](https://github.com/alicevision/AliceVision/blob/develop/INSTALL.md). A Gaussian-splatting plugin (MrGSplat) is also available — [Meshroom README](https://github.com/alicevision/Meshroom).
- COLMAP 4.2.0 is the latest tag, under the "new BSD license". CUDA wheels are on PyPI as `pycolmap-cuda12`, and AMD GPUs are supported via HIP/ROCm when building from source — [COLMAP README](https://github.com/colmap/colmap), [tags](https://github.com/colmap/colmap/tags). OpenMVS v2.4.0 is the latest tag — [tags](https://github.com/cdcseacave/openMVS/tags). Neither is in Fedora 44 per mdapi — [mdapi colmap](https://mdapi.fedoraproject.org/f44/pkg/colmap).
- In a comparative study, COLMAP gave the most micro-surface variation (fine detail plus noise), Meshroom kept detail while suppressing noise, and Metashape (commercial) gave the highest quality — [arXiv 2605.29452 (snippet only)](https://arxiv.org/pdf/2605.29452).
- One study found that "photogrammetry suffers from geometric noise and scale drift (relative error > 10 %)" while structured-light scanning is "more stable and metrically accurate". That study used industrial-scale objects — [PMC12693997 (snippet only)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12693997/). There is a review of photogrammetry for small and micro-scale objects with sub-millimetre features — [Springer (snippet only)](https://link.springer.com/chapter/10.1007/978-3-319-89563-5_4) — and a metrological comparison across small and meso scales — [ScienceDirect S0141635924002666 (not fetchable)](https://www.sciencedirect.com/science/article/pii/S0141635924002666).
- RealityScan Mobile (Epic Games) is free on Android 7.0+. Version 1.8 (Nov 2025) added capture presets, AR guidance and automatic background removal. Models are processed online and can be downloaded or exported to Sketchfab — [CG Channel](https://www.cgchannel.com/2025/11/epic-games-releases-realityscan-mobile-1-8/), [realityscan.com](https://www.realityscan.com/en-US/news/realityscan-mobile-is-now-available-for-android-devices), [Google Play](https://play.google.com/store/apps/details?id=com.epicgames.realityscan&hl=en). The desktop product was renamed RealityScan 2.0 in June 2025 — [CG Channel](https://www.cgchannel.com/2025/06/epic-games-releases-realityscan-2-0-and-realityscan-mobile-1-7/).

**Matting sprays on a heritage object**
- Cyclododecane sublimates at room temperature and is used as a temporary opacifier for scanning archaeological glass — [ScienceDirect (snippet only)](https://www.sciencedirect.com/science/article/abs/pii/S1296207415001132). Conservators measured exposures of 0.75–15.5 mg/m³ indoors and recommend fume hoods and respirators — [Int Arch Occup Environ Health (snippet only)](https://link.springer.com/article/10.1007/s00420-010-0596-1). Commercial cyclododecane spray: ATTBLIME AB24 — [ATTBLIME](https://us-attblime.com/product/attblime-ab24-cyclododecane-spray-sublimating/).
- Nielsen, Jæger and Gregersen (2024) found that AESUB Blue, Transparent and Yellow "all … left residue", which "accumulates with continued application" and persisted for months. The AESUB Yellow residue may contain carboxylic acid, which can degrade metals, glass and organics — [Zenodo 13368686](https://zenodo.org/records/13368686).

**CT scanning of musical instruments**
- The Germanisches Nationalmuseum's MUSICES project (2014–2017, DFG-funded) produced recommendations for 3D-CT of musical instruments — [ViMM (snippet only)](https://www.vi-mm.eu/project/3-dimensional-computed-tomography-scanning-of-musical-instruments/). The Vienna KHM has CT-scanned historic instruments since 2003 — [The Strad (snippet only)](https://www.thestrad.com/lutherie/ct-scanning-for-luthiers-an-essential-guide/7448.article).
- Pitt Rivers / Bate Collection, "Plastic Fantastic? Replicating Historical Musical Instruments": an 18th-century ivory recorder was scanned on a Nikon XT H225 micro-CT at Cranfield. CT "is the only method that can provide the information needed to print an accurate 3D version of a mouth-blown musical instrument". The scan showed beetle damage that altered the windway — [Pitt Rivers Museum](https://www.prm.ox.ac.uk/plastic-fantastic-ct-scan).
- Brown University's Haffenreffer Museum replicated a Native American block flute, **a Chinese ocarina** and whistles.
  - The CT scan was done by an imaging specialist at Rhode Island Hospital, i.e. a clinical CT.
  - The mesh was converted to a solid in Fusion 360, missing parts were sculpted, and the model was split into sections and printed on a Formlabs Form 3 (SLA).
  - Lesson: "the importance of high image resolution in the scanning and design phases".
  - Source: [Autodesk Learn Lab](https://blogs.autodesk.com/learn-lab/2023/01/18/scholars-replicate-indigenous-flutes-with-3d-printing/)
- Through CT images, researchers can observe defects, cracks, previous restorations and tool marks in historical woodwinds — [PubMed 36286354 (snippet only)](https://pubmed.ncbi.nlm.nih.gov/36286354/).
- A 3D CT study of Boston MFA instruments — [MFA Boston](https://www.mfa.org/event/ct-scanning-a-look-inside-the-music).

**CT access in Brazil**
- **CTI Renato Archer (Campinas, SP)** offers "Solicitar serviço de análise por microtomografia de raios X", a non-destructive imaging service producing 3D models with resolution "up to 5 µm". It is open to researchers, companies, startups and inventors. Cost is "sob consulta", with a commercial proposal per request, via servicos@cti.gov.br — [gov.br](https://www.gov.br/pt-br/servicos/solicitar-servico-de-analise-por-microtomografia-de-raios-x-cti-renato-archer).
- **MZUSP (USP, São Paulo)** has a GE Phoenix v|tome|x m that takes samples up to 50 × 50 cm and 50 kg at up to 300 kV. Output is 16-bit TIFF, reconstructed with datos|x 2 and VG Studio Max. External academic and private users are accepted, with 15 days' notice and a user-supplied drive of 10–50 GB per sample. Billing is per hour per specimen in whole hours; rates are not published. Contact mz@usp.br — [MZUSP](https://mz.usp.br/pt/pesquisa/laboratorios-multiusuarios/microtomografia-ct-scan/).
- **UFPE LTC-RX (Recife)** has a Nikon XT H 225 ST with a 3 µm focal spot — [UFPE](https://www.ufpe.br/en/propesqi/lamps/ltcrx).
- **UEL (Londrina)** multi-user central offers micro-CT by request form — [UEL CMLP](https://cmlp.uel.br/equipamentos/). **UFF** has a micro-CT multi-user platform — [UFF](http://microct.sites.uff.br/historico/).
- **MiDS Metrology (Santo André, SP)** is a commercial industrial CT service for plastics, additive manufacturing and other materials. Quotes are by phone, WhatsApp or e-mail (mids@mids.com.br); no specifications or prices are published — [MiDS](https://www.mids.com.br/servico-tomografia-industrial).
- **Dental CBCT in Goiânia**: dental tomography costs about R$250–600 for patients, per the DentMap aggregator — [DentMap (snippet only)](https://dentmap.com.br/radiografia-odontologica/goiania). Dental CBCT gives 3D volumes; guidance is to use the "smallest possible FOV, the smallest voxel size" — [Wikipedia CBCT](https://en.wikipedia.org/wiki/Cone_beam_computed_tomography).

**DICOM → STL**
- InVesalius reconstructs 3D models from CT/MRI DICOM. It offers threshold and watershed segmentation and exports binary/ASCII STL, PLY, OBJ, VRML and Inventor. It runs on Linux, Windows and macOS under GPL-2.0, and originated at CTI Renato Archer — [GitHub](https://github.com/invesalius/invesalius3). Flathub has `br.gov.cti.invesalius` 3.1.999982, GPL-2.0-only — [Flathub API](https://flathub.org/api/v2/appstream/br.gov.cti.invesalius); the latest git tag is v3.1.99998 — [tags](https://github.com/invesalius/invesalius3/tags).
- In 3D Slicer, use Segment Editor → "Export to files" → STL, or Data module → "Export visible segments to models". STL uses the LPS coordinate system — [Slicer docs: Segmentations](https://slicer.readthedocs.io/en/latest/user_guide/modules/segmentations.html), [Slicer forum](https://discourse.slicer.org/t/conversion-of-dicom-to-stl-using-3d-slicer/1810). The latest tag is v5.12.4 — [tags](https://github.com/Slicer/Slicer/tags). It is not on Flathub under `org.slicer.Slicer`, so use the official tarball from slicer.org (inference).

### Inferences
- **Recommended plan for the outer surface:**
  1. Use a turntable with diffuse light and 60–120 photos at two or three elevations.
  2. Put a printed checkerboard or ArUco scale bar in the scene and scale the model with a caliper-measured length (overall length 175 mm, width 85 mm).
  3. Process in COLMAP plus OpenMVS, or in Meshroom if an NVIDIA GPU is available. The alternative is RealityScan Mobile, which processes online, so check its terms.
  4. For a 17 cm object with a good camera, expect accuracy of a few tenths of a mm (unverified, no numeric source found), which is enough for the outer shape of a press-mould master.
  5. Check the scaled model against 3–5 caliper measurements.
- **Glossy varnish.** Do not spray the antique. Use cross-polarised lighting (a polariser on the flash and the lens) or a light tent to kill specular highlights. If opacifying is unavoidable, only pure cyclododecane is defensible, used outdoors and with a respirator. Even then, a conservator should be asked first about the varnish.
- **CT is the high-value option for the interior.** It captures chamber volume, wall thickness, window, windway and labium geometry at once, and the MUSICES, Bate Collection and Brown precedents cover exactly this use case. Options in rough order of cost and accessibility (inference):
  - A dental radiology clinic in Goiânia with CBCT, asked to scan an "objeto" and hand over DICOM. The ceramic walls should be easily penetrable, but the ~17.5 cm length may exceed small dental fields of view, so ask about the large FOV or two stitched scans.
  - A hospital or veterinary CT, which gives about 0.5 mm voxels (typical for clinical CT; not sourced here).
  - University or industrial micro-CT (CTI, MZUSP, UFPE, MiDS), which gives far finer voxels, requires shipping the instrument, and costs more.
- **Pipeline:** DICOM → InVesalius (threshold the ceramic) → STL → MeshLab/Blender cleanup → import into CadQuery as a reference, for example by slicing sections to fit the parametric lofts or by computing the internal cavity volume with trimesh.

### Gaps
- **Rental of structured-light scanners** (Revopoint, Creality, Einscan) in Brazil or Goiânia: not researched because the search budget ran out, so no prices or rental sources.
- **Scaniverse and Polycam** on Android: not verified this session.
- **Typical CBCT and medical CT voxel sizes**, and whether Goiânia dental clinics will scan objects: no source retrieved.
- **Numeric photogrammetry accuracy for a ~17 cm object with open-source tools:** no source with numbers retrieved.
- **UFG (Goiânia)** micro-CT availability: not found; worth asking UFG physics and geology departments directly.
- **No CT scan of a Budrio ocarina specifically** was found.

---

## 5. Measuring internal volume non-destructively (acoustic or gas methods)

### Takeaway
Measuring volume by acoustic Helmholtz resonance is an established technique. Webster and Davies (2010) reached better than ±0.1 % of resonator volume, and newer acoustic volumeters exist. Applied to an ocarina it needs calibration, because the effective neck (window plus holes) is unknown. CT remains the only direct method. Filling with water, sand or seed is fast but risky for an antique porous terracotta and not recommended.

### Cited Findings
- Webster and Davies (2010, *Sensors*):
  - Setup: a single-port resonator of 1–3 L, driven by a loudspeaker and measured with two microphones.
  - Resonance formula: f_res = (c/2π)·√(S_p/(V_c·l_p′)). Object volume: V_P = V_c − S_p·l_p′/(2π·f_res/c)².
  - Accuracy: water volumes within 3 mL (better than ±0.1 % of resonator volume); solids within good agreement up to about 100–400 mL.
  - Limitations: sample-dependent calibration curves were needed, and accuracy degraded when the sample was close to the port.
  - Source: [PMC3231073](https://pmc.ncbi.nlm.nih.gov/articles/PMC3231073/)
- A 2026 "sound-pressure quality-factor" model estimates volume in real time from cavity pressure amplitude, reporting U(k=2) < 0.1 % of cavity capacity in static tests — [Acoustics Australia 2026 (snippet only)](https://link.springer.com/article/10.1007/s40857-026-00385-3).
- An acoustic volumeter for objects of any shape — [PMC7038409 (snippet only)](https://pmc.ncbi.nlm.nih.gov/articles/PMC7038409/). Helmholtz resonators have also been used to estimate fish volume underwater — [ScienceDirect (snippet only)](https://www.sciencedirect.com/science/article/abs/pii/S1881836617302161).

### Inferences
- **Practical acoustic method for this project (calibration by comparison):**
  1. Print 3–4 PLA test vessels with the same window and voicing geometry as the planned design and known chamber volumes, for example 60, 80 and 100 mL.
  2. Record their all-closed pitch at a fixed breath pressure.
  3. Fit f ∝ V^(−1/2), which also gives the effective window term.
  4. Read the reference ocarina's effective volume off that curve from its recorded lowest note.
- **Alternative measurement:** seal the window and all holes except one hole of known diameter, excite it by tapping or with a sine sweep from a small speaker, and read the resonance with a phone mic in Sonic Visualiser.
- **Why it only gives an effective volume:** both methods give an *effective* volume that includes end-correction uncertainty, which is fine because it is exactly the quantity the lumped model needs.
- **Gas-displacement pycnometry and water or seed filling** would give true geometric volume but mean filling or pressurising a porous antique, so they are not recommended.

### Gaps
- I found no published example of acoustic volume measurement applied to an ocarina or any vessel flute.
- No study quantifies how much the fipple and window (an active, blown resonator) shift the Helmholtz frequency compared with passive excitation.

---

## 6. Acoustic simulation: is FEM (Elmer, openCFS, FEniCS, sfepy) useful, or is a lumped model enough?

### Takeaway
For design and tuning, a **calibrated lumped Helmholtz model is enough**, and it is what makers use. Linear-acoustic FEM (Helmholtz equation, eigenfrequency, with PML radiation) can refine hole/window interaction and wall-thickness end corrections for passive resonances. The sounding mechanism (edge tone coupled with the Helmholtz cavity, and pitch drift with blowing speed) needs compressible CFD/LES, as the one ocarina simulation paper found shows. That is research-grade work and not practical for a hobby project.

### Cited Findings
- Kobayashi, Takami, Miyamoto, Takahashi, Nishida and Aoyagi (2009) ran compressible LES in 2D and 3D of an ocarina. They studied the oscillation frequency at different blowing velocities and treated the ocarina as an edge-tone mechanism coupled with a Helmholtz resonator — [arXiv 0911.3567](https://arxiv.org/abs/0911.3567).
- openCFS is an open-source FEM framework, launched in 2020. It supports the Helmholtz equation for time-harmonic acoustics, eigenfrequency analysis, PML absorbing boundaries and aeroacoustic wave operators, and has a Python API (pyCFS). The paper was revised in January 2025 — [arXiv 2207.04443](https://arxiv.org/abs/2207.04443).
- Versions:
  - Elmer FEM: latest tag release-26.2.1 — [tags](https://github.com/ElmerCSC/elmerfem/tags); no Fedora 44 package per mdapi — [mdapi](https://mdapi.fedoraproject.org/f44/pkg/elmerfem).
  - sfepy 2026.2 (2026-06-26, BSD) — [PyPI](https://pypi.org/pypi/sfepy/json).
  - Gmsh 4.15.0 is in Fedora 44 — [mdapi](https://mdapi.fedoraproject.org/f44/pkg/gmsh).
- COMSOL (commercial) has an Acoustics Module for pressure acoustics — [COMSOL](https://www.comsol.com/acoustics-module); not free.

### Inferences
- **Where FEM helps:**
  - Checking how the 10 holes and the window interact, including the local chamber shape near each hole.
  - Estimating how the terracotta wall thickness (the hole "neck" length) changes each hole's effective length.
  - Confirming that the second chamber mode sits well above F6, so it does not cause "airy high notes" or octave instability. This is what E.C.3D's "volume bypass" idea addresses (§2).
- **Suggested pipeline:** export the *cavity* STEP from CadQuery, mesh it with Gmsh, run an Elmer or sfepy (or FEniCSx) Helmholtz eigenvalue problem with a radiation or PML region outside each hole, and compare with the lumped model. This is a weekend-scale experiment for someone comfortable with FEM, not a requirement.
- **FEM cannot replace measurement.** Passive FEM cannot predict the breath-dependent pitch (the "blowing curve"). That has to come from audio measurement (§7) of prototypes.

### Gaps
- I found no published ocarina FEM (eigenfrequency) study and no openly shared ocarina CFD case files.
- The Elmer, FEniCSx and sfepy acoustic modules were not individually verified this session (docs not fetched).

---

## 7. Audio pitch analysis: which tool gives the most accurate cents; workflow to segment a chromatic scale and compute per-note median and cents; blowing curve

### Takeaway
For offline analysis of sustained, clean ocarina notes (523–1397 Hz), **pYIN and CREPE/torchcrepe are the right estimators**. On the published benchmark, CREPE had the highest share of frames within 10 cents of the true pitch (0.909 vs pYIN's 0.826 on realistic resynthesised stems), but this is frame-level accuracy on synthetic data, not ocarinas. **Pitfall:** `librosa.pyin` returns frequencies *quantised to its pitch-bin grid*, and the default `resolution=0.1` gives 10-cent steps. Set `resolution=0.01` (1-cent bins) or refine with `librosa.yin` before taking per-note medians.

Suggested tool roles:
- **Sonic Visualiser 5.2.1 with the pYIN Vamp plugin:** visual inspection.
- **Tony:** semi-automatic note segmentation with CSV export.
- **Lingot:** live checks while tuning.
- **A Python script** (librosa 1.0 and/or torchcrepe): the per-note statistics table and the blowing curve.

### Cited Findings
- **CREPE**, Kim, Salamon, Li and Bello, ICASSP 2018 — [arXiv 1802.06182](https://arxiv.org/abs/1802.06182). Raw pitch accuracy (share of frames within the threshold of the true pitch):

  | Dataset | Threshold | CREPE | pYIN | SWIPE |
  |---|---|---|---|---|
  | RWC-synth | 50 cents | 0.999 | 0.990 | 0.963 |
  | RWC-synth | 10 cents | 0.995 | 0.908 | 0.833 |
  | MDB-stem-synth | 50 cents | 0.967 | 0.919 | 0.925 |
  | MDB-stem-synth | 25 cents | 0.953 | 0.890 | 0.897 |
  | MDB-stem-synth | 10 cents | 0.909 | 0.826 | 0.816 |

  - Model: input 1024 samples at 16 kHz; 360 output bins at 20-cent spacing covering C1–B7 (32.70–1975.5 Hz); the final estimate is a weighted average across bins (sub-bin).
  - pYIN is "almost unaffected" by brown noise.
  - Source: [CREPE paper PDF](https://arxiv.org/pdf/1802.06182)
- **CREPE and torchcrepe packages:**
  - `crepe` 0.0.16 (2024-08, MIT) — [PyPI](https://pypi.org/pypi/crepe/json).
  - `torchcrepe` 0.0.24 (2025-05, MIT) — [PyPI](https://pypi.org/pypi/torchcrepe/json).
  - torchcrepe offers Viterbi (default), weighted-argmax (as in the original CREPE) and argmax decoders, "tiny" and "full" models, and a periodicity (confidence) output with median filtering and thresholding (e.g. `threshold.At(.21)`).
  - Its upper frequency limit is 2006 Hz, and the README example uses a 5 ms hop — [torchcrepe README on PyPI](https://pypi.org/project/torchcrepe/).
- **librosa:**
  - librosa 1.0.0 (2026-08-11, ISC, Python ≥ 3.12) — [PyPI](https://pypi.org/pypi/librosa/json).
  - Signature: `librosa.pyin(y, *, fmin, fmax, sr=22050, frame_length=2048, hop_length=None, n_thresholds=100, beta_parameters=(2,18), boltzmann_parameter=2, resolution=0.1, max_transition_rate=35.92, switch_prob=0.01, no_trough_prob=0.01, fill_na=nan, center=True, …)`. The docstring says "resolution: Resolution of the pitch bins. 0.01 corresponds to cents." It returns `(f0, voiced_flag, voiced_prob)`. The reference is Mauch and Dixon, ICASSP 2014 — [librosa source, core/pitch.py](https://github.com/librosa/librosa/blob/main/librosa/core/pitch.py).
  - In the same source, the final output is `freqs = fmin * 2**(arange(n_pitch_bins)/(12*n_bins_per_semitone)); f0 = freqs[states % n_pitch_bins]`. The returned f0 is therefore snapped to a grid anchored at `fmin`, even though parabolic interpolation is applied to YIN candidates internally — [same source](https://github.com/librosa/librosa/blob/main/librosa/core/pitch.py).
- **pYIN Vamp plugin (Matthias Mauch):** "a modification of the … YIN algorithm for F0 estimation in monophonic audio". It is included in the Vamp Plugin Pack, and the same page lists a "Local Candidate PYIN" variant — [vamp-plugins.org](https://www.vamp-plugins.org/download.html). Fedora 44 ships `vamp-plugin-sdk` 2.10 — [mdapi](https://mdapi.fedoraproject.org/f44/pkg/vamp-plugin-sdk).
- **Sonic Visualiser 5.2.1:** GPL v2+, available as AppImage and .deb, with "no plugins … included", so plugins are downloaded separately — [sonicvisualiser.org](https://www.sonicvisualiser.org/download.html). Fedora 44 packages it as `sonic-visualiser` 5.2.1 — [mdapi](https://mdapi.fedoraproject.org/f44/pkg/sonic-visualiser).
- **Tony:** free and open-source for Windows, Linux and Mac, "designed for high quality pitch and note transcription for scientific applications". It is primarily for solo vocal recordings and exports pitch and note tracks as CSV — [sonicvisualiser.org/tony](https://www.sonicvisualiser.org/tony/).
  - Tony uses pYIN-based pitch and note tracking. It resamples to 44.1 kHz and uses 2048-sample frames (about 46 ms) with a 256-sample hop (about 6 ms) — [Tony paper, TENOR 2015 (snippet only)](http://tenor2015.tenor-conference.org/papers/04-Mauch-Tony.pdf), [ResearchGate](https://www.researchgate.net/publication/277664840_Computer-aided_Melody_Note_Transcription_Using_the_Tony_Software_Accuracy_and_Efficiency).
- **Lingot 1.1.1:** GPL-2, "accurate … perfect for real-time microtonal tuning". It supports Scala `.scl` temperaments and runs on JACK, ALSA, OSS or PulseAudio — [Lingot README](https://github.com/ibancg/lingot). Packaged in Fedora 44 as `lingot` 1.1.1 — [mdapi](https://mdapi.fedoraproject.org/f44/pkg/lingot) — and on Flathub as `org.nongnu.lingot` 1.1.1 — [Flathub API](https://flathub.org/api/v2/appstream/org.nongnu.lingot).
- **Praat:** 7.0.02, on Flathub `org.praat.Praat` under GPL-3.0+ — [Flathub API](https://flathub.org/api/v2/appstream/org.praat.Praat), [tags](https://github.com/praat/praat/tags). Praat has a "Sound: To Pitch (filtered autocorrelation)" command — [Praat manual](https://www.fon.hum.uva.nl/praat/manual/Sound__To_Pitch__filtered_ac____.html). The Python binding `praat-parselmouth` is at 0.4.7 (2025-11-27, GPLv3) — [PyPI](https://pypi.org/pypi/praat-parselmouth/json).
- **aubio:** the last PyPI release is 0.4.9 from 2019-02-08 (GPL-3) — [PyPI](https://pypi.org/pypi/aubio/json). Fedora 44 ships aubio 0.4.9 — [mdapi](https://mdapi.fedoraproject.org/f44/pkg/aubio).
- **Audacity:** 3.7.7 in Fedora 44 — [mdapi](https://mdapi.fedoraproject.org/f44/pkg/audacity) — and 3.7.8 on Flathub, GPL-3.0 — [Flathub API](https://flathub.org/api/v2/appstream/org.audacityteam.Audacity).
- **Android recorder:** Dimowner Audio Recorder is on F-Droid and records WAV (or other formats), with adjustable sample rate and bitrate and a mono/stereo toggle. It is Apache-2.0 — [README](https://github.com/Dimowner/AudioRecorder). The latest tag is v2.4.0 — [tags](https://github.com/Dimowner/AudioRecorder/tags).
- **Breath dependence of ocarina pitch:** E.C.3D notes that more open holes need more air pressure to hit the note, and that airway height changes the "breath curve" — [Printables 474058](https://www.printables.com/model/474058). Kobayashi et al. simulated oscillation frequency against blowing velocity — [arXiv 0911.3567](https://arxiv.org/abs/0911.3567).

### Inferences
- **Evaluation of the chosen tools:**
  - **Lingot** is good for live tuning, since it is accurate and uses a strobe. It is not a logging or statistics tool, so keep it for bench tuning of test pieces.
  - **Audacity** is fine for recording, trimming and labelling notes. Label tracks can be exported and reused as segment boundaries in the script.
  - **Dimowner Audio Recorder** is an appropriate FOSS recorder. Set WAV, 48 kHz, mono. Check whether the phone applies AGC or noise suppression, and hold the phone at a fixed 30–50 cm off-axis from the window to avoid wind noise.
  - **APTuner** was not researched (see Gaps).
- **Most accurate cents for sustained notes, from my reasoning.** On a steady ocarina tone (almost sinusoidal, high SNR), the per-note *median over hundreds of frames* is limited more by breath variation than by the estimator. CREPE (full model with weighted-argmax or Viterbi) and pYIN with fine resolution should both land within about ±1–2 cents of each other. Cross-check the two: if they disagree by more than 3 cents, inspect the segment in Sonic Visualiser.
- **Recommended script outline (Python on Fedora, in a venv):**
  1. Load the WAV at its native 48 kHz: `y, sr = soundfile.read(...)`, mono.
  2. `f0, vflag, vprob = librosa.pyin(y, sr=sr, fmin=440.0, fmax=1760.0, frame_length=4096, hop_length=240, resolution=0.01)`. This gives 5 ms hops and a 1-cent grid, and fmin = 440 Hz aligns the grid with A-440 equal temperament. Optionally run torchcrepe (`model='full'`, `hop_length=sr//200`, `fmin=440`, `fmax=1760`, resampled to 16 kHz) and keep frames with periodicity > 0.5.
  3. Segment: keep voiced frames, then split wherever |Δcents| between consecutive frames exceeds 50 or voicing drops for more than 50 ms. Alternatively, import Audacity labels or Tony's note CSV.
  4. Per segment, discard the first and last 150 ms (attack and release) and compute the median f0, the IQR in cents and the duration. `cents_dev = 1200*log2(f_med / (440*2**((round(69+12*log2(f_med/440))-69)/12)))`, i.e. relative to the nearest equal-tempered note, or relative to the intended note from the fingering list.
  5. Output a CSV and a plot: note → median Hz, deviation in cents, stability. Repeat for 3 takes and report mean ± SD.
- **Blowing curve (breath curve):**
  - For each fingering, record a slow crescendo from the softest to the loudest stable tone.
  - Compute frame RMS (dBFS) alongside f0 and plot cents against dB. The slope in cents/dB and the usable window of dB per note form the blowing curve.
  - Between notes, compare the dB level needed to hit 0 cents; low notes need soft breath and high notes need more pressure, as noted above.
  - For absolute pressure, a cheap water manometer or a digital differential pressure sensor at the mouthpiece would be needed; RMS is only a proxy.

### Gaps
- **APTuner:** not researched, so its licence, algorithm and Play/F-Droid availability are unverified.
- I found no study benchmarking pitch estimators specifically on ocarina or vessel-flute recordings.
- I did not verify whether Dimowner exposes the Android "UNPROCESSED" audio source or disables AGC.
- The Praat manual page did not give an accuracy statement.
- aubio's maintenance status beyond the 2019 release date was not checked.

---

## 8. Print preparation on Fedora: slicers, splitting with dowels/keys, mesh repair, dimensional calibration

### Takeaway
All the main tools are available on Fedora 44 natively or through Flathub:
- PrusaSlicer 2.9.6 (Fedora and Flathub)
- OrcaSlicer 2.4.2 (Flathub only)
- Cura (Fedora ships an old 5.4.0; Flathub has 5.13.0)
- MeshLab 2025.07
- Blender 5.2 with the 3D Print Toolbox 1.4.1

PrusaSlicer's Cut tool adds plug, dowel or snap connectors and dovetails when splitting, which is useful for the drilling jig and for joining PLA halves. For mould-making, keys are better modelled in CadQuery.

### Cited Findings
- **PrusaSlicer** 2.9.6 is in Fedora 44 — [mdapi](https://mdapi.fedoraproject.org/f44/pkg/prusa-slicer) — and on Flathub `com.prusa3d.PrusaSlicer` 2.9.6, AGPL-3.0-only — [Flathub API](https://flathub.org/api/v2/appstream/com.prusa3d.PrusaSlicer).
- **OrcaSlicer** 2.4.2 is on Flathub `com.orcaslicer.OrcaSlicer`, AGPL-3.0-only — [Flathub API](https://flathub.org/api/v2/appstream/com.orcaslicer.OrcaSlicer), [tags](https://github.com/SoftFever/OrcaSlicer/tags). It is not found in Fedora 44 per mdapi.
- **Cura**: Fedora 44 ships `cura` 5.4.0 — [mdapi](https://mdapi.fedoraproject.org/f44/pkg/cura); Flathub `com.ultimaker.cura` has 5.13.0 (LGPL-3.0 and CC-BY-SA-4.0) — [Flathub API](https://flathub.org/api/v2/appstream/com.ultimaker.cura). Git shows 5.14.0-beta — [tags](https://github.com/Ultimaker/Cura/tags).
- **PrusaSlicer Cut tool** (key C):
  - Planar mode at any angle, plus a Dovetail mode with an adjustable tail.
  - Connectors: **Plug**, where a prism is added to one side and subtracted from the other; **Dowel**, where holes are cut in both sides and a separate pin object is generated; and **Snap**.
  - Connector style, shape, depth, size and rotation are adjustable, and tolerance is set next to width and depth.
  - Source: [Prusa Knowledge Base](https://help.prusa3d.com/article/cut-tool_1779)
- **MeshLab** 2025.07 is in Fedora 44 — [mdapi](https://mdapi.fedoraproject.org/f44/pkg/meshlab) — and on Flathub `net.meshlab.MeshLab` 2025.07, GPL-3.0-only — [Flathub API](https://flathub.org/api/v2/appstream/net.meshlab.MeshLab). pymeshlab 2025.7.post1 is GPL-3 — [PyPI](https://pypi.org/pypi/pymeshlab/json).
- **Blender** 5.2.2 is in Fedora 44 — [mdapi](https://mdapi.fedoraproject.org/f44/pkg/blender) — and 5.2 on Flathub, GPL-3.0 — [Flathub API](https://flathub.org/api/v2/appstream/org.blender.Blender).
- **3D Print Toolbox** extension 1.4.1 (released 2026-08-05) requires Blender 4.2 LTS or newer and is GPL-3.0-or-later. It calculates mesh volume and area, checks for bad geometry, offers "Make Manifold", can add thickness, align to bed and scale to size or volume, and exports STL, PLY and OBJ — [extensions.blender.org](https://extensions.blender.org/add-ons/print3d-toolbox/).
- **Python mesh libraries:**
  - trimesh 5.1.0 (MIT) — [PyPI](https://pypi.org/pypi/trimesh/json)
  - manifold3d 3.5.4 — [PyPI](https://pypi.org/pypi/manifold3d/json)
  - numpy-stl 4.0.1 (BSD-3) — [PyPI](https://pypi.org/pypi/numpy-stl/json)
- **Printable-ocarina settings evidence:** nozzle size and wall ordering change the tune and the airway size, so use 0.4 mm nozzle, 0.8 mm walls, outside-to-inside walls — [Printables 412936](https://www.printables.com/model/412936).

### Inferences
- **Recommended stack:**
  1. CadQuery or build123d exports STEP for archiving and STL for printing, with fine tessellation: tolerance about 0.01 mm and angular tolerance about 0.1 rad for the smooth master.
  2. Check watertightness and volume in a script with trimesh or pymeshlab, or in Blender's 3D Print Toolbox.
  3. Slice in PrusaSlicer 2.9.6 from the Fedora repo, or OrcaSlicer from Flathub if you want its calibration wizards (not verified this session).
- **PLA master for plaster:**
  - Print with a 0.1–0.15 mm layer height, or use variable layer height, on the curved outer surface.
  - Sand, then seal with a thin coat (e.g. shellac or primer), then apply mould release.
  - PLA softens at about 55–60 °C and plaster sets exothermically. Keep pours to moderate volumes (general knowledge, not sourced here).
- **Dimensional calibration:**
  1. Print a 50 mm calibration cube and a hole-gauge plate with 2–10 mm holes, which covers the ocarina hole range.
  2. Measure with calipers and set the slicer's XY-compensation or scale correction.
  3. Record the measured shrinkage of the clay body separately and apply it in CAD (§1), not in the slicer.
- **Drilling jig:** a PLA shell that mirrors the outer surface with guide bushings at the calibrated hole centres. The Cut tool's dowels can help if the jig is too large for the bed. Holes should be undersized by about 0.5–1 mm so they can be tuned upward by reaming, since enlarging raises pitch.

### Gaps
- OrcaSlicer's cut-connector feature and calibration wizards were not verified this session.
- Fedora 44 metadata for FreeCAD, praat, colmap, elmerfem and the cadquery Python packages was not found via mdapi. They may exist under different names or only via Flathub or pip.
- I found no source quantifying PLA master deformation under plaster exotherm.
