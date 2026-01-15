# Arkeo All-in-One API Documentation

The Arkeo All-in-One API allows external applications to control and query the Arkeo measurement software. Communication happens using the TCP protocol on port 6360, enabling users to perform a variety of commands manage measurements. Each connected client can send JSON-encoded requests and receive JSON responses.

---

## API Modules

The API is divided in 4 section, each controlling a specific part of the software.

<div class="grid cards" markdown>

-   :material-cog-outline: **MAIN** - **System-level control**

    Manage application state, connections, and global operations such as routine selection and execution.

    ---
    [:octicons-arrow-right-24: Explore MAIN](main/index.md)

-   :material-chart-line: **ROUTINE** - **Measurement routines**

    Configure and run measurement workflows such as JV scans, MPPT, impedance spectroscopy, and luminescence measurements.

    ---
    [:octicons-arrow-right-24: Explore ROUTINE](routine/index.md)

-   :material-thermometer: **TMPCTL** - **Temperature control**

    Monitor and control temperature controllers, setpoints, ramps, and stabilization status.

    ---
    [:octicons-arrow-right-24: Explore TMPCTL](tmpctl/index.md)

-   :material-call-split: **MUX** - **Multiplexer management**

    Configure and control hardware multiplexers for channel routing and device selection.

    ---
    [:octicons-arrow-right-24: Explore MUX](mux/index.md)

</div>

---

## Getting started

If this is your first time using the API, start here:

- 📘 **[API overview & protocol](getting-started/overview.md)**
- 🔧 **[Request & response format](getting-started/protocol.md)**
- 🧪 **[Example JSON commands](getting-started/examples.md)**

---

## Connection details

- **Protocol**: TCP
- **Port**: `6360`
- **Message format**: JSON (length-prefixed)

The API is designed to be language-agnostic and can be used from LabVIEW, Python, MATLAB, C/C++, or any TCP-capable environment.
