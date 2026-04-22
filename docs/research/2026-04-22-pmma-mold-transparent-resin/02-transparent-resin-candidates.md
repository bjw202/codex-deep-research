# Transparent Resin Candidates for PMMA Mold Use

**Researcher**: R2  
**Mode**: mixed  
**Date**: 2026-04-22  
**Scope**: Transparent cast/mold/replication resin families evaluated only through the lens of PMMA mold compatibility, optical clarity, cure temperature/exotherm, shrinkage, viscosity, adhesion to PMMA, inhibitors/solvents, demolding, and prototype vs production fit.

## Executive Notes

PMMA is a good optical mold surface only when the resin system is chemically mild and thermally disciplined. The biggest practical filters are: avoid solvent-rich or styrene-rich systems, avoid cure schedules that push the mold near PMMA softening, and assume that strong wetting plus low shrinkage will increase the odds of sticking unless a release strategy is in place.

The best near-term candidates for direct PMMA-mold replication are low-viscosity, room-temperature, solvent-free clear urethanes and room-temperature clear epoxies. UV-curable acrylate/urethane acrylate systems can work for fast prototyping, but they are usually more shrink-prone and more sensitive to oxygen inhibition and local cure stress. Polyester is the least PMMA-friendly of the listed families because the styrene/solvent character raises attack and crazing risk. Silicone/PDMS is chemically gentle and dimensionally stable, but its softness and elasticity make it a poor match when the goal is a rigid optical replica rather than a flexible part.

## Key Findings

1. PMMA itself is the limiting substrate. The ACRYLITE PMMA technical sheet lists acetone, MEK, methanol, ethyl acetate, and similar solvents as non-resistant, and it warns that the sheet softens above about 91 C and has a 105 C Vicat softening point. That means any resin family with solvent content, aggressive monomers, or a cure schedule that adds heat margin risk to the mold.

2. UV-curable acrylate and urethane acrylate systems are fast and often transparent, but they are the shrinkiest of the useful clear families. The photocurable-materials review notes that acrylate systems dominate because they process quickly, yet shrinkage is more noticeable in acrylic formulations than in epoxy; it also states that viscosity must usually stay below 5 Pa/s for vat processes and that oxygen inhibition is a real issue for free-radical systems. Incure optical-bonder datasheets show the family can be very clear and low viscosity, but shrinkage can still range from 0.01% to 1.9% depending on formulation, so direct PMMA molding needs release and validation.

3. Clear epoxies and clear urethanes are the better fit when the target is a rigid transparent part from a PMMA mold. Epoxies give the best dimensional stability on the list, with vendor and review sources consistently describing low shrinkage and lower warp than acrylates, while clear urethanes combine water-clear appearance, room-temperature cure, low viscosity, and negligible shrinkage in the common casting grades. Polyester remains viable for some decorative clear castings, but its styrene content and higher exotherm make it the riskiest family for PMMA molds; silicone/PDMS is low-shrink and optically clear, but its softness and the higher cure temperatures used by some optical silicone systems narrow its use to special cases.

## Evidence Table

| claim | evidence | source type | confidence | URL |
| --- | --- | --- | --- | --- |
| PMMA is vulnerable to common casting solvents and softens near typical post-cure temperatures | ACRYLITE chemical-resistance chart marks acetone, MEK, methanol, ethyl acetate, toluene, xylene, etc. as non-resistant; PMMA sheet softens above about 91 C and has a Vicat softening point of 105 C | official manufacturer datasheet | high | https://www.acrylite.co/files/content/acrylite.co/documents/product-information/premium/ACRYLITE-Premium-FF-Technical%20Information.pdf |
| Acrylate photopolymer systems shrink more than epoxy and are oxygen-sensitive | Review states acrylate/methacrylate resins are the common radical systems, viscosity must be low for vat processing, transparency must be sufficient, and shrinkage is more noticeable in acrylic than in epoxy; oxygen inhibition is an issue for free-radical systems | academic review | high | https://journals.sagepub.com/doi/10.1177/2280800018764770 |
| UV-curable urethane acrylates can be clear, low viscosity, and very low shrink, but not universally | Incure 7210 is clear, 30-100 cP, 0.05% linear shrinkage; Incure 7664 is clear, 2000-4000 cP, 1.90% linear shrinkage; Incure 7811G is ultra-low shrink, 100K-200K cP, 0.01% linear shrinkage | official vendor datasheets | high | https://www.uv-incure.com/images/PDF/INCURE-7210-.pdf ; https://www.uv-incure.com/images/PDF/INCURE-7664.pdf ; https://uv-incure.com/images/PDF/Optik_7811G_TDS-.pdf |
| UV-curable epoxy can combine optical clarity with low shrink and high Tg | LE-2441 is solvent-free, optically clear, UV-curable, 2500 +/- 500 cP, Tg 157 C, and oxygen-inhibition resistant; LOCTITE 3296 is UV-curable with 0.3% shrinkage and high Tg | official vendor datasheets | high | https://www.caplinq.com/le-2441-one-part-solvent-free-optically-clear-epoxy-resin-le-2441.html ; https://www.caplinq.com/loctite-3296-uv-curable-epoxy-adhesive-for-modules-assembly-3296.html |
| Room-temperature clear urethane casting resins are one of the best direct-cast options for PMMA molds | Poly-Optic 14-Series is water-clear, low-viscosity, long pot-life, and aimed at optical clarity; Smooth-On Crystal Clear 202 EU is water-white, low-viscosity, room-temp cure, negligible shrinkage, UV resistant, and not brittle | official vendor technical bulletins | high | https://polytek.com/content/pdf/technicalbulletin/Polytek_TB_PolyOptic_14-Series_5-5-2021.pdf ; https://www.smooth-on.com/tb/files/CRYSTAL_CLEAR_202_EU_TB.pdf |
| Polyester clear casting resin is clear but carries styrene and heat risk | ETI Castin'Craft Clear Polyester Casting Resin is described as clear, mass-cast capable, low peak exotherm, and minimal shrinkage; the resin basics sheet says casting resin is polyester, has a styrene odor, and over-catalyzing can cause excessive heat and mold distortion; TAP Clear-Lite TDS identifies the resin family as unsaturated polyester resin in styrene | official vendor instructions and SDS/TDS | high | https://eti-usa.com/content/pdfs/ETI_instructions_castingcraftresin_10-27-2020.pdf ; https://www.tapplastics.com/image/pdf/Tech%20Data-%20Flex-Isophthalic.pdf ; https://www.tapplastics.com/image/pdf/MSDS%20TAP%20Casting%20Resin.pdf |
| Optically clear silicones are low-shrink and thermally robust, but softness limits rigid replica use | Dow SILASTIC MS-1001 is optically clear with 92% luminous transmittance and 14 Pa.s mixing viscosity; Momentive INVISISIL silicone is optically clear, low-shrink, and cures at 60 C; Momentive Silopren LSR 7005 is ultra-clear, 94% transmission, <1% haze, and high-temp resistant | official vendor pages and TDS | medium | https://www.dow.com/en-us/pdp.silastic-ms-1001-moldable-silicone.04117871z.html ; https://www.momentive.com/en-us/product-categories/formulated-products/optical-bonding/thermal-cure ; https://www.momentive.com/content/dam/momentive/en-us/products/tds/silopren/silopren-lsr-7005.pdf |
| PMMA is workable as a clear mold only if resin chemistry stays mild and release is validated | ACRYLITE warns that stress, temperature, and chemistry all matter; several resin instructions recommend trial castings and warn about heat build-up, solvent attack, or mold distortion | inference from official sources | medium | https://www.acrylite.co/files/content/acrylite.co/documents/product-information/premium/ACRYLITE-Premium-FF-Technical%20Information.pdf ; https://eti-usa.com/content/pdfs/ETI_instructions_easycastclear_10-27-2020.pdf |

## Contradictions And Uncertainty

The sources disagree mainly on how optimistic to be about clear resin casting in rigid plastic molds. Vendor guidance often assumes silicone, urethane rubber, or polypropylene molds, while the PMMA sheet data show that acrylic is sensitive to solvent exposure and heat. That means a product that is excellent in silicone may still be only marginal in PMMA.

The biggest uncertainty is family-to-family variability inside each resin class. A "clear urethane" can be near-zero shrink in one formulation and much higher in another. The same is true for UV acrylates and epoxies. The ranking here is therefore about family tendencies plus the specific products used as evidence, not a universal guarantee for every brand.

Thermoplastic options are the weakest-supported part of this memo because the question is really about PMMA mold compatibility, not a full melt-processing comparison. The practical inference is that any thermoplastic route that needs temperatures near or above PMMA's softening range is a poor direct-mold choice.

## Decision Implications

For a first pass with a PMMA mold, start with a room-temperature clear urethane casting resin or a room-temperature clear epoxy, then test a small coupon for release and surface haze. Use a polished mold, avoid solvent wipes, and assume a release agent or barrier coat may be needed.

Use UV-curable acrylate or urethane acrylate only when speed or thin-section replication matters more than shrink control. Prefer 100% solids, solvent-free formulations and expect oxygen inhibition and post-cure sensitivity.

Avoid polyester unless you have a reason to accept styrene odor, higher exotherm, and a higher probability of PMMA attack. Silicone/PDMS is the safe chemistry choice, but it is more a flexible optical encapsulant or molding material than a rigid optical replica system.

## Adjacent Questions

1. Which specific PMMA grade is the mold stock: cast acrylic, extruded acrylic, or coated acrylic?
2. Is the process a one-off cast, a short-run prototype tool, or a repeated production mold?
3. Do you need a rigid clear part, or is a flexible optically clear part acceptable?

## Source List

| # | source | date | confidence | URL |
| --- | --- | --- | --- | --- |
| 1 | ACRYLITE Premium FF Technical Information | 2024-07 | high | https://www.acrylite.co/files/content/acrylite.co/documents/product-information/premium/ACRYLITE-Premium-FF-Technical%20Information.pdf |
| 2 | ACRYLITE Chemical Resistance Chart | 2025-03 | high | https://www.acrylite.co/files/content/acrylite.co/documents/product-information/ACRYLITE-Chemical-Resistance-Chart.pdf |
| 3 | 3D printing processes for photocurable polymeric materials | 2018 | high | https://journals.sagepub.com/doi/10.1177/2280800018764770 |
| 4 | Incure Optik 7210 TDS | 2025 | high | https://www.uv-incure.com/images/PDF/INCURE-7210-.pdf |
| 5 | Incure Optik 7664 TDS | 2025 | high | https://www.uv-incure.com/images/PDF/INCURE-7664.pdf |
| 6 | Incure Optik 7811G TDS | 2025 | high | https://uv-incure.com/images/PDF/Optik_7811G_TDS-.pdf |
| 7 | OPTOLINQ LE-2441 product page | 2026-04 | high | https://www.caplinq.com/le-2441-one-part-solvent-free-optically-clear-epoxy-resin-le-2441.html |
| 8 | LOCTITE 3296 product page | 2026-04 | high | https://www.caplinq.com/loctite-3296-uv-curable-epoxy-adhesive-for-modules-assembly-3296.html |
| 9 | Poly-Optic 14-Series technical bulletin | 2021-05 | high | https://polytek.com/content/pdf/technicalbulletin/Polytek_TB_PolyOptic_14-Series_5-5-2021.pdf |
| 10 | Crystal Clear 202 EU technical bulletin | 2025-12 | high | https://www.smooth-on.com/tb/files/CRYSTAL_CLEAR_202_EU_TB.pdf |
| 11 | ETI Castin'Craft Casting Resin Basics | 2020-10 | high | https://eti-usa.com/content/pdfs/ETI_instructions_castingcraftresin_10-27-2020.pdf |
| 12 | TAP Clear-Lite Casting Resin TDS / SDS | 2018 / 2004 | medium | https://www.tapplastics.com/image/pdf/Tech%20Data-%20Flex-Isophthalic.pdf ; https://www.tapplastics.com/image/pdf/MSDS%20TAP%20Casting%20Resin.pdf |
| 13 | Dow SILASTIC MS-1001 product page | 2026-04 | medium | https://www.dow.com/en-us/pdp.silastic-ms-1001-moldable-silicone.04117871z.html |
| 14 | Momentive INVISISIL thermal cure silicones | 2026-04 | high | https://www.momentive.com/en-us/product-categories/formulated-products/optical-bonding/thermal-cure |
| 15 | Momentive Silopren LSR 7005 TDS | 2025-12 | high | https://www.momentive.com/content/dam/momentive/en-us/products/tds/silopren/silopren-lsr-7005.pdf |

## Search And Source Budget

| surface | count |
| --- | --- |
| web searches | 12 |
| source inspections | 10 |
