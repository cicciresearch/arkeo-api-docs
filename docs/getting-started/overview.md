# API Overview

The **Arkeo All-in-One API** provides programmatic access to the ARKEO measurement
application, enabling **automation, remote control, and integration** with
external software such as LabVIEW, Python, MATLAB, or custom test frameworks.

The API is designed for laboratory and research environments where measurements
must be scripted, repeated, synchronized with external instruments, or
integrated into larger experimental workflows.

This page introduces the **core concepts and architecture** of the API before
diving into command details.

---

## What the API is (and is not)

The API is a **control and query interface** to a running ARKEO application.

It allows you to:
- Start, stop, and configure measurements
- Control measurement routines programmatically
- Read back state, status, and results
- Coordinate ARKEO with external hardware or software

It does **not**:
- Replace the ARKEO graphical user interface
- Perform measurements on its own
- Bypass ARKEO’s internal safety checks and limits

The API always acts **through** the ARKEO application.

---

## Typical use cases

The API is commonly used for:

- **Automated testing**
  - Batch measurements
  - Parameter sweeps
  - Long-term stability experiments

- **Integration**
  - Synchronization with environmental chambers
  - Coordination with optical setups or external SMUs
  - Data pipelines and FAIR data workflows

- **Remote control**
  - Headless operation
  - Network-based experiment orchestration

---

## Architecture overview

At a high level, the system consists of three parts:

+-------------------+ TCP / JSON +---------------------+
| External client | <-------------------> | ARKEO application |
| (Python, LV, etc) | | (API server) |
+-------------------+ +---------------------+


- **ARKEO application**
  - Runs locally on the measurement PC
  - Owns all hardware connections
  - Executes measurements and routines
  - Exposes a TCP server for API access

- **External clients**
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

- **MAIN** - Application-level control and global state  
- **ROUTINE** - Measurement routines (JV, tracking, impedance, etc.)  
- **TMPCTL** - Temperature controllers and thermal environments  
- **MUX** - Multiplexer configuration and channel routing  

Targets provide a clear separation between **what** you control and **how** it
is controlled.

---

### Commands

Each target exposes a set of **commands**.

A command:
- Performs an action (e.g. start a routine)
- Changes a configuration
- Queries the current state

Commands are always explicit and deterministic:  
the same command with the same parameters produces the same effect, provided
the system state allows it.

---

### Parameters

Commands may accept **parameters** that define their behavior.

Examples:
- Voltage limits
- Measurement settings
- Channel indices
- Setpoints or modes

Parameters are always provided as structured JSON objects and are validated by
ARKEO before execution.

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

This makes the API suitable for **robust automation and error handling**.

---

## Measurement workflow (high level)

A typical automated measurement sequence looks like this:

1. Connect to the ARKEO API server
2. Configure channels, routines, and settings
3. Select and configure a measurement routine
4. Start the routine
5. Monitor status and progress
6. Stop or finalize the measurement
7. Retrieve or post-process generated data

The exact commands depend on the routine and target involved, but this logical
flow remains consistent.

---

## Relationship to ARKEO software concepts

The API mirrors the same concepts used in the ARKEO user interface:

- **Routines** correspond to measurement tools available in the GUI
- **Channels** map to configured electrical paths and devices
- **Sensors and environments** reflect ARKEO’s internal monitoring systems
- **Settings** use the same parameter names and meanings as the GUI

This ensures that:
- API usage matches documented software behavior
- Scripts remain compatible with manual operation
- Results are consistent across automated and interactive workflows

---

## How this documentation is organized

This documentation is structured around the API architecture:

- **Overview** - Concepts and architecture (this page)
- **Target sections** - One section per target (MAIN, ROUTINE, TMPCTL, MUX)
- **Command references** - Detailed command descriptions and parameters
- **Examples** - Practical command sequences and workflows

You can read the documentation linearly or jump directly to the target you need.

---

## Next steps

If this is your first time using the API:

1. Start with the **MAIN** target to understand application-level control
2. Explore **ROUTINE** to automate measurements
3. Use **TMPCTL** and **MUX** when integrating hardware and environments

Each target section includes:
- Available commands
- Required and optional parameters
- Expected responses
- Notes on behavior and constraints

---
