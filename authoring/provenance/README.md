# Provenance and design notes

This task is a benchmark scaffold for clonal lineage calling from SSR genotypes, not a final validated task instance. The intended biological setting is plant clonal-genetics work in which ramets of the same genet are expected to share a multilocus genotype but may show discordance because of missing calls, allelic dropout, ±1-repeat scoring errors, and rare somatic mutation.

## Literature-supported motivation

The task is motivated by routine population-genetic practice for assigning individual samples to clonal lineages or genets using codominant multilocus marker data such as SSR microsatellites. In field and restoration studies, this is often done to distinguish clonal ramets from sexually produced or independently generated genets.

## Design assumptions

The benchmark is intentionally built around a simplified yet realistic model:

- diploid codominant SSR genotypes
- population-specific clonal structure
- missing alleles and scoring noise
- somatic ±1-repeat drift
- no assumption that all samples with identical multilocus profiles are necessarily the same genet without considering the genotype-specific noise model

## Provisional parameters

The following values are provisional and may change after pilot calibration:

- number of loci
- sample sizes per population
- clonal ramet counts
- error rates and missingness rates
- dropout rates
- somatic mutation rate
- threshold calibration for split excess / merge excess
- ceiling rules for acceptable discordance

These values are not final unless the pilot evidence confirms them.

## Open scientific questions

- whether the task is better framed as a distance-threshold problem or as a likelihood-based assignment problem
- whether hidden truth in the verifier is sufficient for the fixed-data design
- whether the intended challenge is driven mainly by genotype noise or by true genet differentiation

## Canary and data-format policy

CSV and JSON files are not modified with inline comments because doing so would break parsers. The project therefore records the canary issue and the DQ 23.2 open question in authoring evidence notes instead of corrupting data files.
