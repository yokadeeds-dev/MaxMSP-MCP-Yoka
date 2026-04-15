# MaxMSP-MCP-Yoka

A Max/MSP MCP server for LLM-driven patch creation and control — built on top of the open-source [MaxMSP-MCP-Server](https://github.com/tiianhk/MaxMSP-MCE-Server) by tiianhk, extended and restructured as the foundation of a larger AI-to-Max framework.

> **Status:** The core MCP tools work out of the box for basic patch manipulation. The architecture is actively being rebuilt and extended — the full framework layer is what enables reliable, intelligent operation across complex, multi-patch setups.

---

## What this does

This MCP server lets LLMs (like Claude) interact directly with a running Max 9 session: create and connect objects, inspect patches, read documentation, send messages and bangs — all through natural language.

### Current tools
- Add, remove, and connect Max objects in a live patch
- Get and set object attributes and parameters
- Look up official Max documentation per object
- Send bangs and messages to objects
- Inspect patch contents and subpatch windows

---

## Why a fork?

The original server is a clean proof-of-concept for simple, single-patch demos. This fork extends it with stability improvements and prepares the architecture for the framework:

- **Resilient startup** — the MCP server connects to Claude Desktop even when Max is not yet running; individual tool calls fail gracefully instead of crashing the server
- **Improved error handling** — lifespan management and connection recovery
- **Framework-ready structure** — the codebase is being restructured to support the full AI-to-Max workflow described below

---

## The bigger picture: AI-to-Max Framework

This server is the entry point for a framework currently under development. The framework is what makes the system reliable and musically intelligent for **complex setups** — things the raw MCP alone cannot handle:

- Multi-patch sessions with interdependent synthesis modules
- Generative FM architectures (like the Posford Machine) with real-time parameter control
- AI-assisted composition with MIDI, audio routing, and modular signal flow
- Intelligent patch generation from high-level musical descriptions

### What the framework adds (roadmap)

- **Patch context awareness** — understanding the full signal graph, not just individual objects
- **Semantic object relationships** — knowing how modules connect musically, not just technically
- **Multi-agent coordination** — specialized agents for synthesis, effects, routing, and performance
- **State memory** — persistent knowledge of patch configurations and session history
- **Complex setup support** — reliable operation across multi-window, multi-instrument, live-performance environments

---

## Installation

### Prerequisites

- Python 3.8 or newer
- Max 9 or newer
- Claude Desktop (or any MCP-compatible client)

### Setup

**1. Clone this repository:**
```
git clone https://github.com/yokadeeds-dev/MaxMSP-MCP-Yoka.git
cd MaxMSP-MCP-Yoka
```

**2. Create a virtual environment and install dependencies:**
```
python -m venv .venv

# Windows:
.venv\Scripts\activate
# macOS / Linux:
source .venv/bin/activate

pip install -r requirements.txt
```

**3. Add to your Claude Desktop config** (`claude_desktop_config.json`):
```json
"MaxMSPMCP": {
  "command": "C:\\path\\to\\MaxMSP-MCP-Yoka\\.venv\\Scripts\\mcp.exe",
  "args": ["run", "C:\\path\\to\\MaxMSP-MCP-Yoka\\server.py"],
  "env": {
    "VIRTUAL_ENV": "C:\\path\\to\\MaxMSP-MCP-Yoka\\.venv",
    "PATH": "C:\\path\\to\\MaxMSP-MCP-Yoka\\.venv\\Scripts"
  }
}
```

**4. Open the Max companion patch** from `MaxMSP_Agent/demo.maxpat`:
- In the first tab, click `script npm version` to verify npm is installed
- Click `script npm install` to install dependencies
- Switch to the second tab and click `script start` to initiate the Socket.IO connection

**5. Restart Claude Desktop** — the MaxMSP tools will appear automatically.

---

## Demo

### Understand: LLM Explaining a Max Patch

![img](./assets/understand.gif)

[Video link](https://www.youtube.com/watch?v=YKXq566zrec). Acknowledgement: the patch being explained is downloaded from [here](https://github.com/jeffThompson/MaxMSP_TeachingSketches/blob/master/02_MSP/07%20Ring%20Modulation.maxpat). Text comments in the original file are deleted.

### Generate: LLM Making an FM Synth

![img](./assets/generate.gif)

Check out the [full video](https://www.youtube.com/watch?v=Ns89YuE5-to) to listen to the synthesized sounds.

---

## Credits

Based on [MaxMSP-MCP-Server](https://github.com/tiianhk/MaxMSP-MCE-Server) by tiianhk. Extended and maintained as part of the Yoka AI-to-Max framework.

## Disclaimer

This is a third party implementation and not made by Cycling '74.
