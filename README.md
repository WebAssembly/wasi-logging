# WASI Logging

A proposed [WebAssembly System Interface](https://github.com/WebAssembly/WASI) API.

### Current Phase

WASI-logging is currently in [Phase 1].

[Phase 1]: https://github.com/WebAssembly/WASI/blob/42fe2a3ca159011b23099c3d10b5b1d9aff2140e/docs/Proposals.md#phase-1---proposed-spec-text-available-cg--wg

### Champions

- Dan Gohman

### Phase 4 Advancement Criteria

The Phase 4 Adancement Criteria for this API are not yet defined.

## Table of Contents

- [Introduction](#introduction)
- [Goals](#goals)
- [Non-goals](#non-goals)
- [API walk-through](#api-walk-through)
  - [Use case 1](#use-case-1)
  - [Use case 2](#use-case-2)
- [Detailed design discussion](#detailed-design-discussion)
  - [[Tricky design choice 1]](#tricky-design-choice-1)
  - [[Tricky design choice 2]](#tricky-design-choice-2)
- [Considered alternatives](#considered-alternatives)
  - [[Alternative 1]](#alternative-1)
  - [[Alternative 2]](#alternative-2)
- [Stakeholder Interest & Feedback](#stakeholder-interest--feedback)
- [References & acknowledgements](#references--acknowledgements)

### Introduction

WASI Logging is a WASI API for emitting log messages.

### Goals

The primary goal of WASI logging is to be a simple logging API usable
as a stderr destination in commands and as a logging output in headless
programs.

### Non-goals

WASI Clocks is not aiming to be a general-purpose output stream, with
support for error reporting or asynchronous operation.

### API walk-through

There are two main use cases.

#### Logging use case

The logging API can be used to log simple messages:

```
   log(Level::Info, "fyi", "The program is running");
```

#### Stderr use case

The logging API can be used as an output for a command-style stderr.

```
   log(Level::Info, "stderr", "Message printed to stderr in a command");
```

### Detailed design discussion

### What levels should there be?

The log levels are similar to those of [log4j] and the [Rust log crate].

It excludes log4j's `FATAL` level. The recommended behavior on a `FATAL` error
is to emit an `Error`-level error and to trap.

Another similar API is the POSIX `syslog` function. `LOG_EMERG`, `LOG_ALERT`,
and `LOG_CRIT` have no corresponding level, because WASI programs don't have
visibility into how their own errors affect "the system" as a whole. A plain
`Error` level should be used, optionally with a trap if it's desirable to
halt execution. And `LOG_NOTICE` and `LOG_INFO` both correspond to `Info`,
because other popular systems don't make a distinction between these levels.

[log4j]: https://logging.apache.org/log4j/2.x/manual/customloglevels.html
[Rust log crate]: https://docs.rs/log/latest/log/enum.Level.html

### What should the context be?

Currently the context parameter is an uninterpreted string, because it's the
simplest thing that works for now. It may evolve into something else though.

### Stakeholder Interest & Feedback

TODO before entering Phase 3.

[This should include a list of implementers who have expressed interest in implementing the proposal]

### References & acknowledgements

Many thanks for valuable feedback and advice from:

- Luke Wagner
