# clonal-lineage-calling

## Difficulty

This task is intended to model clonal lineage assignment from diploid SSR genotypes under realistic genotyping error. The intended challenge is not a generic programming exercise: the samples are drawn from populations where ramets of the same genet, selfed relatives, and independent genets can produce overlapping multilocus phenotypes because of missing calls, allelic dropout, ±1-repeat scoring errors, and occasional somatic variants.

The scientific difficulty is expected to come from distinguishing discordance caused by stochastic genotyping noise or clonal propagation from genuinely independent genet differences. The current scaffold is intentionally provisional: the parameter set, gate calibration, and difficulty claims are still marked as unvalidated and subject to pilot testing.

## Reference solution

The reference approach is a deterministic, data-driven clustering workflow that operates only on the observed genotypes. For each population, it computes a robust mismatch score between pairs of samples that tolerates missing loci and near-miss alleles caused by ±1-repeat scoring noise or somatic mutation. It then derives a population-specific clustering threshold from the empirical distribution of those pairwise scores rather than from a fixed global cutoff. Connected components within each population define lineage labels, and those labels are written to the required output CSV.

This is a real method that does not import the hidden truth or generator. It is intended as a defensible oracle scaffold, not a final validated benchmark solution.

## Verification

The verifier checks the output file contract before any scientific checks: required file presence, CSV schema, row count, sample completeness, lineage uniqueness, and population-locality constraints. The scientific layer then evaluates the lineage partition against hidden truth when those files are present on the verifier side, computing the split-excess S and merge-excess E metrics by population and testing them against calibrated thresholds.

The current task is intentionally scaffolded without final threshold values or pilot evidence. The verifier therefore permits pending validation while documenting that the hidden truth and thresholds remain unresolved until the calibrated pilot is run. This avoids claiming unverified performance metrics.

## Pilot calibration workflow

A deterministic pilot workflow is recorded in the provenance generator. It creates the public SSR data and emits candidate hidden-truth files in the verifier area with `enabled: false` so the benchmark stays explicitly pending unless a human reviewer approves the real threshold calibration. This keeps the task useful for local development while preserving the requirement to run a real pilot before making final scientific claims.
