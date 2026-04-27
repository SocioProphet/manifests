# SocioProphet Beam/Ray Manifest Evidence Contract

Status: draft
Owner: SocioProphet MLOps
Consumes:
- SocioProphet/socioprophet-standards-knowledge: `standards/ray-learning-ecosystem-standard.v1.md`
- SocioProphet/socioprophet-standards-knowledge: `standards/model-serving-loop-standard.v1.md`
- SocioProphet/socioprophet-standards-knowledge: `standards/evaluation-fabric-standard.v1.md`
- SocioProphet/socioprophet-standards-storage: `standards/evaluation-record-standard.v1.md`
- SocioProphet/socioprophet-standards-storage: `standards/evidence-bundle-standard.v1.md`
- SocioProphet/sociosphere: `standards/angel-of-the-lord/README.md`

## Purpose

This document defines how SocioProphet deployment manifests must carry evidence references for Beam data lineage, Ray learning runs, model-serving runtime classification, evaluation results, regression checks, and rollback or remediation.

## Manifest doctrine

A manifest is not only deployment YAML. For SocioProphet learning systems, a manifest must be evidence-bound:

```text
manifest -> data lineage -> model/run lineage -> evaluation record -> regression check -> serving runtime classification -> rollback path -> Angel gate where required
```

## Required manifest annotations or sidecar metadata

SocioProphet manifests SHOULD include or reference:

```yaml
socioprophet.io/data-pipeline-decision: DataPipelineDecision id
socioprophet.io/beam-pipeline-ref: Beam pipeline or output dataset ref
socioprophet.io/ray-learning-run: RayLearningRun id
socioprophet.io/evaluation-record: EvaluationRecord id
socioprophet.io/evidence-bundle: EvidenceBundle id
socioprophet.io/epoch-regression-check: EpochRegressionCheck id
socioprophet.io/serving-runtime: ray_serve | kuberay | kserve | seldon | triton | bentoml | mlflow | torchserve | tensorflow_serving | legacy_clipper | other
socioprophet.io/runtime-status: primary | supported | specialized | experimental | legacy_reference | deprecated
socioprophet.io/rollback-policy: required policy or artifact ref
socioprophet.io/angel-grade: AngelEpochGrade id where required
```

## Beam/Ray rules

- Beam is the canonical durable data pipeline substrate.
- Ray Data is a Ray-local adapter unless a Beam exception is documented.
- Ray Train, Ray Tune, Ray RLlib, Ray Serve, and KubeRay are canonical Ray learning/runtime components.
- Ray Serve and KubeRay are the primary serving substrate for new SocioProphet serving work.
- Clipper is legacy-reference only and must never be marked as active primary runtime.

## Blocking conditions

A manifest should fail SocioProphet promotion review if:

- data lineage is missing;
- Beam exception is missing when Beam is not used for durable data processing;
- evaluation record is missing;
- regression check is missing for epoch-bearing subjects;
- runtime status is absent or incorrect;
- rollback path is absent;
- Angel of the Lord review blocks publication, transition, or deployment.

## Runtime examples

### Ray Serve / KubeRay primary path

```yaml
socioprophet.io/serving-runtime: ray_serve
socioprophet.io/runtime-status: primary
socioprophet.io/ray-learning-run: ray-run-...
socioprophet.io/evaluation-record: eval-...
socioprophet.io/evidence-bundle: evidence-...
```

### Clipper legacy reference only

```yaml
socioprophet.io/serving-runtime: legacy_clipper
socioprophet.io/runtime-status: legacy_reference
socioprophet.io/active-default: "false"
```
