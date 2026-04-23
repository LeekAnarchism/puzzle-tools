# Church Puzzle Game Specification

## Overview

Church is a laser puzzle game where players must position mirrors and blockers to direct laser beams from eyes on the grid edges to hit a church target in the center.

## Grid

- Configurable size: 2-20 columns × 2-20 rows (default: 5×5)
- Single-cell border around grid where eyes are placed

## Puzzle Elements

### Church
- Target cell — must be hit by all lasers to win

### Eyes
- Placed on grid edges (top, bottom, left, right)
- Each emits a laser pointing inward

### Buildings (Square Tiles)
- Solid — absorbs lasers. Laser stops at entry face.

### Triangle Tiles (Mirrors)
- Corner variants: NW, NE, SW, SE
- Laser hitting diagonal reflects 90°
- Laser passing through empty half continues straight

## Laser Mechanics

1. Laser travels cell-by-cell through grid
2. At each cell:
   - **Church**: reach → success, stop
   - **Building**: stops at face
   - **Triangle**: reflect 90° if hitting solid half, else pass through
   - **Empty**: pass through
3. Exits when reaching grid edge or out of bounds

### Reflection Mapping
- NW (/): reflect if dc<0 or dr<0 (→ {-dc, -dr})
- NE (\): reflect if dc>0 or dr<0 (→ {dc, dr})
- SW (\): reflect if dc<0 or dr>0 (→ {dc, dr})
- SE (/): reflect if dc>0 or dr>0 (→ {-dc, -dr})

## Win Condition

All lasers from all eyes must reach the church.

## Tools

| Tool | Action |
|------|--------|
| Select | Rectangle select, drag to move, Cmd/Ctrl+click for group |
| Church | Click to place |
| Eye | Click edge to toggle |
| Building | Click to place/remove |
| Triangle | Click to place (corner selectable) |
| Erase | Click to remove |

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| Delete/Backspace | Delete selected |
| Cmd/Ctrl+C | Copy |
| Cmd/Ctrl+X | Cut |
| Cmd/Ctrl+V | Paste |
| Cmd/Ctrl+A | Select all |
| Escape | Deselect |

## Export/Import

Export/import puzzle state as JSON:
```json
{
  "cols": 5,
  "rows": 5,
  "church": { "r": 2, "c": 2 },
  "eyes": { "top:0": true, "right:1": true },
  "buildings": {
    "0,0": { "type": "square" },
    "1,1": { "type": "triangle", "corner": "NE" }
  }
}
```