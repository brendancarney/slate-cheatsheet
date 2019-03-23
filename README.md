# Slate Cheatsheet

A quick reference for common actions in a [SlateJS](https://docs.slatejs.org/) Editor.


## Commands

### Chaining
To make a series of commands without being interrupted by normalization:

```
// normalization is run after the delegate returns
editor.withoutNormalizing(() => {
    editor.splitBlock().setBlocks({ type: "paragraph", data: {}})
}
```


## Selection

### Modifying

#### Select All

```
editor.moveToRangeOfDocument()
```

#### Save and Restore Selection
```
// Save selection before focusing on something else
const selection = editor.value.selection

// Restore editor selection later on
editor.change(change => change.select(selection))
```

### Analyzing

#### Basic

```
// also has start, end, anchor
const { key, offset, path } = editor.value.selection.focus
```

#### Selection is in a block of a given type

```
const type = "paragraph"
const isInType = editor.value.blocks(block => block.type === type)
```

#### Selection is directly after an inline of a given type

```
const previous = editor.value.document.getPreviousSibling(editor.value.focusText.key)
const isAfter = previous.type === type && editor.value.focus.offset === 0
```

## Data

### Set Data

```
const data = { alignment: "left" }
editor.setBlocks({data})
```

### Merge Data

```
const data = { alignment: "left" }
editor.setNodeByKey(node.key, { data: node.data.merge(data)})
```

## Querying

### Find Parent

```
// `key` == the node that you want to find the parent for
const document = editor.value.document
document.getParent(key)
```

### Search for `node` in a `nodes` collection

```
const parent = editor.value.document.getParent(node.key)
// See Immutable JS List for other search functions
const index = parent.nodes.indexOf(node);
```

## Misc

### Analyze changes made to the value in `onChange`

```
onChange = (change) => {
  const opTypes = change.operations.map(operation => operation.type)
}
```

### Check if a node is empty
```
node.text === ""
```

### Check if the current line is empty
```
editor.value.startBlock.text === ""
```

### Multiple Editors on the Same Page

```
import { Value } from "slate"
import initialValue from "./json-value.json"
// This value can only be used in one `Editor` component.
const value1 = Value.fromJSON(initialValue)
// If we want to use the same initial value, we create a new one:
const value2 = Value.fromJSON(initialValue)

<Editor value={value1}>
<Editor value={value2}>
```
