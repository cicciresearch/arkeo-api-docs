# API Overview

The **Arkeo All-in-One API** provides programmatic access to the ARKEO measurement
application, enabling **automation, remote control, and integration** with
external software such as LabVIEW, Python, MATLAB, or custom test frameworks.

The API is designed for laboratory and research environments where measurements
must be scripted, repeated, synchronized with external instruments, or
integrated into larger experimental workflows.

This page introduces the core concepts and architecture of the API before
diving into command details.

---

## What the API is (and is not)

The API is a **control and query interface** to a running ARKEO application.

It allows you to:

- Start, stop, and configure measurements
- Control measurement routines programmatically
- Read back state, status, and results
- Coordinate ARKEO with external hardware or software

It does not

- Replace the ARKEO graphical user interface
- Add funtions that cannot be accessed by the user interface
- Perform measurements on its own
- Bypass ARKEO’s internal safety checks and limits

The API always acts through the ARKEO application.

---

## Architecture overview

At a high level, the system consists of two parts:

**ARKEO application**

  - Runs locally on the measurement PC
  - Owns all hardware connections
  - Executes measurements and routines
  - Exposes a TCP server for API access

**External clients**

  - Connect over TCP
  - Send JSON-encoded commands
  - Receive structured JSON responses

Multiple clients may connect, but **measurement state is global** and managed
by ARKEO.

---

## Core API concepts

### Targets

Every API command is addressed to a **target**.
A target represents a logical subsystem inside ARKEO.

Main targets include:

- [**MAIN**](../main/index.md) - Application-level control and global state  
- [**ROUTINE**](../routine/index.md) - Measurement routines (JV, tracking, impedance, etc.)  
- [**TMPCTL**](../tmpctl/index.md) - Temperature controllers and thermal environments  
- [**MUX**](../mux/index.md) - Multiplexer configuration and channel routing  

Targets provide a clear separation between **what** you control and **how** it
is controlled.

---

### Commands

Each target exposes a set of **commands**.

A command:

- Performs an action (e.g. start a routine)
- Changes a configuration
- Queries the current state

Commands are always explicit and deterministic: the same command with the same parameters produces the same effect, provided the system state allows it. Every command returns a response. New commands **should not** be send before a response is received.

---

### Parameters

Commands may accept **parameters** that define their behavior.

Examples:

- Routine name
- Measurement settings
- Channel indices
- Setpoints or modes

Parameters are always provided as structured JSON objects and are validated by ARKEO before execution. If an unknown or wrong parameter is send, the command is ignored and an error object is returned.

---

### Requests and responses (conceptual)

All communication follows a **request → response** pattern:

- The client sends a request
- ARKEO processes it
- ARKEO returns a response indicating success or failure

Responses always include:

- Execution status
- Optional data payload
- Error information if something went wrong

---

## Measurement workflow (high level)

A typical automated measurement sequence looks like this:

1. Connect to the ARKEO API server
2. Send a StartRoutine command
3. Wait until the routine finished initializing by polling the GetTestStatus command
4. Apply the correct settings with the ApplySettings command
5. (optional) use any custom commands if required by the routine
6. Start the measurement with the StartMeasurement command
7. Monitor status and progress with the GetTestStatus and GetTestData command
8. Retrieve or post-process generated data

The exact commands depend on the routine and target involved, but this logical
flow remains consistent.

---
## Next steps

If this is your first time using the API:

1. Start with the [**MAIN**](../main/index.md) target to understand application-level control
2. Explore [**ROUTINE**](../routine/index.md) to automate measurements
3. Use [**TMPCTL**](../tmpctl/index.md) and [**MUX**](../mux/index.md) when integrating hardware and environments

Each target section includes:
- Available commands
- Required and optional parameters
- Expected responses
- Notes on behavior and constraints

---
