# Common Issues

These are common issues that people run into when using SlateJS

## Pressing Enter Copies the Block

By default, Slate runs `splitBlock` when you press enter. This will copy the data from your current block and create a new one of the same type. This is why pressing enter in an image could cause the image to be duplicated. Instead, you may need to do something like this when the user presses enter:

```
editor.splitBlock().setBlocks("paragraph")
```
