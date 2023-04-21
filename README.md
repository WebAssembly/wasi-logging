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
  - [Logging use case](#logging-use-case)
  - [Stderr use case](#stderr-use-case)
- [Detailed design discussion](#detailed-design-discussion)
  - [What levels should there be?](#what-levels-should-there-be)
- [Stakeholder Interest & Feedback](#stakeholder-interest--feedback)
- [References & acknowledgements](#references--acknowledgements)

### Introduction

WASI Logging is a WASI API for emitting log messages.

### Goals

The primary goal of WASI logging is to be a simple logging API usable
as a stderr destination in commands and as a logging output in headless
programs.

### Non-goals

WASI Logging is not aiming to be a general-purpose output stream, with
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

The log levels are similar to those of [log4j], the [Rust log crate], the
[Python log levels], the [Ruby log levels], the [.NET log levels], the
[Go zap library log levels], and the [Go zerolog library levels].

Another similar API is the POSIX `syslog` function. `LOG_EMERG` and `LOG_ALERT`
have no corresponding levels, because WASI programs don't have visibility into
how their own errors affect "the system" as a whole. A `Critical` level should
be used instead, optionally with a trap if it's desirable to halt execution.
Similarly, `LOG_NOTICE` and `LOG_INFO` both correspond to `Info`, because most
of the popular systems don't make a distinction between these levels.

[log4j]: https://logging.apache.org/log4j/2.x/manual/customloglevels.html
[Rust log crate]: https://docs.rs/log/latest/log/enum.Level.html
[Python log levels]: https://docs.python.org/3/library/logging.html#levels
[Ruby log levels]: https://ruby-doc.org/stdlib-2.4.0/libdoc/logger/rdoc/Logger.html
[.NET log levels]: https://docs.microsoft.com/en-us/dotnet/core/extensions/logging?tabs=command-line#log-level
[Go zap library log levels]: https://pkg.go.dev/go.uber.org/zap/zapcore#Level
[Go zerolog library levels]: https://github.com/rs/zerolog#leveled-logging

### What should the context be?

Currently the context parameter is an uninterpreted string, because it's the
simplest thing that works for now. It may evolve into something else though.

### Stakeholder Interest & Feedback

TODO before entering Phase 3.

### References & acknowledgements

Many thanks for valuable feedback and advice from:

- Luke Wagner
