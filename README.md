# README — Zerodays Patch // Global Cross-Conn Monitor

**Version:** 2.4.1  
**Status:** Secure Connection / Online  
**Developer:** Zorathedev00 Ai  

This application is a high-performance, real-time network monitoring dashboard designed for deep packet inspection, global traffic analysis, and live data interception simulation. It functions as a "Zero-Day" style cross-connection monitor, tracking bandwidth utilization across multiple active nodes and services globally.

## 🎯 Overview

The **Zerodays Patch v2.4.1** provides a comprehensive interface to visualize:
*   **Live Bandwidth Utilization**: Real-time graphs showing incoming vs outgoing traffic rates (MB/s).
*   **Global Data Matrix & Node Status**: A dynamic grid representing active connections from various countries with simulated latency/traffic states.
*   **Deep Packet Inspection (DPI)**: Filters by Source IP, Destination IP, Protocol, and Service for detailed network flow analysis.
*   **WhatsApp Live Intercept Simulation**: Displays random geolocation data, E.164 phone numbers, connection types, and sync times in real-time.
*   **Keylogger Capture**: Captures simulated keystrokes with timestamps, PID tracking, and scrollable history (with auto-trimming to maintain performance).
*   **System Logs & Export**: Stores up to 500 events and supports CSV export of logs including time, location, target ID, connection type, and traffic volume.

---

## 🚀 Quick Start Guide

### 1. Launching the Interface
The application operates as a Progressive Web App (PWA) or standalone dashboard. It is designed to run inside a browser window (`window.close()` available via header button).

**Access Point:**  
[http://trymetools.ultimatetool.2bd.net/](http://trymetools.ultimatetool.2bd.net/)  

*(Note: If direct access fails due to DNS/Parsing issues like `panel.hidden` or `matrix-cell`, use the primary URL above as it encapsulates all runtime assets including the JavaScript engine and CSS logic.)*

### 2. Navigation & Tabs
Use the top toolbar buttons to switch between operational modes instantly:

*   **🏠 Overview**: The main dashboard showing live traffic stats, global node status (Matrix), active services, and real-time WhatsApp intercept data.
*   **🔍 Inspect**: Opens a filtered packet inspection table where you can monitor specific IPs or protocols in detail.
*   **🔔 Notif**: Displays a queue of system notifications (e.g., threshold alerts, unknown IP detections).
*   **📋 Logs**: Shows the scrollable history of intercepted events with export options (CSV Download / Clear All).
*   **⚙️ Settings**: Allows configuration updates for dark mode toggles, update intervals, and log verbosity levels.

---

## 🛠 Functional Modules & Details

### A. Traffic Analysis Engine
Located in the "Overview" tab under `stats-graph-layout`:
*   **Interface Detection**: Automatically identifies the active network adapter (`en0`, etc.) via `navigator.connection`.
*   **Dynamic Rate Calculation**: Adjusts simulation base rates based on actual connection type:
    *   4G/5G/Wi-Fi6 → Base rate ~5 MB/s (simulated spikes).
    *   3G → Reduced to ~1.5 MB/s.
    *   2G/GPRS → Reduced further.
*   **Visualization**: Renders smooth, animated line graphs for INCOMING and OUTGOING traffic using HTML5 Canvas with gradient fills and real-time resizing support.

### B. Global Cross-Conn Monitor (Matrix & Map)
Located in the "Overview" tab under `vis-grid`:
*   **Global Data Matrix**: Generates a grid of randomly selected country codes paired with unique session IDs (`#XXXXX`). Each cell toggles between `CONN` (Active/Online) and `WAIT` states, simulating live heartbeat signals from remote nodes.
*   **Node Status Grid**: Represents ~195 active global nodes. Nodes pulse visually when active and dim when idle, providing an at-a-glance map of network health across countries like US, RU, DE, JP, etc.

### C. Deep Packet Inspection (DPI) Module
Located in the "Inspect" tab:
*   **Data Sources**: Populated by a simulated packet buffer containing 200+ random entries with realistic IP ranges (`192.168.x.x`, `8.8.8.8`, etc.).
*   **Filtering Capabilities**: Supports real-time filtering by text input fields for:
    *   Source IP Address
    *   Destination IP Address
    *   Protocol Type (TCP/UDP/IPIC)
    *   Service Name (e.g., HTTPS, HTTP, SSH)
*   **Output Format**: Displays source/dest IPs in monospace font with port numbers and byte counts aligned strictly to the table structure.

### D. WhatsApp Live Intercept & Keylogger
Located at the bottom of the "Overview" tab (`bottom-grid`):
*   **WhatsApp Section**: Simulates a live feed showing location coordinates (randomly generated from country lists), E.164 phone format numbers, connection types (5G/Wi-Fi 6), and last synchronization timestamps.
*   **Keylogger Capture Box**: A scrollable text area that logs simulated keystrokes every ~150ms. Includes:
    *   Timestamps (`[HH:MM:SS]`)
    *   Keypress codes (e.g., `Enter`, `Space`, alphanumeric keys)
    *   Process IDs (PIDs) for simulation granularity.
    *   Auto-trimming mechanism to keep DOM size under 3KB of text content before resetting scroll position.

---

## 📊 Data Simulation Logic

The application uses a state-based JavaScript object model (`const state = { ... }`) to manage runtime data without backend dependencies. All visualizations update via `setInterval` loops at fixed intervals (1000ms for core data, 150ms for fast events like keylogging).

### Core State Variables:
*   **Traffic**: Tracks cumulative MB transferred and per-second rates stored in arrays `in[]`, `out[]`.
*   **Packets**: A buffer holding up to 200 simulated network packets for inspection tables.
*   **Logs**: Stores the last 500 events for exportable CSV reports.
*   **Notifications**: Manages a dynamic list of alert popups triggered by random probability checks (`Math.random() > 0.98`).

---

## 💾 Data Sources & Export Formats

### Logs Table (CSV Structure)
When exporting via "⬇ CSV Export", the data follows this exact format:
```csv
Time,Location,Phone,Connection,Traffic
14:32:10,"Kabul, AF",+93 76543210,5G,12.45 MB
```

### Inspect Table (JSON/HTML Compatible)
Rows are constructed with monospace fonts and color-coded borders for readability in terminal-style views. Supports slicing operations to prevent UI lag during high-traffic simulations.

---

## ⚙️ Configuration Options

In **Settings** tab (`tab-settings`), users can adjust:
*   **Dark Mode**: Enabled by default; toggles background contrast between `#0f172a` and `#eab308`.
*   **Update Interval**: Default set to 1000ms for smooth animation frames.
*   **Log Level**: Adjustable via dropdown options (Debug, Info, Warning) though currently primarily affects console output verbosity or internal trace flags.

### Reset Functionality
A dedicated "🔄" button in the header resets all traffic counters, clears graph history, and flushes packet buffers immediately without restarting the session.

---

## 🖥 Display & Responsiveness

The interface uses CSS Grid (`grid-template-columns: repeat(auto-fill, ...)`) and Flexbox layouts that adapt dynamically:
*   **Desktop (>900px)**: Displays panels in a complex 2-column grid with side-by-side statistics and maps.
*   **Mobile (<900px)**: Collapses into single-column stacks where graphs move vertically above the matrix, ensuring touch-friendly interaction on smaller screens.

Scrollbars are customized globally to minimize visual clutter while maintaining accessibility for log-heavy sections like `logsBody` or `keylogBox`.

---

**Footer Info:**  
*zerodays patch v2.4.1 // Secure Connection*  
*Designed/build by Zorathedev00 Ai*
