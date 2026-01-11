# Generative Matter

> **AI-enhanced materials database for architectural and design applications**

[![DOI](https://img.shields.io/badge/DOI-10.7910%2FDVN%2FU6O6KS-blue)](https://doi.org/10.7910/DVN/U6O6KS)

Generative Matter is a database of **120,000+ material synthesis recipes** with physical properties and AI-generated visual descriptions, designed for **AI agents**, **researchers**, and **computational designers** working between materials science and architecture.

This repository is associated with the paper:

> Catherine Graubard, Daniel Koehler.  
> **“Generative Matter for Architecture: LLM-Guided Discovery and Low-Tech Prototyping of Resilient Synthetic Materials.”**  
> In: *ACADIA 2025 Proceedings*, Miami, forthcoming 5–7 November 2025.

This repository also accompanies the master’s thesis:

**LLM Meta-Materials: A Paradigm Shift in Architecture through LLM-
Driven Synthetic Materials**

by **Catherine Graubard**

Thesis  
Presented to the Faculty of the Graduate School of  
The University of Texas at Austin  

Master of Science in Sustainable Design  
The University of Texas at Austin  

May 2025  

**APPROVED BY**  
**SUPERVISING COMMITTEE:**  
Dr. Daniel Koehler, Supervisor  
Dr. Juliana Felkner, Co-Supervisor  

- 🔬 **120,000+ Materials** with complete synthesis recipes  
- 📊 **Rich Property Data**: Crystal structure, bandgap, density, thermodynamics  
- 🎨 **AI Visual Descriptions**: Appearance data for curated materials  
- 🤖 **MCP-Compatible**: Ready for AI agent integration  
- 📁 **Multiple Formats**: Excel (human-readable) + JSON (AI-ready)  

---

## Overview

This repository provides structured material synthesis data optimized for:

- **AI-powered material discovery** and recommendation systems  
- **Computational design** workflows requiring material properties  

At its core, Generative Matter links:

- **Synthesis recipes** (inputs, temperatures, durations, cooling)  
- **Physical properties** (structure, bandgap, density, thermodynamics)  
- **AI-generated visual descriptors** (color, texture, luster, opacity)  
- **Text-to-image prompts** for photorealistic visualization  

---

## Quick Start

Download and open the main Excel file containing the complete database of ≈120,000 materials (e.g. `MaterialRecipes.xlsx` or `MaterialRecipes_Full.xlsx`, depending on your final naming).

### Example: Python + Excel

```python
import pandas as pd

df = pd.read_excel("MaterialRecipes.xlsx")

# Example: filter for metallic-looking materials
metallic = df[df["AI_Reflectivity_Luster"].str.contains("metallic", na=False)]

# Get an image generation prompt
prompt = df.iloc[0]["AI_Image_Prompt_1_Closeup"]
print(prompt)
```

### For Developers & AI Agents (JSON / MCP workflow)

```python
import json

with open("ai_database/materials_database.jsonl") as f:
    for line in f:
        material = json.loads(line)

        # Access synthesis recipe
        temp = material["recipe"]["heating"]["temperature_celsius"]

        # Access material properties
        bandgap = material["properties"]["electronic"]["bandgap"]
        crystal = material["properties"]["structure"]["crystal_system"]
```

---

## Repository Structure

> Adjust this section to match the files you actually ship in your GitHub release.

```text
Generative-Matter-V2/
├── MaterialRecipes.xlsx or MaterialRecipes_Full.xlsx   # Excel: complete database (~120K materials)
├── Nanoforge_MCP/                                     # Example MCP resources / integration
├── ai_database/                                       # MCP-compliant AI database (optional)
│   ├── materials_database.jsonl                       # Streaming format (memory efficient)
│   ├── materials_database.json                        # Complete JSON
│   ├── materials_index.json                           # Search index
│   └── materials/*.json                               # Individual material files
│
├── scripts/
│   ├── generate_visual_descriptions.py                # Generate AI appearance data
│   └── convert_to_mcp.py                              # Convert to MCP / JSON formats
│
└── README.md
```

---

## Data Formats

### Excel

The Excel file contains, per material:

- Composition and synthesis recipe  
- Physical properties (e.g. density, crystal system, bandgap, formation energy)  
- AI-generated visual characteristics, including:  
  - Primary / secondary colors  
  - Surface texture & reflectivity  
  - Opacity & edge characteristics  
  - 3× text-to-image prompts (close-up, context, macro / detail)

### JSON / MCP

Each material follows a MCP-friendly JSON schema, for example:

```json
{
  "id": "Ag3Er2Ga8La1",
  "uri": "material://Ag3Er2Ga8La1",
  "composition": { "formula": "Ag3Er2Ga8La1", "elements": { "Ag": 3, "Er": 2, "Ga": 8, "La": 1 } },
  "recipe": {
    "materials": [ ... ],
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

---

## MCP Integration

This database can be exposed as a **Model Context Protocol (MCP)** resource.

**Resource URIs** – each material has a unique identifier of the form:  
`material://<id>`

**Typical MCP operations**:

- `search_materials` – query by composition, properties, or synthesis conditions  
- `get_material` – retrieve complete material data by ID  

See the `Nanoforge_MCP/` and `ai_database/` directory (if present) for concrete integration examples.

---

## How to cite

If you use Generative Matter in academic work, please cite **both** the paper and the dataset / code snapshot.

### 1. Paper

> Catherine Graubard, Daniel Koehler.  
> “Generative Matter for Architecture: LLM-Guided Discovery and Low-Tech Prototyping of Resilient Synthetic Materials.”  
> In: *ACADIA 2025 Proceedings*, Miami, forthcoming 5–7 November 2025.

**BibTeX:**

```bibtex
@inproceedings{GraubardKoehler_GenerativeMatter_2025,
  author    = {Graubard, Catherine and Koehler, Daniel},
  title     = {Generative Matter for Architecture: LLM-Guided Discovery and Low-Tech Prototyping of Resilient Synthetic Materials},
  booktitle = {Proceedings of the 2025 ACADIA Conference},
  address   = {Miami, USA},
  year      = {2025},
  note      = {Forthcoming 5--7 November 2025}
}
```

### Dataset

> *Generative Matter: AI-Enhanced Material Synthesis Database (v2.0.0)*, 2026.  
> DOI: `10.7910/DVN/U6O6KS`

```bibtex
@dataset{Graubard_GenerativeMatter_2026,
  author    = {Graubard, Catherine},
  title     = {Generative Matter},
  year      = {2026},
  publisher = {Harvard Dataverse},
  doi       = {10.7910/DVN/U6O6KS}
}
```

### Master’s Thesis

```bibtex
@thesis{Graubard_LLM_MetaMaterials_2025,
  author = {Graubard, Catherine},
  title  = {LLM Meta-Materials: A Paradigm Shift in Architecture through LLM-Driven Synthetic Materials},
  school = {The University of Texas at Austin},
  year   = {2025}
}
```

---

## License

- **Data**: Creative Commons Attribution 4.0 International (CC BY 4.0)  
- **Code**: MIT License  

---

## 📧 Contact

**Catherine Graubard**  
cg47875@utexas.edu  

**Daniel Koehler**  
Assistant Professor of Architecture  
The University of Texas at Austin  
daniel.koehler@utexas.edu  

---

**Last Updated**: 2026  
**Materials**: 120,000+  
**MCP Compatible**: Yes (v2024-11-05)
