# Repair Notes

Verifier pass for the critic review repair queue in `99-critic-review.md`.

## H1
- Target file: `97-journal.md` and future `00-final-synthesis.md`
- Original claim: The synthesis mixes transparent-resin compatibility with PMMA forming / replication routes, so R3 reads like primary evidence for resin selection instead of adjacent context.
- Cited source if present: `97-journal.md` says the working synthesis includes both resin-family choice and PMMA forming routes; `03-pmma-mold-forming-methods.md` explicitly frames PMMA replication routes as a separate process chain.
- Source check result: Supported. The journal and R3 both show the scope overlap, and the criticism about framing is valid.
- Correction: Rewrite the synthesis so R3 is labeled as supporting process context only, while resin-family selection remains the primary decision axis.
- Confidence: High

## H2
- Target file: `02-transparent-resin-candidates.md`
- Original claim: “The best near-term candidates for direct PMMA-mold replication are low-viscosity, room-temperature, solvent-free clear urethanes and room-temperature clear epoxies.”
- Cited source if present: `02-transparent-resin-candidates.md` cites specific urethane, epoxy, and vendor datasheets, and later states that family-to-family variability means the ranking is about tendencies plus examples, not a universal guarantee.
- Source check result: Partially supported. The cited examples justify a first-pass preference, but not a universal compatibility order across all formulations.
- Correction: Rephrase the ranking as a formulation-specific first-pass hypothesis, not a broad family-level rule.
- Confidence: High

## M1
- Target file: `04-surface-release-optical-durability.md`
- Original claim: The release/optical durability guidance focuses on PMMA surface energy, thin fluorinated release layers, haze, transmittance, roughness, and birefringence.
- Cited source if present: `04-surface-release-optical-durability.md` cites surface tension / SFE, FDTS, ReleasePLAS, haze/transmittance, and birefringence references.
- Source check result: Supported, but incomplete. The file covers the main release and optical QA points, yet it does not explicitly elevate residue transfer, cycle-life degradation, UV-grade dependence, or stress / birefringence aging as failure modes.
- Correction: Add those failure modes to the durability discussion or the uncertainty section so the optical-release guidance reflects actual process risk.
- Confidence: Medium

## M2
- Target file: `01-process-feasibility.md`
- Original claim: PMMA tooling is feasible only in a narrow low-heat, low-stress, chemically gentle envelope, and should be treated as prototype or short-run tooling rather than durable production tooling.
- Cited source if present: `01-process-feasibility.md` cites PMMA thermal limits, chemical fragility, and UV / low-temperature yes-cases.
- Source check result: Supported in substance, but the boundary language is too strong if stated as “only viable.” The evidence shows narrow viability, not exclusivity.
- Correction: Soften to “viable in narrow low-heat, low-stress, chemically gentle regimes” while preserving the short-run / prototype nuance.
- Confidence: High

## M3
- Target file: `04-surface-release-optical-durability.md`
- Original claim: PMMA surface energy is described as moderate, with release analysis using both surface tension and surface free energy numbers.
- Cited source if present: `04-surface-release-optical-durability.md` uses 44-45 mN/m as surface tension from one film datasheet and about 39.5-40 mN/m as surface free energy from academic work.
- Source check result: Supported, but terminology is mixed. Surface tension and surface free energy are related but not numerically interchangeable, so the current wording can mislead readers into treating them as the same metric.
- Correction: Label the metric used by each source explicitly and avoid implying the values are directly equivalent across grades or measurement methods.
- Confidence: High

## Unresolved
- H1 still needs to be applied in the journal and carried forward into the eventual final synthesis, since `00-final-synthesis.md` is not present yet.
- M1 remains a documentation gap rather than a direct contradiction; the missing failure modes should be added in a later repair pass if the synthesis depends on them.
