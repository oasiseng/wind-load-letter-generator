# Wind Load Letter Generator

A single-file browser tool that generates a draft wind-pressure certification letter for residential fenestration permitting in Florida, based on [ASCE 7-22](https://www.asce.org/publications-and-news/asce-7) Components & Cladding (Chapter 30, Part 1) wind loads.

You fill in the project info on the left, the letter renders live on the right, and you print to PDF. **The output is a draft template only. It is not engineering certification, and it must be reviewed, modified as needed, and sealed by a licensed Professional Engineer before use on any permit submittal.**

---

## ⚠️ Scope and Limitations — Read This First

**v1.0 is intentionally narrow.** This version is built for the simplest, most common Florida residential permitting case and nothing else:

- **Single-family detached residences**
- **Single-story only** (typical mean roof heights under ~20 ft)
- **Rectangular building plans** with simple gable or hip roofs
- **Enclosed buildings** (per ASCE 7-22 §26.12)
- **Flat or near-flat sites** with no topographic effects (Kzt = 1.0)
- **Wall-mounted fenestration only** — windows, entrance doors, sliding glass doors, storefront/sidelite assemblies, curtain wall, louvers, garage doors, hurricane shutters

### Out of scope for v1.0 (do NOT use this tool for these)

- Multi-story buildings of any kind (residential or commercial)
- Buildings with mean roof height above ~30 ft
- Complex roof geometries (multi-level, monoslope, hip-and-valley with mansards, etc.)
- Non-rectangular building plans
- Open or partially enclosed buildings (warehouses, carports, open pavilions, etc.) — the calculation supports them mathematically, but the boilerplate language and zone treatment in this v1.0 letter is not appropriate for them
- Skylights, roof-mounted components, or any roof zone (1/2/3) calculations — this version only computes wall zones (4/5)
- Sites with topographic effects (Kzt > 1.0) — hills, escarpments, ridges
- Sites in special wind regions (mountainous terrain, gorges)
- Any structure outside Florida or any jurisdiction not using FBC 2023 / ASCE 7-22
- Anything requiring an engineering review more substantive than a fenestration product approval comparison

If your project falls outside the above scope, **do not use this tool**. Use a full structural analysis package and have a licensed PE perform the engineering directly. See [Need a sealed letter?](https://windcalculations.com/contact) below.

---

## What it does

- Computes ASCE 7-22 Components & Cladding wind pressures for the project site
- Builds an 8-page letter template covering: cover letter and intro, site/aerial images and product info, wind design parameters and required design pressures, engineering approval summary and limitations, documentation list with PE sign-off block, an exhibit cover page, and a two-page detailed wind calculation walkthrough showing every step of the math
- Adapts the descriptive language throughout the letter based on the system types in the project (windows, doors, storefronts, etc.)
- Reports all pressures in either **ASD** or **LRFD** basis consistently, with automatic conversions for manufacturer DPs listed at a different basis
- Lives entirely in the browser — nothing is uploaded, no server, no account, no internet required after loading the page once

---

## Versioning

**v1.0 (current).** Single-family detached residential, single-story, simple geometry. Wall zones 4 and 5 only. Enclosed buildings only. Flat terrain only. This is the version published in this repo.

**v2.0 (planned).** Will extend to multi-story residential and light commercial, complex roof geometries, roof zone pressures (zones 1/1'/2/2'/3), topographic factor handling, and a broader system-type library. No release date.

The tool will display the current version in the form panel subtitle so you can verify what you're using.

---

## Quick start

1. Download `wind_letter_generator.html` from this repo
2. Open it in Chrome or Edge (double-click the file, or right-click → Open With → Chrome). Firefox and Safari work but Chrome/Edge handle print rendering most reliably
3. Fill in the form on the left. The letter on the right updates as you type
4. Print using the green button at the bottom of the form (or `Ctrl+P` / `Cmd+P`). Choose **Save as PDF** as the destination, make sure **Background graphics** is checked
5. **Have a licensed PE review the output, modify as needed, and apply the seal and signature** — there is a clearly marked box on the signature page for the seal

No installation, no build step, no dependencies. The file is portable.

---

## Wind speed lookup

The tool requires you to enter the ultimate design wind speed (V) for the project location. Two free tools you can use:

- **[ASCE 7 Hazard Tool](https://ascehazardtool.org)** — the official ASCE site. Pick "Wind", "ASCE 7-22", the risk category, drop a pin on the site, and it returns the wind speed. This is the authoritative source.
- **[windcalculations.com](https://windcalculations.com)** — free wind-speed lookup tool with FL-specific defaults. Maintained by Oasis Engineering. Faster for typical FL projects.

Both will give you the same number for any FL site. Use whichever is more convenient.

---

## ASD vs LRFD — quick primer

This matters because if you mix bases, the comparison between site pressures and manufacturer DPs is meaningless.

**ASCE 7-22 produces ultimate (strength-level / LRFD) wind pressures.** That's how the standard works.

**Florida Product Approvals usually list design pressures in ASD (allowable stress design).** That's the industry convention.

These two are **not directly comparable** without conversion. Per ASCE 7-22 §2.4.1:

```
W_ASD = 0.6 × W_strength
```

So a strength-level wind pressure of 50 psf is equivalent to 30 psf in ASD. A manufacturer DP of 90 psf (ASD) is equivalent to 150 psf at strength level.

### What the tool does about it

The **Pressure reporting basis** selector controls what basis every pressure in the letter is reported in. Set it to ASD (default) and every reported number — the headline DP, the zone table on page 3, the calc table on page 7b — is multiplied by 0.6 internally and labeled "(ASD)".

For each product, you tell the tool which basis the manufacturer used (the "Listed DP basis" dropdown). If it matches the letter basis, the DP is shown as-is. If it differs, the tool converts and prints both values, bolding the one used for comparison.

**Rule of thumb for FL residential:** set the letter to **ASD** and set each product's listed basis to **ASD**. That matches Florida Product Approval convention and what reviewers expect.

---

## Disclaimer

**THIS SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED.**

- This tool produces a **draft letter template only**, not engineering certification. The output is not valid as a permit submittal until reviewed, edited as needed, and sealed by a licensed Professional Engineer who has independently verified all inputs, calculations, and conclusions
- Wind pressure calculations use ASCE 7-22 Components & Cladding methodology for wall zones (4 and 5). The implementation has been spot-checked against published reference values but has not been independently audited or certified
- No warranty is made regarding the accuracy, completeness, fitness for any particular purpose, or compliance with any building code, jurisdiction, or product approval
- The user (and any sealing engineer) is solely responsible for verifying every input, every output number, every code reference, and every word of boilerplate language for accuracy and applicability to the specific project
- This tool does not constitute engineering services, an engineer-client relationship, or a substitute for a licensed Professional Engineer's independent judgment
- Use of this tool does not create any obligation or liability on the part of the authors, contributors, or Oasis Engineering LLC

**If you are not a licensed Professional Engineer and you are using this output for a permit submittal, you are likely engaging in the unauthorized practice of engineering, which is illegal in every U.S. state. Don't do that. Hire a PE.**

---

## Need a sealed letter?

If you are a contractor, homeowner, or building official looking for a sealed wind-pressure letter for a Florida project — or if your project falls outside the v1.0 scope above — Oasis Engineering provides sealed wind calculation services across all 50 states (currently licensed in 37):

- [oasisengineering.com](https://oasisengineering.com) — main firm site
- [windcalculations.com](https://windcalculations.com) — wind-specific service hub with calculators and tools
- [floridawindcalcs.com](https://floridawindcalcs.com) — FL-specific wind letter service

Typical turnaround for residential FL wind letters is 24–48 hours. Multi-state, multi-story, container homes, manufactured homes, solar, and other specialty wind analysis available.

---

## License

This project is released under the [MIT License](LICENSE). You are free to use, modify, and redistribute it. The license does **not** waive the requirement that engineering work be performed and sealed by a licensed PE.

---

## Contributing

This project is published as a public reference implementation. **Pull requests, feature requests, and support requests are not accepted.** See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

If you want a tool tailored to a specific scope, an extension to multi-story or commercial work, or a sealed letter for an actual project, contact Oasis Engineering directly using the links above.

---

## Tech notes

- **Single HTML file.** All HTML, CSS, and JavaScript are contained in `wind_letter_generator.html`. No build step, no dependencies, no internet required at runtime (only on initial load for Google Fonts, which degrades gracefully if blocked)
- **Runs entirely in the browser.** No data leaves the device. Project info, manufacturer products, uploaded images — all stay local. Safe for use with confidential project data
- **Calculation engine.** Implemented from scratch following ASCE 7-22 Chapter 30 Part 1. Reference check: V=160 mph, Exposure C, h=30 ft, θ=4.76°, A=50 sf → Zone 4: +52.92 / -57.84 psf, Zone 5: +52.92 / -66.52 psf (strength level)
- **Browser support.** Best on Chrome and Edge (Chromium-based). Firefox and Safari work but print rendering of the background swoosh decoration may be inconsistent

---

## Repository structure

```
wind-letter-generator/
├── README.md                       this file
├── LICENSE                         MIT license text
├── CONTRIBUTING.md                 contribution policy (short version: no)
└── wind_letter_generator.html      the tool — just open in a browser
```
