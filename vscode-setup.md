# VSCODE SETUP NOTES

#### Basic viewing shortcuts

```text
1. CTRL + b (hide left side)
2. CTRL +  j (hide bottom)
3. CTRL + ALT + B (hide the right side)
4. CTRL + + (to increase page size) 
5. CTRL + - (to decrease page size) 
6. CTRL + 0 (to reset the layout) 
```

#### Open VS Code to a blank slate - stop it reopening a closed folder and start fresh

1. Open VS Code.
2. Press `Ctrl + ,` to open Settings.
3. Search for:
   - `restore windows`
4. Find Window: Restore Windows.
5. Change it to `none`.

That tells VS Code not to reopen your previous project/window when you launch it.

Then, if you want an actual blank new editor as well, search Settings for:

`startup editor`

Under Workbench › Startup Editor, you can choose something like:

- `None` - completely empty VS Code window.
- `New Untitled File` - opens with one blank file ready to type in.
- `Welcome Page` - opens the VS Code welcome/start screen.

Blank Slate:
> Window: Restore Windows - `none` <br>
> Workbench: Startup Editor - `welcomePage`