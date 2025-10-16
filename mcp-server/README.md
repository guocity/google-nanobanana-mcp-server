# Nano Banana MCP Server

[![npm version](https://badge.fury.io/js/nanobanana-mcp.svg)](https://www.npmjs.com/package/nanobanana-mcp)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

A Model Context Protocol (MCP) server that integrates the powerful Gemini 2.5 Flash Image model for advanced image generation, editing, and manipulation capabilities.

## 🌟 Features

- **🎨 Image Generation**: Create stunning images from text prompts with customizable styles and variations
- **✏️ Image Editing**: Modify existing images with natural language instructions
- **🔧 Image Restoration**: Restore and enhance old or damaged photos
- **🎯 Icon Generation**: Create app icons, favicons, and UI elements in multiple sizes
- **🎨 Pattern & Texture Generation**: Generate seamless patterns and textures for backgrounds
- **📖 Story Sequencing**: Generate sequential images that tell visual stories or processes
- **📊 Diagram Generation**: Create technical diagrams, flowcharts, and architectural mockups

## 📋 Prerequisites

- **Node.js 18+** and npm
- **Gemini API Key**: Set one of these environment variables:
  - `NANOBANANA_GEMINI_API_KEY` (recommended)
  - `NANOBANANA_GOOGLE_API_KEY` 
  - `GEMINI_API_KEY` (fallback)
  - `GOOGLE_API_KEY` (fallback)

For API key setup, see the [official Gemini API documentation](https://ai.google.dev/tutorials/setup).

## 📦 Installation

### From npm

```bash
npm install -g nanobanana-mcp
```

### From Source

```bash
git clone https://github.com/gemini-cli-extensions/nanobanana.git
cd nanobanana/mcp-server
npm install
npm run build
npm install -g .
```

## 🚀 Usage

### Standalone Server

Start the MCP server in stdio mode:

```bash
nanobanana-mcp
```

Or with development mode:

```bash
npm run dev
```

### Integration with Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "nanobanana": {
      "command": "nanobanana-mcp",
      "args": []
    }
  }
}
```

### Available Tools

#### 1. `generate_image`

Generate single or multiple images from text prompts.

**Parameters:**
- `prompt` (string, required): The text prompt describing the image to generate
- `outputCount` (number): Number of variations (1-8, default: 1)
- `styles` (array): Artistic styles (photorealistic, watercolor, oil-painting, sketch, pixel-art, anime, vintage, modern, abstract, minimalist)
- `variations` (array): Variation types (lighting, angle, color-palette, composition, mood, season, time-of-day)
- `format` (string): Output format - "grid" or "separate" (default: "separate")
- `seed` (number): Seed for reproducible variations
- `preview` (boolean): Automatically open generated images (default: false)

**Example:**

```json
{
  "name": "generate_image",
  "arguments": {
    "prompt": "sunset over mountains",
    "outputCount": 3,
    "styles": ["watercolor", "oil-painting"],
    "preview": true
  }
}
```

#### 2. `edit_image`

Edit an existing image based on a text prompt.

**Parameters:**
- `prompt` (string, required): The text prompt describing the edits to make
- `file` (string, required): The filename of the input image
- `preview` (boolean): Automatically open generated images (default: false)

**Example:**

```json
{
  "name": "edit_image",
  "arguments": {
    "prompt": "add sunglasses to the person",
    "file": "portrait.jpg",
    "preview": true
  }
}
```

#### 3. `restore_image`

Restore or enhance an existing image.

**Parameters:**
- `prompt` (string, required): The text prompt describing the restoration
- `file` (string, required): The filename of the input image
- `preview` (boolean): Automatically open generated images (default: false)

**Example:**

```json
{
  "name": "restore_image",
  "arguments": {
    "prompt": "remove scratches and improve clarity",
    "file": "old_photo.jpg"
  }
}
```

#### 4. `generate_icon`

Generate app icons, favicons, and UI elements.

**Parameters:**
- `prompt` (string, required): Description of the icon to generate
- `sizes` (array): Icon sizes in pixels (16, 32, 64, 128, 256, 512, 1024)
- `type` (string): "app-icon", "favicon", or "ui-element" (default: "app-icon")
- `style` (string): "flat", "skeuomorphic", "minimal", or "modern" (default: "modern")
- `format` (string): "png" or "jpeg" (default: "png")
- `background` (string): "transparent", "white", "black", or color name (default: "transparent")
- `corners` (string): "rounded" or "sharp" (default: "rounded")
- `preview` (boolean): Automatically open generated images (default: false)

**Example:**

```json
{
  "name": "generate_icon",
  "arguments": {
    "prompt": "coffee cup logo",
    "sizes": [64, 128, 256],
    "type": "app-icon",
    "style": "minimal"
  }
}
```

#### 5. `generate_pattern`

Generate seamless patterns and textures.

**Parameters:**
- `prompt` (string, required): Description of the pattern
- `size` (string): Pattern tile size (default: "256x256")
- `type` (string): "seamless", "texture", or "wallpaper" (default: "seamless")
- `style` (string): "geometric", "organic", "abstract", "floral", or "tech" (default: "abstract")
- `density` (string): "sparse", "medium", or "dense" (default: "medium")
- `colors` (string): "mono", "duotone", or "colorful" (default: "colorful")
- `repeat` (string): "tile" or "mirror" (default: "tile")
- `preview` (boolean): Automatically open generated images (default: false)

**Example:**

```json
{
  "name": "generate_pattern",
  "arguments": {
    "prompt": "geometric hexagons",
    "type": "seamless",
    "style": "geometric",
    "colors": "duotone"
  }
}
```

#### 6. `generate_story`

Generate sequential images that tell a story or process.

**Parameters:**
- `prompt` (string, required): Description of the story or process
- `steps` (number): Number of sequential images (2-8, default: 4)
- `type` (string): "story", "process", "tutorial", or "timeline" (default: "story")
- `style` (string): "consistent" or "evolving" (default: "consistent")
- `layout` (string): "separate", "grid", or "comic" (default: "separate")
- `transition` (string): "smooth", "dramatic", or "fade" (default: "smooth")
- `format` (string): "storyboard" or "individual" (default: "individual")
- `preview` (boolean): Automatically open generated images (default: false)

**Example:**

```json
{
  "name": "generate_story",
  "arguments": {
    "prompt": "a seed growing into a tree",
    "steps": 5,
    "type": "process",
    "style": "consistent"
  }
}
```

#### 7. `generate_diagram`

Generate technical diagrams and visualizations.

**Parameters:**
- `prompt` (string, required): Description of the diagram
- `type` (string): "flowchart", "architecture", "network", "database", "wireframe", "mindmap", or "sequence" (default: "flowchart")
- `style` (string): "professional", "clean", "hand-drawn", or "technical" (default: "professional")
- `layout` (string): "horizontal", "vertical", "hierarchical", or "circular" (default: "hierarchical")
- `complexity` (string): "simple", "detailed", or "comprehensive" (default: "detailed")
- `colors` (string): "mono", "accent", or "categorical" (default: "accent")
- `annotations` (string): "minimal" or "detailed" (default: "detailed")
- `preview` (boolean): Automatically open generated images (default: false)

**Example:**

```json
{
  "name": "generate_diagram",
  "arguments": {
    "prompt": "user authentication flow",
    "type": "flowchart",
    "style": "professional",
    "complexity": "detailed"
  }
}
```

## 🛠️ Development

### Build

```bash
npm run build
```

### Development Mode with Watch

```bash
npm run dev
```

### Type Checking

```bash
npm run typecheck
```

### Start Server

```bash
npm start
```

## 🏗️ Architecture

### Core Components

- **`index.ts`**: MCP server implementation using `@modelcontextprotocol/sdk`
- **`imageGenerator.ts`**: Handles all Gemini API interactions and response processing
- **`fileHandler.ts`**: Manages file I/O, smart filename generation, and file searching
- **`types.ts`**: TypeScript interfaces for type safety

### Key Features

- **Type-Safe**: Full TypeScript support with comprehensive interfaces
- **Error Handling**: Robust error handling with detailed debug logging
- **Protocol Compliance**: Strict adherence to Model Context Protocol (MCP) specification
- **Resource Efficient**: Optimized for Claude and other MCP clients

## 🔐 Environment Configuration

The server supports multiple environment variables for API key authentication:

```bash
# Recommended for Gemini API key
export NANOBANANA_GEMINI_API_KEY="your-api-key"

# Alternative for Vertex API
export NANOBANANA_GOOGLE_API_KEY="your-api-key"

# Fallbacks
export GEMINI_API_KEY="your-api-key"
export GOOGLE_API_KEY="your-api-key"
```

## 🐛 Troubleshooting

### No API Key Found

Ensure one of the supported environment variables is set:

```bash
export NANOBANANA_GEMINI_API_KEY="your-key"
```

### Build Errors

Ensure Node.js 18+ is installed:

```bash
node --version
npm run build
```

### Type Errors

Run type checking to identify issues:

```bash
npm run typecheck
```

### Debug Mode

The server includes detailed logging output on stderr for debugging:

```bash
nanobanana-mcp 2>&1 | grep -i "debug\|error"
```

## 📄 Legal

- **License**: Apache License 2.0 - See [LICENSE](../../LICENSE)
- **Author**: Gemini CLI Extensions
- **Repository**: [github.com/gemini-cli-extensions/nanobanana](https://github.com/gemini-cli-extensions/nanobanana)

## 🤝 Contributing

Contributions are welcome! Please see our [Contributing Guidelines](../../docs/contributing.md).

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run `npm run build && npm run typecheck`
5. Submit a pull request

## 📚 Related Resources

- [Model Context Protocol Specification](https://modelcontextprotocol.io/)
- [Gemini API Documentation](https://ai.google.dev/)
- [Claude Desktop Setup Guide](https://claude.ai/docs)
- [Main Nano Banana Repository](https://github.com/gemini-cli-extensions/nanobanana)

## 🙋 Support

For issues, questions, or suggestions, please open an issue on [GitHub](https://github.com/gemini-cli-extensions/nanobanana/issues).

---

Made with ❤️ by the Gemini CLI Extensions team
