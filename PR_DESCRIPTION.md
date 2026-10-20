# Description

Closes #22

Add a deterministic property-style test for the rolling-window invariant in SPEC §3.1. It compares the production ledger against an independently implemented `std::Vec` reference model.

### Changes
- Model pruning, same-second coalescing, and bounded merge-forward independently of production code.
- Exercise fixed-seed traces containing timestamp advances, admitted transfers, and rejected transfers. A failure reports its seed and operation index for reproduction.
- Cover expiry and coalescing with short traces, plus an 8,300-operation stress trace that crosses `MAX_WINDOW_ENTRIES` and checks merge-forward behavior.
- Update [docs/audit-pack.md](docs/audit-pack.md) to record this as partial property-suite evidence for issue #6. Broader randomized policy/context coverage remains outstanding.

### Test workload
The test is included in the normal `cargo test` suite with no ignored test cases. It performs a bounded 10,348 generated operations: four 512-operation traces and one 8,300-operation merge stress trace.

### Validation
- `git diff --check` passes.
- Rust formatting, Clippy, and test-suite commands could not be run locally because `cargo`/`rustc` are unavailable in the environment.
