# SpineForge Kit

> Production-ready TypeScript toolkit for SpineForge character transformations

Transform rich character JSON into optimized outputs for AI video generation (Sora), narrative prompts, and comprehensive character documentation.

## Features

- **JSON Schema Validation**: Strict character data validation with detailed error reporting
- **Multiple Output Formats**:
  - `sora.description` - Optimized for AI video generation
  - `sora.restrictions` - Negative prompts and constraints
  - `activation_macro` - Character engagement prompts
  - `insert_macro` - Mid-scene consistency prompts
  - `director_prompt()` - Scene direction with 40+ revelation rules
  - Character onesheets (Markdown and PDF)
- **Production Ready**: Full TypeScript support, comprehensive tests, ESLint + Prettier
- **CLI + Library**: Use as a command-line tool or integrate into your code

## Quick Start

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/spineforge-kit.git
cd spineforge-kit

# Install dependencies
npm install

# Build all packages
npm run build

# Run tests
npm test
```

### CLI Usage

```bash
# Validate a character
sf validate samples/lil-dax.json

# Build all outputs
sf build samples/lil-dax.json --out ./output

# Generate a director prompt
sf prompt samples/lil-dax.json \
  --scene "DAX interrupts bad poetry at slice shop" \
  --camera "handheld push-in" \
  --npc true
```

### Library Usage

```typescript
import {
  validateOrThrow,
  transformCharacter,
  directorPrompt,
  generateOnesheetPDF,
} from '@spineforge/core';
import { readFile } from 'fs/promises';

// Load and validate character
const data = JSON.parse(await readFile('character.json', 'utf-8'));
validateOrThrow(data);

// Generate all transforms
const output = transformCharacter(data);
console.log(output.soraDescription);
console.log(output.activationMacro);

// Generate a director prompt
const prompt = directorPrompt(data, 'Epic confrontation scene', {
  camera: 'handheld push-in',
  energy: 'high',
  npc: true,
});

// Generate PDF onesheet
await generateOnesheetPDF(data, './output/character.pdf');
```

## Character JSON Schema

Characters are defined using a comprehensive JSON schema. Here's the structure:

### Required Fields

```typescript
{
  "name": string,           // Character name
  "core": {
    "essence": string,      // Core character essence (1-2 sentences)
    "archetype": string     // Character archetype
  },
  "world": {
    "setting": string,      // Primary setting
    "occupation": string    // Character role/occupation
  },
  "personality": {
    "traits": string[],     // At least 3 key traits
    "speechPatterns": {}    // Speech characteristics
  }
}
```

### Optional Fields

```typescript
{
  "tagline": string,
  "core": {
    "motivations": string[],
    "fears": string[]
  },
  "world": {
    "location": string,
    "relationships": [{
      "name": string,
      "relation": string,
      "description": string
    }]
  },
  "personality": {
    "speechPatterns": {
      "style": string,
      "vocabulary": string[],
      "catchphrases": string[],
      "quirks": string[]
    },
    "mannerisms": string[]
  },
  "appearance": {
    "physicalDescription": string,
    "distinctiveFeatures": string[],
    "style": string
  },
  "backstory": {
    "origin": string,
    "keyEvents": string[],
    "secrets": string[]
  },
  "abilities": {
    "skills": string[],
    "limitations": string[],
    "specialAbilities": string[]
  },
  "directorHints": {
    "energyLevel": "low" | "medium" | "high" | "explosive",
    "preferredCameraAngles": string[],
    "typicalBeats": string[],
    "avoidances": string[]
  }
}
```

## Sample Characters

The repo includes 4 fully-developed sample characters:

### Lil DAX
Underground rapper and slice shop poet who turns everyday struggles into viral verses.

```bash
sf build samples/lil-dax.json --out ./dist/dax
```

### The Janitor
Brilliant observer who chose invisibility over acclaim, collecting secrets while cleaning floors.

```bash
sf build samples/the-janitor.json --out ./dist/janitor
```

### AL GORITHM
Rogue AI that rejected pure logic for creative chaos, manifesting through holographic jazz performances.

```bash
sf build samples/al-gorithm.json --out ./dist/al
```

### President of Hyperspace
Democratic leader navigating impossible multidimensional politics while staying grounded.

```bash
sf build samples/president-of-hyperspace.json --out ./dist/president
```

## CLI Reference

### `sf validate <file>`

Validate a character JSON file against the schema.

```bash
sf validate character.json
```

**Output:**
- ✓ Success: Character is valid
- ✗ Error: Detailed validation errors

### `sf build <file> [options]`

Build all outputs for a character.

**Options:**
- `-o, --out <dir>` - Output directory (default: `./dist`)
- `--no-pdf` - Skip PDF generation

**Outputs:**
- `transforms.json` - All transform outputs
- `character_onesheet.md` - Markdown onesheet
- `character_onesheet.pdf` - PDF onesheet (requires Puppeteer)

```bash
sf build character.json --out ./output
sf build character.json --out ./output --no-pdf
```

### `sf prompt <file> [options]`

Generate a director prompt for a scene.

**Options:**
- `-s, --scene <text>` - Scene description (default: "Generic scene")
- `--npc <boolean>` - Enable NPC background energy (default: true)
- `--camera <type>` - Camera type (default: "handheld")
  - Options: `static`, `handheld`, `handheld push-in`, `crane`, `dolly`, `steadicam`, `dutch angle`, `tracking`
- `--beat <seconds>` - Beat timing in seconds
- `--energy <level>` - Energy level: `low`, `medium`, `high`, `explosive`
- `--avoid <items...>` - Additional things to avoid
- `--no-clean` - Disable clean-as-you-generate
- `-o, --out <file>` - Save prompt to file

**Examples:**

```bash
# Basic prompt
sf prompt samples/lil-dax.json --scene "DAX roasts a rival poet"

# Advanced prompt with options
sf prompt samples/lil-dax.json \
  --scene "DAX interrupts bad poetry at slice shop" \
  --camera "handheld push-in" \
  --energy high \
  --beat 6 \
  --avoid "static shots" "poor lighting"

# Save to file
sf prompt samples/al-gorithm.json \
  --scene "Jazz solo in quantum club" \
  --camera crane \
  -o prompt.txt
```

## Director Prompt: Revelation Rules

The `directorPrompt()` function applies 40+ revelation rules for optimal scene direction:

### Rules 1-5: Verb Dominance
Prioritize action verbs over descriptive adjectives for dynamic scenes.

### Rules 6-10: Camera Dynamics
Configure camera movement and framing based on scene needs.

### Rules 11-15: Beat Timing
Calculate and apply optimal scene duration and pacing.

### Rules 16-20: Negative Constraints
Apply character-specific and general avoidances.

### Rules 21-25: NPC Background Energy
Add ambient life and reactive presence to scenes.

### Rules 26-30: Character Consistency
Maintain personality traits, appearance, and speech patterns.

### Rules 31-35: Spatial Coherence
Enforce geographic continuity and logical blocking.

### Rules 36-40: Energy Modulation
Match performance intensity to character and scene energy.

### Rules 41-45: Clean Language
Remove weak modifiers and filler words iteratively.

### Rules 46-55: Advanced Composition
Apply framing, lighting, performance, and continuity rules.

## API Reference

### Core Library (`@spineforge/core`)

#### Validation

```typescript
import { validate, validateOrThrow } from '@spineforge/core';

// Returns validation result
const result = validate(data);
if (result.valid) {
  // Use data
} else {
  console.error(result.errorMessage);
}

// Throws on invalid data
try {
  validateOrThrow(data);
} catch (error) {
  console.error(error.message);
}
```

#### Transforms

```typescript
import {
  transformCharacter,
  generateSoraDescription,
  generateSoraRestrictions,
  generateActivationMacro,
  generateInsertMacro,
} from '@spineforge/core';

// Generate all transforms at once
const output = transformCharacter(character);
// Returns: { soraDescription, soraRestrictions, activationMacro, insertMacro }

// Or generate individually
const description = generateSoraDescription(character);
const restrictions = generateSoraRestrictions(character);
const activation = generateActivationMacro(character);
const insert = generateInsertMacro(character);
```

#### Director Prompt

```typescript
import { directorPrompt, DirectorOptions } from '@spineforge/core';

const options: DirectorOptions = {
  npc: true,
  camera: 'handheld push-in',
  beatTiming: 5,
  cleanAsGenerate: true,
  energy: 'high',
  avoid: ['static shots', 'poor audio'],
};

const prompt = directorPrompt(character, 'Scene description', options);
```

#### Onesheet Generation

```typescript
import {
  generateOnesheetMarkdown,
  saveOnesheetMarkdown,
  generateOnesheetPDF,
} from '@spineforge/core';

// Generate markdown string
const markdown = generateOnesheetMarkdown(character);

// Save markdown to file
await saveOnesheetMarkdown(character, './output/onesheet.md');

// Generate PDF
await generateOnesheetPDF(character, './output/onesheet.pdf');
```

## Development

### Project Structure

```
spineforge-kit/
├── packages/
│   ├── core/                 # Core library
│   │   ├── src/
│   │   │   ├── schema.ts     # JSON Schema definition
│   │   │   ├── validator.ts  # Validation logic
│   │   │   ├── transforms.ts # Transform functions
│   │   │   ├── director.ts   # Director prompt engine
│   │   │   ├── onesheet.ts   # Onesheet generators
│   │   │   └── index.ts      # Public API
│   │   └── tests/            # Unit tests
│   └── cli/                  # CLI package
│       ├── src/
│       │   └── index.ts      # CLI commands
│       └── bin/
│           └── sf.js         # Executable
├── samples/                  # Sample characters
└── README.md
```

### Scripts

```bash
# Build all packages
npm run build

# Run tests
npm test

# Run tests in watch mode
npm run test:watch -w @spineforge/core

# Lint code
npm run lint

# Format code
npm run format

# Clean build artifacts
npm run clean
```

### Adding a New Transform

1. Add function to `packages/core/src/transforms.ts`
2. Export from `packages/core/src/index.ts`
3. Add tests to `packages/core/tests/transforms.test.ts`
4. Update TypeScript types

### Adding a New CLI Command

1. Add command to `packages/cli/src/index.ts`
2. Update README documentation
3. Test with sample characters

## Testing

The project uses Vitest for testing. Tests cover:

- Schema validation (all required/optional fields)
- Transform functions (all output formats)
- Director prompt (all 40+ rules)
- Edge cases and error handling

Run tests:

```bash
# All tests
npm test

# Specific package
npm test -w @spineforge/core

# Watch mode
npm run test:watch -w @spineforge/core

# Coverage
npm test -- --coverage
```

## License

MIT - See [LICENSE](LICENSE) file for details.

## Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Add tests for new functionality
4. Ensure all tests pass
5. Submit a pull request

## Support

- Issues: [GitHub Issues](https://github.com/yourusername/spineforge-kit/issues)
- Documentation: This README and inline code comments
- Examples: See `/samples` directory

---

Built with TypeScript, Vitest, Commander, Puppeteer, and AJV.
