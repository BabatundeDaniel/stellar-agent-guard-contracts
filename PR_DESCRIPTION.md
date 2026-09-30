# Description

Closes #22

Adds a deterministic property-style test for the rolling-window invariant in SPEC §3.1, comparing the production ledger to an independent `std::Vec` reference model.

### Changes
- **Reference model:** Independently models pruning, same-second coalescing, bounded merge-forward, and total updates.
- **Generated traces:** Fixed-seed traces mix timestamp advances, admissions, and rejected operations. Failures report the seed and operation index for exact reproduction.
- **Boundary coverage:** Short traces exercise expiry/coalescing; a bounded 8,300-operation stress trace crosses `MAX_WINDOW_ENTRIES` and checks merge-forward results.
- **Audit pack:** Updated [docs/audit-pack.md](docs/audit-pack.md) to record this as partial property-suite evidence for #6; randomized policy/context coverage remains outstanding.

### Workload and validation
- The test is not ignored and runs under `cargo test`. Its generated workload is bounded to 10,348 operations (four 512-operation traces and one 8,300-operation stress trace).
- [ ] `cargo fmt --check`, `cargo clippy --all-targets --all-features`, and `cargo test` pass locally.
- [x] PR description references the issue (`Closes #22`).
