# PMMA Mold Forming Methods - Transparent Resin

**Researcher**: R3  
**Mode**: mixed  
**Date**: 2026-04-22  
**Scope**: Non-machining fabrication routes for PMMA molds/replicas, including hot embossing, thermal nanoimprint/microimprint, injection molding, compression molding, solvent/cast replication from MMA or PMMA solutions, thermoforming/vacuum forming, UV-assisted replication where relevant, and the master-tool chain needed before PMMA replication.

## Executive Notes

PMMA can be replicated with useful precision by thermal embossing and thermal nanoimprint, and those are the most directly defensible routes for fine micro/nano features. Injection compression molding is stronger for throughput and optical parts, but PMMA shrinkage/recovery still limits exact pitch transfer. Casting PMMA/MMA against a treated master can preserve nanostructure and optical finish well, but it is chemistry- and cure-sensitive. Thermoforming/vacuum forming works only where coarse precision is acceptable. For direct PMMA replication, rigid masters with low roughness and low surface energy matter more than the nominal process name.

## Key Findings

1. Hot embossing of PMMA can faithfully transfer microfeatures in the low-micron range, but filling becomes incomplete as cavities shrink and aspect ratio rises.
2. Thermal nanoimprint on PMMA reaches submicron to millimeter scale, but the practical limit depends strongly on temperature, pressure, imprint time, molecular weight, and recovery after imprint.
3. Injection compression molding can improve PMMA replication accuracy versus plain injection molding, but shrinkage and warpage still define the final pitch and form error.
4. Solvent/cast replication using PMMA dissolved in MMA, or PMMA precursor mixtures cast on fluorinated silicon masters, can produce high-fidelity nanotopography with good release.
5. Thermoforming/vacuum forming is the weakest precision route here; it is acceptable for ~hundreds of microns features, not for optical micro/nano detail.
6. Master choice is the real bottleneck: quartz, chromium, silicon, nickel electroforms, and epoxy masters are all used; anti-sticking treatments are often the difference between clean release and damaged replicas.

## Evidence Table

| claim | evidence | source type | confidence | URL |
| --- | --- | --- | --- | --- |
| PMMA hot embossing can reproduce 1.6-4.6 µm periods and 180 nm-2.6 µm heights with high fidelity, but smaller cavities underfill. | Chromium molds replicated onto 200 µm PMMA foils gave 99.1% height fidelity at 4.6 µm period and only 80.0% at the smaller 2.7 µm/1.5 µm case; process ran at 115 °C, 34.3 MPa, 5 min, demolded at 40 °C with no anti-sticking layer. | academic | high | https://www.nature.com/articles/s41598-020-79936-1 |
| Thermal NIL on PMMA spans 100 nm to millimeter scale, but feature size ceiling depends on temp, pressure, time, and PMMA molecular weight. | NIL on PMMA at 200 °C, 20 bar, 20 min duplicated a 1.3 mm square pattern without defects using 12 kg/mol PMMA; the study explicitly links duplicability to imprint conditions and resist thickness/etch back. | academic | high | https://www.sciencedirect.com/science/article/abs/pii/S0167931706000281 |
| Injection compression improves PMMA replication accuracy, but shrinkage still shifts pitch. | In PMMA Fresnel lens replication, compression improved pitch transfer; reported absolute deviations were about 0.1-0.8 µm for step height and about 3.7-11.1 µm for pitch depending on mode, with PMMA showing better average replication than COP because of lower viscosity. | academic | high | https://pmc.ncbi.nlm.nih.gov/articles/PMC6316790/ |
| Variotherm injection molding is a viable PMMA replication route for microstructured parts, but it trades against tooling and machine cost. | PMMA microstructures made by variotherm injection molding were described as having high replication numbers at low cycle times and precise demolding; the paper frames high machine and mold cost as the main drawback. | academic | medium | https://pmc.ncbi.nlm.nih.gov/articles/PMC6521382/ |
| Mold cavity thickness and mold surface roughness materially affect PMMA micro-injection outcomes. | In PMMA micro-injection molding, cavity thickness ranged from 0.05 to 0.25 mm and cavity roughness from Ra 46.55 nm to 462.57 nm; filling integrity and roughness replication ratio varied strongly with both parameters. | academic | medium | https://pmc.ncbi.nlm.nih.gov/articles/PMC9860902/ |
| PMMA/MMA casting against a treated silicon master can replicate nanoscale gratings and benefits from fluorinated release coating. | PMMA (120k Mw) dissolved in MMA at 8 wt% with 2 wt% DMPA was deposited on FTDS-coated silicon molds patterned with nanoscale gratings, indicating a solvent-cast and polymerized replication route with built-in release support. | academic | high | https://pmc.ncbi.nlm.nih.gov/articles/PMC3940926/ |
| Thermoforming/vacuum forming is precision-limited relative to embossing, but can form PMMA microcontainers around the 300 µm scale. | A thin PMMA plate was thermoformed into a 25x25 array of thin-walled microcontainers, each about 300 µm in diameter and depth, with the tool evacuated and heated above Tg before forming. | academic | medium | https://pmc.ncbi.nlm.nih.gov/articles/PMC2583012/ |
| Nickel electroforms, Cr molds, quartz molds, and epoxy masters are all practical pre-PMMA master-tool options. | Electroforming transferred nano-to-micro details from a direct-written master into nickel with little loss; the nickel mold then hot-embossed PMMA foils. Separately, quartz/Cr molds embossed PMMA via a low-cost optical microembossing route, and epoxy masters were reported to release without special solvents. | academic | high | https://pmc.ncbi.nlm.nih.gov/articles/PMC7183046/ ; https://pmc.ncbi.nlm.nih.gov/articles/PMC4138730/ ; https://pmc.ncbi.nlm.nih.gov/articles/PMC3117225/ |
| UV-assisted replication is not the standard direct route for PMMA; it is mainly a parallel route for UV-curable resists. | The NIL literature distinguishes UV-NIL resists from thermoplastic PMMA and notes that thermal NIL remains more widely used for PMMA-compatible replication because it works with a broader range of polymer materials. | academic | medium | https://www.sciencedirect.com/science/article/abs/pii/S0167931706000281 |

## Contradictions And Uncertainty

The strongest tension in the literature is between fidelity and throughput. Hot embossing and thermal NIL give the best micro/nano transfer, but injection molding and injection compression are more attractive for volume. Another uncertainty is direct comparability: several sources report PMMA itself, while others report PMMA/COP, PET, or masters that later transfer into PMMA. The direction is clear, but exact process windows are not universal because PMMA molecular weight, mold release chemistry, and thermal history shift recovery, shrinkage, and warpage.

## Decision Implications

If the target is optical or microfluidic PMMA with sub-10 µm detail, start with thermal embossing or thermal NIL on a rigid, low-Ra master and plan for fluorinated release treatment. If the target is multi-cavity or higher-volume PMMA optics, injection compression is the better production route, but expect process compensation for pitch shrinkage and demolding stress. If the target tolerates only coarse precision, thermoforming can be a lower-cost shape route, but it is not the right answer for fine optical surface relief.

## Adjacent Questions

1. Which master fabrication chain gives the best cost-to-fidelity ratio for PMMA replicas: LIGA/nickel electroform, quartz/Cr, or silicon with fluorosilane release?
2. How much of the apparent PMMA shrinkage is process-induced recovery versus geometry-induced elastic springback after release?

## Source List

| # | source | date | confidence | URL |
| --- | --- | --- | --- | --- |
| 1 | Wettability control of polymeric microstructures replicated from laser-patterned stamps | 2020 | high | https://www.nature.com/articles/s41598-020-79936-1 |
| 2 | Pattern replication of 100 nm to millimeter-scale features by thermal nanoimprint lithography | 2006 | high | https://www.sciencedirect.com/science/article/abs/pii/S0167931706000281 |
| 3 | Manufacturing Signatures of Injection Molding and Injection Compression Molding for Micro-Structured Polymer Fresnel Lens Production | 2018 | high | https://pmc.ncbi.nlm.nih.gov/articles/PMC6316790/ |
| 4 | Cell Morphology on Poly(methyl methacrylate) Microstructures as Function of Surface Energy | 2019 | medium | https://pmc.ncbi.nlm.nih.gov/articles/PMC6521382/ |
| 5 | Effects of Cavity Thickness and Mold Surface Roughness on the Polymer Flow during Micro Injection Molding | 2023 | medium | https://pmc.ncbi.nlm.nih.gov/articles/PMC9860902/ |
| 6 | Nanotopographic Substrates of Poly (Methyl Methacrylate) Do Not Strongly Influence the Osteogenic Phenotype of Mesenchymal Stem Cells In Vitro | 2014 | high | https://pmc.ncbi.nlm.nih.gov/articles/PMC3940926/ |
| 7 | Microfabrication of Chip-sized Scaffolds for Three-dimensional Cell cultivation | 2009 | medium | https://pmc.ncbi.nlm.nih.gov/articles/PMC2583012/ |
| 8 | Synergies between Surface Microstructuring and Molecular Nanopatterning for Controlling Cell Populations on Polymeric Biointerfaces | 2020 | high | https://pmc.ncbi.nlm.nih.gov/articles/PMC7183046/ |
| 9 | Hot embossing for fabrication of a microfluidic 3D cell culture platform | 2011 | medium | https://pmc.ncbi.nlm.nih.gov/articles/PMC3117225/ |

## Search And Source Budget

| surface | count |
| --- | --- |
| web search calls | 15 |
| open/source-inspection calls | 2 |
| total | 17 |
