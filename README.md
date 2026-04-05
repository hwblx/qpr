# qpr - Quick PlantUML Renderer

`qpr` is a lightweight bash script that renders PlantUML diagrams using Docker. It simplifies the process of generating SVG or PNG diagrams from the terminal without requiring a local Java or PlantUML installation. Diagrams can also be displayed directly in graphics-capable terminals (currently supporting Kitty).

## Features

- **Docker-powered**: No local dependencies other than Docker. The script will prompt to pull the `plantuml/plantuml` image if it's not found locally.
- **SVG & PNG Support**: Default output is SVG, with an option for PNG.
- **Batch Rendering**: Supports multiple files or filename prefixes.
- **Terminal Preview**: Integration with Kitty terminal (`kitten icat`) to display diagrams directly in your terminal.
- **Smart Path Handling**: Automatically resolves relative paths for Docker volume mounting.

## Templates

The repository includes a `templates/` directory with starter files that you can copy and modify for your own projects:
- **C4 Model**: Templates for System Context (C1), Container (C2), Component (C3), and Code (C4) diagrams using the [C4-PlantUML](https://github.com/plantuml-stdlib/C4-PlantUML) library.

## Prerequisites

- [Docker](https://www.docker.com/)
- (Optional) [Kitty Terminal](https://sw.kovidgoyal.net/kitty/) for the `--print` feature.

## Installation

1. Download the `qpr` script.
2. Make it executable:
   ```bash
   chmod +x qpr
   ```
3. Move it to a directory in your `PATH` (e.g., `~/.local/bin` or `/usr/local/bin`).

## Usage

`qpr` accepts both full filenames and filename prefixes. If a prefix is provided, it will render all matching `.puml` files.

```bash
qpr [options] <prefix-or-filename>...
```

### Options

- `--png`          Output PNG instead of the default SVG.
- `--print`        Display the resulting PNG in the terminal (requires Kitty terminal). Implies the `--png` flag.
- `-q, --quiet`    Suppress status messages.
- `-h, --help`     Show help message.

### Examples

Render a specific `.puml` file to SVG:
```bash
qpr diagram.puml
```

Render all `.puml` files starting with the prefix "c" to PNG and preview them in the terminal:
```bash
qpr --print c
```

## License

MIT
