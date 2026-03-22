I have updated the **Code Quality** section of the README to reflect the reality of decompiling a C++ engine like Rayne. It differentiates between the "High Quality" recovery of assets and the "Low Quality" (but still useful) recovery of the game's logic.

---

# RayneDecompiler

**RayneDecompiler** is a specialized reverse-engineering toolkit designed to analyze and deconstruct games built on the [Rayne Engine](https://github.com/uberpixel/Rayne). Since Rayne is a high-performance C++ engine, this tool focuses on bridging the gap between raw machine code and the engine's original class structures.

## Features

* **Header Mapping:** Automatically correlates Rayne's C++ class definitions (e.g., `RN::Entity`, `RN::Scene`) with binary offsets.
* **Asset Extraction:** Unpacks custom Rayne asset formats like `.rq` (models) and texture blobs.
* **Shader Recovery:** Decompiles SPIR-V/DXIL shader binaries found in APK `assets/` back into readable HLSL/GLSL.
* **Ghidra Integration:** Includes scripts to auto-label engine-specific functions within a disassembled `.so` or `.exe`.

---

## Decompilation Quality Standards

The quality of the output depends on which part of the Rayne project is being targeted. This tool categorizes output into three levels:

### 1. High-Fidelity Recovery (Assets & Shaders)
* **Code Quality:** **High.**
* **Description:** Because Rayne's asset loading logic is open-source, we can mirror the serialization exactly. Models, textures, and scene hierarchies are recovered with nearly 100% accuracy. Shaders are translated back into readable HLSL/GLSL using SPIRV-Cross, maintaining original logic flow.
* **Output:** Ready-to-use files for a fresh Rayne project.

### 2. Medium-Fidelity Recovery (Engine Calls)
* **Code Quality:** **Medium.**
* **Description:** By importing Rayne's C++ headers into a disassembler, we can identify internal engine calls (e.g., `RN::Renderer::Render()`). 
* **Output:** Assembly code with descriptive labels, making it clear where the engine ends and the game logic begins.

### 3. Low-Fidelity Recovery (Game Logic)
* **Code Quality:** **Low (Pseudocode).**
* **Description:** Game-specific logic (player movement, AI, UI handling) is compiled into machine code. Decompiling this results in "Pseudocode"—functional C code that lacks original variable names and comments.
* **Output:** Logic-accurate but human-difficult code (e.g., `if(a > 10)` instead of `if(playerHealth > 10)`).

---

## Implementation Standards

To ensure the decompiler remains robust as the Rayne Engine evolves:

* **Zero-Inference Parsing:** The tool never "guesses" data structures. Every parser is grounded in the official Rayne source code.
* **Reference Tagging:** Every decompilation script includes a comment pointing to the specific file in the `uberpixel/Rayne` repository that it targets.
* **Modular Architecture:** Asset parsers are isolated from the core binary disassembler to allow for easy updates when the `.rq` or `.rnb` formats change.

---

## Getting Started

### Prerequisites
Soon
