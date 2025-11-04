#Nanoforge Materials Database - MCP Access Guide

## Overview
This database contains 119987 material synthesis recipes with properties.
Generated: 2025-10-30T15:15:56.048154Z
MCP Version: 2024-11-05

## Access Patterns

### 1. Stream Processing (Memory Efficient)
```python
import json

# Process one material at a time
with open('materials_database.jsonl', 'r') as f:
    for line in f:
        material = json.loads(line)
        # Process material...
```

### 2. Load Complete Database
```python
import json

with open('materials_database.json', 'r') as f:
    materials = json.load(f)
```

### 3. Direct Material Access
```python
import json

# Load specific material
composition = "Ag3Er2Ga8La1"
with open(f'materials/{composition}.json', 'r') as f:
    material = json.load(f)
```

### 4. Search via Index
```python
import json

with open('materials_index.json', 'r') as f:
    index = json.load(f)

# Find all materials containing Copper
cu_materials = index['by_element']['Cu']

# Find all cubic crystals
cubic_materials = index['by_crystal_system']['cubic']

# Check property ranges
temp_range = index['property_ranges']['temperature_celsius']
print(f"Synthesis temperatures: {temp_range['min']}°C - {temp_range['max']}°C")
```

## Data Structure

Each material record contains:
- `composition`: Chemical formula and elemental breakdown
- `recipe`: Complete synthesis instructions (materials, heating, cooling, etc.)
- `properties`: Material properties (structure, energetics, electronic)
- `metadata`: MCP resource URI and provenance

See `schema.json` for complete structure documentation.

## MCP Integration

This database follows the Model Context Protocol (MCP).
See `mcp_resources.json` for:
- Resource URI templates
- Tool definitions
- Query schemas

## Files

- `materials_database.jsonl` - Streaming format (119987 lines)
- `materials_database.json` - Complete database (JSON array)
- `materials_index.json` - Search index
- `materials/` - Individual material files (119987 files)
- `schema.json` - Complete schema documentation
- `mcp_resources.json` - MCP integration definitions
