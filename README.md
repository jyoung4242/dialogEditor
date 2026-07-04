# Skyrelda Dialogue Tree Editor

A powerful, interactive visual dialogue tree editor for creating complex branching conversations with conditional logic, state
management, and playtest capabilities.

## Features

### 🎭 Dialogue Node Creation & Management

- **Create nodes** with speaker names, character portraits, and dialogue text
- **Edit node properties** including automatic transitions and conditional routing
- **Delete nodes** with integrity protection (prevents orphaning the entire tree)
- **Node positioning** on a visual canvas with full drag-and-drop support
- **Automatic naming** with collision detection and kebab-case validation

### 🎯 Branching & Logic

- **Player choices** - Create multiple dialogue options for players to select
- **Conditional routing** - Branch dialogue based on active game flags/state
- **Automatic transitions** - Set nodes to auto-advance to the next node
- **Flag system** - Define and manage global state flags that control dialogue flow
- **Choice modifiers** - Choices can set, require, or complete flags and quests

### 🗺️ Canvas Navigation

- **Zoom controls** - Zoom in/out with buttons or mouse wheel (40%-150%)
- **Pan & drag** - Click and drag to move around the canvas
- **Reset view** - Quickly return to default zoom (100%) and pan (origin)
- **Visual connections** - See dialogue flow with curved bezier paths between nodes

### 🧪 Playtest Mode

- **Real-time testing** - Play through your dialogue tree to test branching logic
- **Flag toggling** - Dynamically enable/disable flags during playtest
- **Conditional evaluation** - See how conditions resolve based on active flags
- **Choice validation** - Test that player choices lead to correct outcomes
- **Flag management** - Restore default flags or clear all flags mid-playtest

### 💾 Import/Export

- **Export JSON** - Download your dialogue tree as a structured JSON file
- **Copy JSON** - Copy dialogue tree data to clipboard for sharing
- **Import JSON** - Load previously saved dialogue trees
- **Format preservation** - Maintains all metadata, positioning, and state

### 🔍 Search & Validation

- **Text search** - Search across all dialogue node content
- **Link validation** - Automatically detect broken references to non-existent nodes
- **Reachability analysis** - Identify nodes that can never be reached from the start node
- **Error reporting** - Clear error messages for import/export issues

## Getting Started

### Opening the Editor

1. Open `index.html` in any modern web browser
2. The editor loads with a sample "Skyrelda" dialogue tree for reference

### Basic Workflow

#### 1. Create Your First Node

- Click the **+ Node** button in the top toolbar
- A new node appears on the canvas at a default position
- Click the node to select it and edit its properties in the right panel

#### 2. Configure Node Content

In the right panel, set:

- **Speaker** - Who is speaking (e.g., "Narrator", "NPC Name")
- **Portrait** - Character portrait identifier
- **Text** - The dialogue content

#### 3. Add Player Choices

- In the **Choices** section, click to add a new choice
- Enter the **Label** (what the player sees)
- Set the **Next Node** (where this choice leads)
- Optionally configure flags the choice requires or sets

#### 4. Choose the Right Routing Type

- Use **Choices** when the player should actively pick what happens next. Each visible choice has its own label, target node, and
  optional flag requirements or effects.
- Use **Conditional Branching** when the story should route automatically based on state. Conditions are checked when a node is
  entered; the first condition whose required flag is active sends the flow to its target before normal player choices are shown.
- Use **Fallback Paths** for the default route when no special player choice or condition applies. In this editor, that usually means
  an **Auto Next** target for a linear continuation, or a deliberate `null` target to end the conversation cleanly.

#### 5. Create Connections

- From a choice, condition, or automatic transition, select a destination node
- Visual curves will show dialogue flow on the canvas
- Use the dropdown to pick from existing nodes

#### 6. Test Your Tree

- Click the **Run Test** button to enter playtest mode
- Start from the beginning and make choices to verify the flow
- Toggle flags to test conditional branching
- Confirm fallback paths still work when no condition matches and no player choice is available
- Exit playtest to return to editing

#### 7. Save Your Work

- Click **Export JSON** to download your dialogue tree
- Click **Copy JSON** to copy to clipboard
- Click **Import** to load a previously saved tree

## Node Properties Reference

### Core Fields

- **Speaker** - Name of the character speaking
- **Portrait** - Portrait identifier for character visualization
- **Text** - Main dialogue content

### Routing Options

- **Choices** - Array of player-selectable dialogue options
  - Each choice has a label and target node reference
  - Use these for explicit player agency: the player decides which visible route to take
  - Choices can require flags, set flags, and start or complete quests
- **Conditions** - Optional automatic branches based on flags
  - Each condition checks for a required flag
  - Conditions are evaluated on node entry before the node is presented for normal choice/auto-next handling
  - If multiple conditions match, the first matching condition's next node is chosen
- **Auto Next** - Optional fallback advancement to the next node
  - Use this for the default path through a linear beat
  - Set it to `null` when the node intentionally ends the conversation

### State Modification

- **Sets Flag** - Node can activate a flag when entered
- **Requires Flag** - Choice/condition only available if flag is active
- **Quest Markers** - Choices can start or complete quests

### Editor Metadata

- **Position (x, y)** - Visual position on the canvas (auto-saved)
- **Search visibility** - All text fields are searchable

## File Format

### JSON Structure

Exported dialogue trees follow this structure:

```json
{
  "id": "conversation-id",
  "startNodeId": "start-node",
  "worldState": {
    "flags": ["flag-one", "flag-two"]
  },
  "nodes": {
    "node-id": {
      "speaker": "Character Name",
      "portrait": "portrait-id",
      "text": "Dialogue text",
      "choices": [
        {
          "label": "Player sees this",
          "nextNodeId": "target-node",
          "requiresFlag": "optional-flag",
          "setsFlag": "flag-set-by-choice"
        }
      ],
      "conditions": [
        {
          "requiresFlag": "required-flag",
          "nextNodeId": "conditional-target"
        }
      ],
      "autoNextNodeId": null,
      "setsFlag": "optional-flag",
      "editorMetadata": {
        "x": 150,
        "y": 200
      }
    }
  }
}
```

### ID Format

- IDs must be **kebab-case** (lowercase letters, numbers, and hyphens)
- Valid: `start-node`, `npc-greeting`, `choice-1`
- Invalid: `Start Node`, `NPC_GREETING`, `choice 1`

## Tips & Best Practices

### Organization

- Use descriptive node IDs that indicate their purpose
- Group related nodes near each other on the canvas for clarity
- Use the search feature to quickly locate dialogue content

### Flag Management

- Define all flags in the **Flags** section before using them
- Use consistent naming conventions (e.g., `has-item-sword`, `met-npc-elder`)
- Keep flag names short and meaningful

### Playtest Strategy

1. Test the "happy path" first (default choices, no conditions)
2. Enable flags individually to test conditional branches
3. Verify that all choices lead to valid nodes
4. Check that no nodes are unreachable from the start

### Performance

- The editor handles large dialogue trees well
- Use reasonable zoom levels for best performance
- Export frequently to prevent accidental data loss

## Browser Compatibility

- Chrome/Edge (recommended)
- Firefox
- Safari
- Any modern browser supporting ES6, React 18, and CSS Grid

## Keyboard Shortcuts

- **Mouse Wheel** - Zoom in/out
- **Left Click + Drag** (on canvas) - Pan view
- **Left Click + Drag** (on node) - Move node
- **Right Click** (context menu) - Available for future expansion

## Troubleshooting

### Import Not Working

- Ensure the JSON file is valid (check for proper formatting)
- Verify the file contains required fields: `id`, `startNodeId`, `nodes`
- Check browser console for specific error messages

### Broken Links Warning

- The editor displays broken links as warnings
- These occur when a choice or condition references a non-existent node
- Fix by selecting a valid target node from the dropdown

### Unreachable Nodes

- Nodes that can't be reached from the start node are highlighted
- Verify these nodes are intentional (endings, fallback states)
- Create choices or conditions that lead to these nodes if they should be reachable

### Data Loss

- Always export or copy your dialogue tree before closing
- The editor uses browser local state (not persistent storage)
- Reload the page will lose unsaved work

## Advanced Usage

### Exporting for Game Integration

1. Export your dialogue tree as JSON
2. Parse the JSON in your game engine
3. Use the node structure to drive your dialogue system
4. The `editorMetadata` can be ignored in production

### Batch Editing

- Export your tree to JSON
- Edit the JSON file directly for bulk changes
- Import the modified file back into the editor

### Multi-Tree Projects

- Create separate dialogue trees for different NPCs or scenes
- Each tree has a unique `id` and `startNodeId`
- Import/export individual trees as needed

## Credits

**Skyrelda Dialogue Tree Editor** - A visual dialogue authoring tool for game developers and narrative designers.

Built with React, Tailwind CSS, and Babel for instant JSX compilation.

---

**Happy writing!** Create engaging, branching dialogues for your game or interactive story. 🎮✍️
