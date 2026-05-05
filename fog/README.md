# Fog manifests subtree

This subtree remaps FogStack deployment and profile work into the existing `SocioProphet/manifests` repo.

## Contents

- `base/` — canonical Fog deployment bundle skeleton
- `overlays/single-home/` — local/single-site profile overlay and example
- `overlays/multi-home/` — fleet-managed two-site profile overlay and example
- `overlays/regional-multimesh/` — regional multimesh profile overlay and example
- `examples/site-seed-demo/` — demo topology/site seed
- `docs/` — deployment profile and planning-alignment notes

## Current profile classes

The subtree currently carries three profile classes:

1. `single-home`
2. `multi-home`
3. `regional-multimesh`

These are shared deployment/profile composition seeds. Runtime gateway behavior remains in `SocioProphet/cloudshell-fog`; shared contracts remain in `SocioProphet/api-spec`; shared policy decisions remain in `SocioProphet/policy-fabric`; release-proof and trust-graph work remains in `SocioProphet/prophet-platform`.

## Working rule

Changes to shared deployment/profile shape should land here first or in lockstep with runtime and release-proof changes that consume those profiles.
