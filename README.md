# codemd-metrics

Written by the CodeMD VS Code extension ("Codemd: Publish Product Metrics to
GitHub"). `product.json` is a counts-only summary of the product
as of the default branch: feature and sub-feature status, coverage, test and
bug counts, when each feature last changed, the teams (`@org/team`, from
CODEOWNERS) that own it, a daily trend, and for a feature checked with Check
Feature, its ship-readiness verdict, confidence and counts (never its report),
and for each feature on the codemd.dev list, how complete the code is
(claim counts, coverage, test counts) and which features implement it.

`observations/<run id>.json` is one run's feature list, so codemd.dev can
combine every run into one agreed list. Function names in it are hashed with
the salt in `consensus/salt` (pseudonymous: anyone with the code and this
branch can recompute them). codemd.dev writes that agreed list back here as
`canonical/features.json` and `canonical/decisions.jsonl`. Each publish
removes observations past the newest 200 runs or 90 days, and feature evidence
past the newest 5 runs.

`feature-evidence/<run id>.json` is the matching feature callgraph,
per-function test evidence and per-function recent activity (commits that
changed the function's own lines, and when). Function nodes are keyed by the
same salted hashes and carry the function's name; edges use the hashes.

`security-findings.json` is the Security tab's findings: each one's title,
feature, confidence, whether it is a verified ship blocker, the outcome and
fix in the review's words, and its attack path as function and file names.

No file here names a developer (only team handles) or contains source code
or test names. Only security-findings.json names files. This branch is separate from your code; it never needs to be merged.
