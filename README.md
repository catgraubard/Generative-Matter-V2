# Generative Matter

> **AI-enhanced materials database for architectural and design applications**

A comprehensive database of **120,000+ material synthesis recipes** with detailed physical properties and AI-generated visual descriptions, designed for AI agents, researchers, and computational designers.

## 🎯 Overview

This repository provides structured material synthesis data optimized for:
- **AI-powered material discovery** and recommendation systems
- **Computational design** workflows requiring material properties
- **Educational** materials science applications
- **Research** in materials informatics and generative design

## ✨ Key Features

- 🔬 **120,000+ Materials** with complete synthesis recipes
- 📊 **Rich Property Data**: Crystal structure, bandgap, density, thermodynamics
- 🎨 **AI Visual Descriptions**: Appearance data for 291+ curated materials (color, texture, luster)
- 🤖 **MCP-Compatible**: Ready for AI agent integration
- 📁 **Multiple Formats**: Excel (human-readable) + JSON (AI-ready)
- 🖼️ **Image Prompts**: 3 photorealistic prompts per material (DALL-E/Midjourney/Stable Diffusion)

## 🚀 Quick Start

### For Designers & Researchers

```python
import pandas as pd

# Load human-readable Excel file
df = pd.read_excel('MaterialRecipes_with_AI_Descriptions.xlsx')

# Browse materials by visual properties
metallic = df[df['AI_Reflectivity_Luster'].str.contains('metallic')]

# Get image generation prompt
prompt = df.iloc[0]['AI_Image_Prompt_1_Closeup']
# → Use with DALL-E, Midjourney, or Stable Diffusion
```

### For AI Agents & Developers

```python
import json

# Load MCP-compliant database (streaming format)
with open('ai_database/materials_database.jsonl') as f:
    for line in f:
        material = json.loads(line)
        
        # Access synthesis recipe
        temp = material['recipe']['heating']['temperature_celsius']
        
        # Access material properties
        bandgap = material['properties']['electronic']['bandgap']
        crystal = material['properties']['structure']['crystal_system']
```

## 📂 Repository Structure

```
Generative-Matter/
├── MaterialRecipes_with_AI_Descriptions.xlsx   # Excel (human-readable, 291 curated)
├── MaterialRecipes_Full.xlsx                   # Excel (complete, 120K materials)
│
├── ai_database/                                # MCP-compliant AI database
│   ├── materials_database.jsonl                # Streaming format (memory efficient)
│   ├── materials_database.json                 # Complete JSON
│   ├── materials_index.json                    # Search index
│   └── materials/*.json                        # Individual material files
│
├── scripts/
│   ├── generate_visual_descriptions.py         # Generate AI appearance data
│   └── convert_to_mcp.py                       # Convert to MCP format
│
└── README.md
```

## 📊 Data Formats

### Excel Format (Human-Readable)

**MaterialRecipes_with_AI_Descriptions.xlsx** - Curated subset with visual descriptions:
- Material composition and synthesis recipe
- Physical properties (29 columns)
- AI-generated visual characteristics (12 columns):
  - Primary/Secondary Colors
  - Surface Texture & Reflectivity
  - Opacity & Edge Characteristics
  - 3× Image Generation Prompts

**MaterialRecipes_Full.xlsx** - Complete database (120,000 materials)

### JSON Format (AI-Ready)

**MCP-Compliant Structure** - Each material includes:
```json
{
  "id": "Ag3Er2Ga8La1",
  "uri": "material://Ag3Er2Ga8La1",
  "composition": { "formula": "...", "elements": {...} },
  "recipe": { 
    "materials": [...],
    "heating": { "temperature_celsius": 900, "duration_hours": 2 },
    "cooling": { "method": "natural" }
  },
  "properties": {
    "structure": { "crystal_system": "monoclinic", "density": 6358 },
    "electronic": { "bandgap": 0.012 },
    "energetics": { "formation_energy_per_atom": -1965 }
  }
}
```

**Three access methods:**
- `materials_database.jsonl` - Stream one material at a time (memory efficient)
- `materials_database.json` - Load complete database
- `materials/{composition}.json` - Direct file access

## 🔍 Search & Query

### Simple Filtering

```python
# Search by element
index = json.load(open('ai_database/materials_index.json'))
copper_materials = index['by_element']['Cu']

# Search by crystal system
cubic_materials = index['by_crystal_system']['cubic']
```

### Property-Based Search

```python
# Find semiconductors with specific bandgap
materials = json.load(open('ai_database/materials_database.json'))

semiconductors = [
    m for m in materials
    if 0.5 < m['properties']['electronic']['bandgap'] < 3.0
]
```

## 🎯 Use Cases

**Material Discovery**: Find materials with target properties (bandgap, crystal structure, synthesis temperature)

**AI Image Generation**: Generate photorealistic material visualizations using included prompts

**Synthesis Planning**: Extract exact synthesis conditions (temperature, time, cooling method)

**Computational Design**: Integrate material constraints into generative design workflows

**Education**: Teaching materials science, crystallography, and synthesis methods

## 📈 Database Statistics

| Metric | Value |
|--------|-------|
| Total Materials | 120,000+ |
| Unique Elements | 61 |
| Crystal Systems | 7 |
| Temperature Range | 5°C - 2500°C |
| Bandgap Range | 0 - 5.2 eV |
| With AI Descriptions | 291 (growing) |

## 🤖 MCP Integration

This database follows the **Model Context Protocol** specification for seamless AI agent integration.

**Resource URIs**: Each material has a unique identifier  
Format: `material://Ag3Er2Ga8La1`

**Supported Operations**:
- `search_materials` - Query by composition, properties, or synthesis conditions
- `get_material` - Retrieve complete material data by ID

See `ai_database/mcp_resources.json` for complete specifications.

## 🛠️ Scripts

**generate_visual_descriptions.py** - Generate AI appearance descriptions using GPT-4o
```bash
python scripts/generate_visual_descriptions.py
```

**convert_to_mcp.py** - Convert Excel data to MCP-compliant JSON
```bash
python scripts/convert_to_mcp.py
```

## 📖 Data Sources

- **Material Properties**: Computational materials science (DFT calculations)
- **Synthesis Recipes**: LLM-generated based on materials science principles
- **Visual Descriptions**: GPT-4o with expert validation

## 🤝 Contributing

Contributions welcome! Consider:
- Adding synthesis recipes for new materials
- Enhancing property data
- Improving AI visual descriptions
- Building analysis tools or integrations

## 📄 License

[Specify license - MIT, Apache 2.0, CC-BY, etc.]

## 📧 Contact

**Generative Matter Project**  
Daniel Bolojan - University of Texas at Austin School of Architecture

For questions, collaborations, or suggestions, please open an issue or reach out directly.

---

**Last Updated**: October 2025  
**Materials**: 120,000+  
**MCP Compatible**: Yes (v2024-11-05)
