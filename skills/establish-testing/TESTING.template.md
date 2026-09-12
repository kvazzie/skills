# Testing

<!-- Keep this table first. Add one row per adopted test type. -->

## Quick reference

| Test type | Use when | Framework | Location and naming | Command |
| --- | --- | --- | --- | --- |
| `<type>` | `<behavioral boundary>` | `<runner>` | `<directory>/<pattern>` | `<command>` |

## Choosing a test type

Explain how to choose among the adopted test types. Define the boundary each type owns and the behavior it should leave to another type.

## Layout and naming

State whether tests are colocated or separate. Give exact directories, filename patterns, and the rules for shared test support files.

## Test style

Describe the expected structure of a test and the project's conventions for assertions, fixtures, mocks, shared helpers, setup, and cleanup. Use small examples only when prose would leave the rule ambiguous.

## Commands

| Purpose | Command |
| --- | --- |
| Full suite | `<command>` |
| One test type | `<command>` |
| One file | `<command>` |
| One case | `<command>` |

Document watch mode and coverage only when they apply.

## Dependencies and configuration

Name the test dependencies the project has adopted, where their configuration lives, and the rule for adding or changing them.

## CI

State which test commands CI runs and which results are required. If CI testing has not been adopted, say so directly.

## Disposable diagnostics

Keep one-off diagnostic probes outside the repository or in an ignored temporary location, and remove them after use. Any behavior check retained in the repository is a test and follows this document.
