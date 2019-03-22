# Slate Cheatsheet

A quick reference for common actions in a [SlateJS](https://docs.slatejs.org/) Editor.

## Selection

### Select All

```
editor.moveToRangeOfDocument()
```

## Data

### Set Data

```
const data = { alignment: "left" }
editor.setBlocks({data})
```

## Querying

### Find Parent

```
// `key` == the node that you want to find the parent for
const document = editor.value.document
document.getParent(key)
```

## Misc

## Multiple Editors on the Same Page

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
