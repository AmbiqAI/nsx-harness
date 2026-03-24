# nsx-harness

`nsx-harness` provides lightweight runtime helpers used by NSX applications for
printing, debug log forwarding, and optional profiling integration.

Contents:
- AmbiqSuite-oriented print and logging helpers
- TFLM debug-log bridge and micro-profiler support
- public headers in `includes-api/`
- regression tests carried forward from the migration baseline

This module is CMake-first and intended to be consumed through `nsx create-app`
or vendored module workflows.
