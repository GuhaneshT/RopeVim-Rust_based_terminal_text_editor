# 🪢 Rope-Based Text Editor

> A lightweight, terminal-based text editor written in Rust — built around a rope data structure for efficient text manipulation.

![Rust](https://img.shields.io/badge/Rust-1.65%2B-orange?style=flat-square&logo=rust)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey?style=flat-square)
![Build](https://img.shields.io/badge/Build-cargo-red?style=flat-square)

---

## Overview

The Rope-Based Text Editor is a minimal, keyboard-driven terminal editor that focuses on correctness, performance, and simplicity. Instead of storing text as a single contiguous string, it uses a **rope data structure** — a binary tree of string slices — which makes insertions, deletions, and edits significantly more efficient, especially on large files.

This project is both a fully usable editor and an exploration of how editors work under the hood, built with Rust's strong systems programming ecosystem.

---

## Why Rope?

Traditional text editors often back their buffers with plain strings or gap buffers, which can degrade with repeated insertions or deletions — particularly in large files. A rope avoids this:

| Operation | String / Array | Rope |
|-----------|---------------|------|
| Insert at middle | O(n) — shifts memory | O(log n) |
| Delete at middle | O(n) — shifts memory | O(log n) |
| Split / join | O(n) | O(log n) |
| Random access | O(1) | O(log n) |

For a text editor doing hundreds of edits per session, these properties add up — especially as file sizes grow.

---

## Features

- **Rope-backed buffer** — efficient insert, delete, and undo operations at any position
- **Undo / Redo** — full history of editing actions, accessible via keyboard
- **Custom filename** — set the output filename interactively during the session
- **Interactive help menu** — in-editor keybinding reference, accessible at any time
- **Cross-platform** — runs on Windows, macOS, and Linux via `crossterm`
- **Keyboard-driven workflow** — no mouse required
- **Minimal dependencies** — just `crossterm` and `ropey`

---

## Tech Stack

| Crate | Purpose |
|-------|---------|
| [`ropey`](https://crates.io/crates/ropey) | Rope data structure for text storage and manipulation |
| [`crossterm`](https://crates.io/crates/crossterm) | Cross-platform terminal rendering, cursor control, and keyboard input |

---

## Installation

### Prerequisites

- [Rust](https://rustup.rs/) (stable, 1.65 or later)
- A terminal emulator
- Git (optional, for cloning)

### Clone and Build

```bash
git clone https://github.com/username/rope-text-editor.git
cd rope-text-editor
cargo build --release
```

### Run

```bash
cargo run --release
```

Or invoke the compiled binary directly:

```bash
./target/release/rope-text-editor
```

---

## Usage

### Launching the Editor

```bash
cargo run --release
```

The editor opens a blank buffer in your terminal. Start typing immediately.

### Editing Text

- Type any characters to insert text at the cursor
- Use **←** and **→** arrow keys to move the cursor
- Press **Enter** to insert a new line
- Press **Backspace** to delete the character before the cursor

### Help Menu

Press **Ctrl+M** to open the in-editor help menu, which displays all available keybindings. Press **Esc** to return to editing.

### Saving and Quitting

| Action | Keybinding |
|--------|-----------|
| Save the file | `Ctrl+S` |
| Set a custom filename | `Ctrl+X` |
| Quit the editor | `Ctrl+A` |

### Undo and Redo

| Action | Keybinding |
|--------|-----------|
| Undo | `Ctrl+Z` |
| Redo | `Ctrl+Y` |

---

## Keybindings

| Keybinding | Action |
|-----------|--------|
| `Ctrl+A` | Quit the editor |
| `Ctrl+S` | Save the current file |
| `Ctrl+X` | Set a custom filename |
| `Ctrl+M` | Open the help menu |
| `Ctrl+Z` | Undo last change |
| `Ctrl+Y` | Redo reverted change |
| `Backspace` | Delete character before cursor |
| `← / →` | Move cursor left / right |
| `Enter` | Insert a new line |
| `Esc` | Return from help menu to editor |

---

## Project Structure

```
rope-text-editor/
├── Cargo.toml
├── Cargo.lock
├── LICENSE
├── README.md
└── src/
    ├── main.rs        # Entry point and program startup
    ├── editor.rs      # Rope-based text storage, editing logic, key handling
    └── ui.rs          # Terminal rendering and interactive help menu
```

### Module Breakdown

**`src/main.rs`**
Entry point. Initialises the terminal, sets up the editor state, and runs the main event loop.

**`src/editor.rs`**
Core logic. Manages the rope buffer, handles cursor position, processes keyboard input, and implements undo/redo history.

**`src/ui.rs`**
Rendering layer. Draws the editor surface and the interactive help menu to the terminal using `crossterm`.

---

## Design Goals

This project was built with a clear set of intentions:

- Understand how text editors manage their internal buffers
- Explore the performance characteristics of rope-based text storage in Rust
- Build a minimal but genuinely usable terminal application
- Practice systems programming with real-world I/O and interaction patterns
- Create a solid foundation for future editor improvements

---

## Roadmap

Possible future enhancements, in rough order of priority:

- [ ] Vertical cursor movement (Up / Down arrow keys)
- [ ] Line numbers in the gutter
- [ ] File open on launch (`rope-text-editor <filename>`)
- [ ] Viewport scrolling for files larger than the terminal height
- [ ] Search and replace functionality
- [ ] Clipboard support (copy, cut, paste)
- [ ] Syntax highlighting for common languages
- [ ] Multiple buffer / split-pane support
- [ ] Configurable keybindings

---

## Contributing

Contributions are welcome. To get started:

1. Fork the repository
2. Create a new branch for your feature or fix:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Make your changes
4. Run the test suite:
   ```bash
   cargo test
   ```
5. Submit a pull request with a clear description of what changed and why

Please follow standard Rust conventions (`rustfmt`, `clippy`) and include tests where appropriate.

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Acknowledgements

- Inspired by classic terminal editors — [Vim](https://www.vim.org/) and [GNU Nano](https://www.nano-editor.org/)
- Built on the excellent [`ropey`](https://crates.io/crates/ropey) and [`crossterm`](https://crates.io/crates/crossterm) crates
- Motivated by the desire to understand what happens beneath the surface of every editor we use
