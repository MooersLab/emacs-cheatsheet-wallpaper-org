![Version](https://img.shields.io/static/v1?label=EmacsWallPaper&message=0.1&color=brightcolor)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
![Org-Mode Friendly](https://img.shields.io/badge/Org--Mode-Friendly-green)

# Emacs Keybindings Desktop Wallpaper

> A customizable Emacs cheat sheet overlay on your favorite background image — available in both LaTeX and Org-mode formats!

Create a desktop wallpaper displaying your most-used Emacs keybindings overlaid on a background image. Perfect for learning, reference, or sharing your Emacs workflow. Designed to be beginner-friendly for org-mode users who may be uncomfortable with raw LaTeX.

<p align="center"><img src="EmacsCheatSheet.png" alt="Emacs Cheatsheet Example" width="1200" height="600"/></p>

---

## 🌟 Features

- **Two formats available:**
  - [`EmacsCheatSheet.tex`](https://github.com/MooersLab/emacs-wallpaper-3) - Pure LaTeX file for LaTeX users
  - `EmacsCheatSheet.org` - Org-mode friendly version with detailed instructions
- **Custom background image** - Use your own wallpaper
- **Exact-size PDF output** - No margins, perfect for wallpapers (using `standalone` document class)
- **Self-contained** - Org-mode version requires no Emacs configuration changes
- **Fully customizable** - Change keybindings, colors, positions, and text size
- **Extensively documented** - Comments and instructions throughout

---

## 📋 Table of Contents

- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
  - [For LaTeX Users](#for-latex-users)
  - [For Org-Mode Users](#for-org-mode-users)
- [Detailed Tutorial](#detailed-tutorial)
  - [Using the LaTeX File](#tutorial-1-using-the-latex-file)
  - [Using the Org-Mode File](#tutorial-2-using-the-org-mode-file)
- [Customization Guide](#customization-guide)
- [File Structure](#file-structure)
- [Troubleshooting](#troubleshooting)
- [FAQ](#faq)
- [Contributing](#contributing)
- [Compatibility](#compatibility)
- [Update History](#update-history)
- [License](#license)
- [Funding](#funding)

---

## 🔧 Prerequisites

### For LaTeX Version (.tex file):
- LaTeX distribution installed (TeX Live, MiKTeX, or MacTeX)
- Packages: `standalone`, `graphicx`, `xcolor`, `tikz`, `array`, `parskip`
- Or use [Overleaf](https://www.overleaf.com/) (online LaTeX editor)

### For Org-Mode Version (.org file):
- Emacs (version 26+)
- Org-mode (included with Emacs)
- LaTeX distribution (for PDF export)

---

## 🚀 Quick Start

### For LaTeX Users

1. **Download** `EmacsCheatSheet3.tex`
2. **Edit** the image path (line 18):
   ```latex
   \includegraphics[width=3.5\textwidth]{~/Pictures/ChineseWall3.png}
   ```
   Change to your image path.
3. **Compile:**
   ```bash
   pdflatex EmacsCheatSheet3.tex
   ```
4. **Done!** Your PDF is ready.

### For Org-Mode Users

1. **Download** `EmacsCheatSheet_FRIENDLY.org`
2. **Open** in Emacs:
   ```
   emacs EmacsCheatSheet_FRIENDLY.org
   ```
3. **Trust the file:** When prompted about local variables, type `y` and press Enter
4. **Edit** the image path (line 38)
5. **Export:** Press `C-c C-e l p`
6. **Done!** Your PDF is ready.

---

## 📚 Detailed Tutorial

### Tutorial 1: Using the LaTeX File

#### Step 1: Prepare Your Background Image

Choose or create a background image (PNG, JPG, or PDF). Place it somewhere accessible, like:
```
~/Pictures/ChineseWall3.png
```

#### Step 2: Download and Open the File

Download `EmacsCheatSheet3.tex` and open it in your favorite text editor or LaTeX IDE.

#### Step 3: Customize the Image Path

Find line 18:
```latex
\node at (0,0) {\includegraphics[width=3.5\textwidth]{~/Pictures/ChineseWall3.png}};
```

Change the path to your image:
```latex
\node at (0,0) {\includegraphics[width=3.5\textwidth]{/full/path/to/your/image.png}};
```

#### Step 4: Edit Keybindings (Optional)

Find the keybinding sections (lines 22-241). Each entry follows this pattern:
```latex
C-x C-c & Exit. \\
```

- **Before `&`** = Keybinding
- **After `&`** = Description
- **`\\`** = End of line (required!)

**To add a new keybinding:**
```latex
C-x C-c & Exit. \\
C-x k & Kill buffer. \\  ← Add this line
```

**To remove a keybinding:** Simply delete the entire line.

#### Step 5: Compile

##### Option A: Command Line
```bash
pdflatex EmacsCheatSheet3.tex
```

##### Option B: In Emacs
Open the file and press: `C-c C-c` (if using AUCTeX)

##### Option C: Online (Overleaf)
1. Upload `EmacsCheatSheet3.tex` to Overleaf
2. Upload your background image
3. Click "Recompile"

#### Step 6: Set as Wallpaper

The generated `EmacsCheatSheet3.pdf` is exactly the size of your content. Convert to PNG if needed:
```bash
convert -density 300 EmacsCheatSheet3.pdf EmacsCheatSheet3.png
```

---

### Tutorial 2: Using the Org-Mode File

> **Perfect for org-mode users who are uncomfortable with LaTeX!**

#### Step 1: Open the File in Emacs

```bash
emacs EmacsCheatSheet_FRIENDLY.org
```

#### Step 2: Trust the Local Variables

When you first open the file, Emacs will show a prompt:

```
The local variables list in EmacsCheatSheet_FRIENDLY.org
contains values that may not be safe (*).

Do you want to apply it?  You can type
y  -- to apply the local variables list.
n  -- to ignore the local variables list.
!  -- to apply and mark as safe permanently
```

**Type `y` and press Enter.**

**What does this do?** The local variables at the bottom of the file tell org-mode to use the `standalone` document class, which creates a PDF exactly the size of your content (not US Letter).

**Is it safe?** Yes! The local variables just add a document class definition. You can view them at the bottom of the file.

#### Step 3: Change Your Background Image

Press `C-s` to search for: `CHANGE THIS PATH`

Find line 38:
```latex
\includegraphics[width=3.5\textwidth]{~/Pictures/ChineseWall3.png}
```

Change it to your image path:
```latex
\includegraphics[width=3.5\textwidth]{/Users/yourname/Desktop/myimage.png}
```

**Tip:** Use absolute paths (full path) to avoid issues.

#### Step 4: Edit Your Keybindings

Scroll down to the LaTeX content blocks. You'll see sections like:

```latex
\noindent{\bfseries Undo, Save, Exit} & \\
    C-u n & Repeat $<$comand$>$ n times.\\ 
    C-g & No do last command. \\
    C-x C-c & Exit. \\
```

**To edit:**
- Text before `&` = Keybinding
- Text after `&` = What it does
- `\\` at the end = End of line (keep this!)

**To add a keybinding:**
```latex
C-x C-c & Exit. \\
C-x k & Kill buffer. \\  ← Add your new line
```

**Don't worry about the LaTeX syntax** - just follow the pattern!

#### Step 5: Export to PDF

Press: **`C-c C-e l p`**

Or use the menu: **Export → Export to LaTeX → As PDF file and open**

Emacs will:
1. Generate a `.tex` file from your org file
2. Compile it with LaTeX
3. Create a PDF exactly the size of your content
4. Open it for you to view

#### Step 6: Find Your PDF

The PDF is saved in the same directory as your `.org` file with the same name:
```
EmacsCheatSheet_FRIENDLY.pdf
```

---

## 🎨 Customization Guide

### Changing the Background Image

**LaTeX file (line 18):**
```latex
\node at (0,0) {\includegraphics[width=3.5\textwidth]{your-image.png}};
```

**Org file (line 38):**
```latex
\node at (0,0) {\includegraphics[width=3.5\textwidth]{your-image.png}};
```

### Changing Text Color

Find this line (line 36 in org file):
```latex
\color{lime}
```

Change `lime` to any of these colors:
- Standard: `white`, `black`, `red`, `blue`, `green`, `yellow`, `cyan`, `magenta`
- Semi-transparent: `white!80` (80% opacity), `black!50` (50% opacity)

### Changing Text Size

Find `\begin{footnotesize}` in the file and change to:
- `\begin{tiny}` - Smallest
- `\begin{scriptsize}` - Very small
- `\begin{footnotesize}` - Small (current)
- `\begin{small}` - Slightly smaller than normal
- `\begin{normalsize}` - Normal
- `\begin{large}` - Large
- `\begin{Large}` - Larger
- `\begin{LARGE}` - Very large
- `\begin{huge}` - Huge
- `\begin{Huge}` - Largest

### Moving the Text Overlay

Find this line:
```latex
\node at (1.02,0) {
```

Change `(1.02,0)` to different coordinates:
- **First number** (horizontal): Higher = further right
- **Second number** (vertical): Higher = further up

Examples:
- `(0,0)` - Center
- `(2,0)` - Right of center
- `(-1,0)` - Left of center
- `(1.02,2)` - Right and up

### Changing Column Widths

Find `\begin{minipage}{270pt}` and change `270pt` to:
- `200pt` - Narrower
- `300pt` - Wider
- `350pt` - Much wider

### Adding a Semi-Transparent Background to Text

Wrap your table in a color box:
```latex
\colorbox{white!90}{%  % 90% white (10% transparent)
  \begin{minipage}{270pt}
    \begin{tabular}{ll}
      Your keybindings here...
    \end{tabular}
  \end{minipage}%
}
```

---

## 📁 File Structure

```
EmacsWallPaper/
├── EmacsCheatSheet3.tex              # Pure LaTeX version
├── EmacsCheatSheet_FRIENDLY.org      # Org-mode friendly version
├── EmacsCheatsheet3.png              # Example output image
├── README.md                          # This file
└── ChineseWall3.png                  # Example background image
```

### What's in Each File?

**`EmacsCheatSheet3.tex`**
- Pure LaTeX file
- Uses `standalone` document class
- Compile with: `pdflatex EmacsCheatSheet3.tex`
- For users comfortable with LaTeX

**`EmacsCheatSheet_FRIENDLY.org`**
- Org-mode file with instructions
- Self-contained (uses local variables)
- Export with: `C-c C-e l p` in Emacs
- For org-mode users, LaTeX-phobic users
- Has detailed comments and customization tips

---

## 🔍 Troubleshooting

### Problem: "Two \\documentclass commands" error

**Cause:** You tried to put the entire `.tex` file inside `#+BEGIN_EXPORT latex` in org-mode.

**Solution:** Use the provided `EmacsCheatSheet_FRIENDLY.org` file, which is properly structured for org-mode export.

---

### Problem: Image not found / "File not found" error

**Cause:** LaTeX can't find your background image.

**Solutions:**
1. Use an **absolute path**: `/Users/yourname/Pictures/image.png`
2. Use `~` expansion: `~/Pictures/image.png` 
3. Or place the image in the **same directory** as your `.tex` or `.org` file

**Test if path works:**
```bash
ls -l ~/Pictures/ChineseWall3.png
```
If you get "No such file or directory", the path is wrong.

---

### Problem: PDF is US Letter size, not content size

**Cause:** The `standalone` document class isn't being used.

**For .tex file:**
- Check line 1 is: `\documentclass[10.5pt]{standalone}`

**For .org file:**
- Did you answer `y` to the local variables prompt?
- Check line has: `#+LATEX_CLASS: standalone`
- Try closing and reopening the file, answer `y` again
- Or add to your `~/.emacs`:
```elisp
(with-eval-after-load 'ox-latex
  (add-to-list 'org-latex-classes
    '("standalone" "\\documentclass{standalone}")))
```

---

### Problem: Text not visible on the image

**Cause:** Text color blends with background.

**Solution:** Change text color or add a semi-transparent background box:

```latex
\color{white}  % or \color{black}, \color{yellow}, etc.
```

Or wrap in a colorbox:
```latex
\colorbox{white!90}{%  % Semi-transparent white background
  Your content here
}
```

---

### Problem: "Overfull \\hbox" warnings

**Cause:** Text or image is too wide for the container.

**Solutions:**
1. Reduce minipage width: `\begin{minipage}{250pt}` (was 270pt)
2. Reduce image width: `width=3.0\textwidth` (was 3.5)
3. Use smaller text: `\begin{scriptsize}` instead of `\begin{footnotesize}`

---

### Problem: Emacs won't let me answer 'y' to local variables

**Cause:** Your Emacs might have local variables disabled.

**Solution:** Add to `~/.emacs`:
```elisp
(setq enable-local-variables t)
```

Or answer `!` instead of `y` to mark as safe permanently.

---

## ❓ FAQ

### Q: Do I need to modify my Emacs configuration?

**A:** No! The org-mode version uses local variables at the bottom of the file. Just answer `y` when prompted.

### Q: Will this affect my other org files?

**A:** No! Local variables only affect the file they're in. Your other org files work normally.

### Q: Can I use this with Overleaf?

**A:** Yes! Upload `EmacsCheatSheet3.tex` and your background image to Overleaf and compile.

### Q: The local variables prompt appears every time. How do I stop this?

**A:** Answer `!` (exclamation point) instead of `y` - this marks the variables as safe permanently.

Or add to `~/.emacs`:
```elisp
(with-eval-after-load 'ox-latex
  (add-to-list 'org-latex-classes
    '("standalone" "\\documentclass{standalone}")))
```
Then you can delete the local variables from the bottom of the org file.

### Q: What's the difference between the .tex and .org files?

**A:**
| Feature | .tex file | .org file |
|---------|-----------|-----------|
| LaTeX knowledge required | High | Low |
| Self-documented | No | Yes (instructions included) |
| Org-mode workflow | No | Yes |
| Emacs config needed | No | No (uses local variables) |
| Compilation method | `pdflatex` | `C-c C-e l p` |

**Both produce the same PDF output!** Choose based on your comfort level.

### Q: Can I share this with others?

**A:** Yes! 
- **LaTeX version:** Just send the `.tex` file. They compile with `pdflatex`.
- **Org-mode version:** Send the `.org` file. They open in Emacs and answer `y` to the prompt.

### Q: How do I convert the PDF to PNG for my wallpaper?

**A:** Use ImageMagick:
```bash
convert -density 300 EmacsCheatSheet.pdf EmacsCheatSheet.png
```

Or use Preview (Mac), GIMP, or Photoshop.

### Q: The keybindings don't work with my Emacs config!

**A:** This cheat sheet uses keybindings from a [specific Emacs configuration](https://codeberg.org/MooersLab/emacs30init). Some keybindings may be different in your setup.

To check a keybinding in your Emacs:
```
C-h k [keybinding]
```

For example: `C-h k C-x C-c` shows what `C-x C-c` does in your configuration.

---

## 🤝 Contributing

Contributions are welcome! Here are some ways you can help:

- **Report bugs:** Open an issue describing the problem
- **Add keybindings:** Submit a PR with useful keybindings
- **Improve documentation:** Fix typos or clarify instructions
- **Share templates:** Create variations with different layouts

### How to Contribute:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes
4. Test your changes (compile both .tex and .org files)
5. Submit a pull request

---

## 🔗 Compatibility

### Tested With:

- **LaTeX:** TeX Live 2023, MiKTeX 23.10, MacTeX 2023
- **Emacs:** 26.3, 27.2, 28.2, 29.1, 30.0
- **Org-mode:** 9.5+
- **Operating Systems:** Linux, macOS, Windows

### Related Emacs Configuration:

The keybindings in this cheat sheet work with this [Emacs configuration](https://codeberg.org/MooersLab/emacs30init). You can run it using the `--init-directory` flag in Emacs 29+:

```bash
emacs --init-directory=/path/to/emacs30init
```

---

## 📜 Update History

| Version | Changes | Date |
|:-------:|:--------|:----:|
| Version 0.1| Added org-mode friendly version with local variables; extensive documentation; customization guides | 2025 February 4 |

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2025 [Your Name]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

---

## 💰 Funding

This work was supported by:
- NIH: R01 CA242845, R01 AI088011
- NIH: P30 CA225520 (PI: R. Mannel)
- NIH: P30 GM145423 (PI: A. West)

---

## 🙏 Acknowledgments

- Thanks to all contributors and users
- Background image credit: [Add your credit here]
- Inspired by the need for accessible Emacs learning materials

---

## 📞 Contact & Support

- **Issues:** [GitHub Issues](https://github.com/MooersLab/EmacsWallPaper/issues)
- **Discussions:** [GitHub Discussions](https://github.com/MooersLab/EmacsWallPaper/discussions)
- **Email:** [your.email@example.com]

---

## ⭐ Star This Repository

If you find this useful, please give it a star! It helps others discover the project.

---

<p align="center">Made with ❤️ for the Emacs community</p>
