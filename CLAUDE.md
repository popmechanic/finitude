# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

![Banner](banner.png)

## Repository Overview

**SONGFIELD** is a creative constraint tool for songwriters built as a single HTML file application. It generates random creative prompts across 7 categories (Theme, Symbol Pair, Mechanic, Form, Color Mood, Harmony, Production Move) using AI and dice-rolling mechanics.

## Architecture

### Single-File Application Structure
- **Finitude.html** - Complete self-contained React application
- **banner.png** - Visual branding asset
- **CLAUDE.md** - This documentation file

### Technology Stack
- **React 19.1.1** via ESM modules from esm.sh
- **Babel Standalone** for JSX transformation in browser
- **Tailwind CSS v4** via CDN for styling
- **Fireproof database** (`use-fireproof@0.23.0`) for local-first data persistence
- **call-ai library** for AI integration with streaming responses
- **html2canvas-pro** for screenshot functionality

### Key Dependencies (CDN-based)
```javascript
// Import map configuration
"react": "https://esm.sh/react@19.1.1/es2022/react.mjs"
"react-dom": "https://esm.sh/react-dom@19.1.1/es2022/react-dom.mjs"
"use-fireproof": "https://esm.sh/use-fireproof@0.23.0"
"call-ai": "https://esm.sh/call-ai"
"use-vibes": "https://esm.sh/use-vibes"
```

## Application Features

### Core Mechanics
- **7-step creative process** with randomized options via dice rolling
- **AI-generated constraints** for each category using structured prompts
- **One veto per session** - ability to replace a rolled option
- **Local data persistence** using Fireproof database
- **Session tracking** with unique seeds and timestamps
- **Export functionality** (copy to clipboard, print)

### Creative Categories
1. **Theme** - Minimal emotional territory phrases
2. **Symbol Pair** - Two resonant images (e.g., "Moths + Static")
3. **Mechanic** - Musical DNA to borrow (rhythm, harmony, etc.)
4. **Form** - Song structure notation
5. **Color Mood** - Emotional palette with context
6. **Harmony** - Chord progressions and approaches
7. **Production Move** - Specific production techniques

## Development Workflow

### Running the Application
```bash
# Serve locally (any static server)
python -m http.server 8000
# or
npx serve .
# Then open http://localhost:8000/Finitude.html
```

### Key Code Patterns

#### AI Integration
- Uses `call-ai` library with structured JSON schemas
- Fallback options for each category when AI fails
- Streaming request tracking with iframe communication

#### State Management
- React hooks for UI state (`useState`, `useEffect`)
- Fireproof `useLiveQuery` for database-driven state
- Session persistence with unique seeds

#### Error Handling
- Comprehensive Babel transform error catching
- JSX syntax error detection and reporting
- Unhandled promise rejection tracking
- Parent window communication for error reporting

### Database Schema
```javascript
// Session document structure
{
  type: 'songfield-session',
  seed: number,           // Unique session identifier
  timestamp: string,      // ISO timestamp
  selections: object,     // User selections by category
  rollHistory: array,     // Dice roll history
  completedAt: string     // Completion timestamp
}
```

## Styling Architecture

### Design System
- **Color Palette**: `#70d6ff` (blue), `#ff70a6` (pink), `#ffd670` (yellow), `#e9ff70` (lime), `#ff9770` (orange), `#242424` (dark)
- **Typography**: System fonts with black weight emphasis
- **Layout**: Card-based design with bold borders
- **Patterns**: Diagonal stripes and geometric backgrounds

### Responsive Design
- Mobile-first approach with Tailwind utilities
- Grid layouts for options and sessions
- Flexible button and card scaling

## AI Prompt Engineering

### Structured Prompts
Each category has carefully crafted prompts optimizing for:
- **Minimal, understated language** (avoiding flowery/overwrought phrasing)
- **Specific constraints** (BPM ranges, chord notation, etc.)
- **Practical application** (stageable techniques, readable forms)
- **Consistent JSON response format**

### Response Validation
- JSON schema enforcement for all AI responses
- Fallback content for each category
- Length limits on explainer text (150 characters)

## Browser Requirements

- **Modern ES2022 support** for ESM modules
- **ES6+ features** (async/await, destructuring, arrow functions)
- **Canvas API** support for screenshot functionality
- **Clipboard API** for export features

This application demonstrates a local-first, AI-integrated creative tool pattern suitable for artistic constraint generation.