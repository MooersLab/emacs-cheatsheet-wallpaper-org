# Why Your PDF Compiled to Letter Size (NOT Content Size)

## The Problem

Your LaTeX log shows:
```
Document Class: article 2024/06/29 v1.4n Standard LaTeX document class
```

It should show:
```
Document Class: standalone
```

**This means the `standalone` class is NOT being used.**

---

## Root Cause

You **didn't answer 'y'** to the local variables prompt when you opened the file in Emacs.

Without answering 'y':
- Local variables don't run
- The `standalone` class is never added to `org-latex-classes`
- Org-mode defaults to using `article` class
- Article class creates US Letter (8.5" x 11") pages

---

## Solution 1: Answer 'y' to the Prompt ⭐ EASIEST

### Step 1: Close the File
```
C-x k   (kill-buffer)
```

### Step 2: Reopen the File
```
emacs EmacsCheatSheet_FRIENDLY.org
```

### Step 3: You'll See This Prompt

```
The local variables list in EmacsCheatSheet_FRIENDLY.org
contains values that may not be safe (*).

  * eval: (add-to-list 'org-latex-classes ...)

Do you want to apply it?  You can type
y  -- to apply the local variables list.
n  -- to ignore the local variables list.
!  -- to apply and mark as safe permanently.
```

### Step 4: Type `y` and Press Enter

**You MUST do this!** If you type `n` or just press Enter, it won't work.

### Step 5: Verify It Worked

Check if the class was added:
```
M-: (assoc "standalone" org-latex-classes)
```

Press `Enter`. 

**If you see `nil`** → Didn't work, try again
**If you see something else** → Success!

### Step 6: Export
```
C-c C-e l p
```

---

## Solution 2: Use the BIND Method (Alternative)

If local variables keep failing, use `EmacsCheatSheet_BIND_METHOD.org`

This file uses `#+BIND` instead of local variables:
```org
#+BIND: org-latex-classes (cons '("standalone" "\\documentclass{standalone}") org-latex-classes)
```

**Advantage:** Works even if local variables are disabled

**Export:** Same way - `C-c C-e l p`

---

## Solution 3: Add to Your Emacs Config (Permanent)

Add this to `~/.emacs` or `~/.emacs.d/init.el`:

```elisp
(with-eval-after-load 'ox-latex
  (add-to-list 'org-latex-classes
    '("standalone" 
      "\\documentclass{standalone}"
      ("\\section{%s}" . "\\section*{%s}")
      ("\\subsection{%s}" . "\\subsection*{%s}"))))
```

Then:
1. Restart Emacs OR run `M-x eval-buffer`
2. You can now **delete** the local variables from the bottom of your org file
3. Export normally: `C-c C-e l p`

**Advantage:** Works for all files, no prompt needed

---

## Solution 4: Test with Simple File First

Use `test_standalone.org` to verify standalone works:

```bash
emacs test_standalone.org
```

1. Answer `y` to the prompt
2. Export: `C-c C-e l p`
3. Check the PDF size

**If the PDF is tiny (just the text size)** → Standalone works! ✅
**If the PDF is US Letter size** → Standalone not working ❌

---

## How to Tell If It Worked

### After Opening the File (Before Export):

Check if standalone class was added:
```
M-: (assoc "standalone" org-latex-classes)
```

Should return something like:
```
("standalone" "\\documentclass{standalone}" ...)
```

If it returns `nil`, it didn't work.

### After Export:

Look at the `.tex` file that org-mode generated:
```bash
head -1 EmacsCheatSheet_FRIENDLY.tex
```

Should show:
```latex
\documentclass{standalone}
```

If it shows `\documentclass[11pt]{article}`, it didn't work.

### Check the PDF:

**Content-sized PDF:**
- Width and height match your content
- No white margins around edges
- Perfect for wallpapers

**Letter-sized PDF:**
- 8.5" × 11" (US Letter)
- Big white margins
- Content centered on page

---

## Common Mistakes

### ❌ Mistake 1: Pressing Enter Instead of 'y'

The prompt defaults to `n` (no). If you just press Enter without typing `y`, the local variables won't apply.

**Fix:** Type `y` explicitly

---

### ❌ Mistake 2: Answering 'n' by Accident

If you answer `n`, org-mode remembers your choice for the session.

**Fix:** Close and reopen the file, answer `y` this time

---

### ❌ Mistake 3: Local Variables Disabled in Emacs

Some Emacs configs disable local variables for security.

**Check your config for:**
```elisp
(setq enable-local-variables nil)  ; ← This disables them
```

**Fix:** Change to:
```elisp
(setq enable-local-variables t)    ; ← This enables them
```

Or use the BIND method instead (Solution 2)

---

### ❌ Mistake 4: Not Restarting Emacs After Config Change

If you added the standalone class to your `~/.emacs`, you need to restart Emacs or run `M-x eval-buffer`.

**Fix:** Restart Emacs

---

## Debugging Checklist

Run through these checks:

1. ☐ Opened file in Emacs
2. ☐ Saw the local variables prompt
3. ☐ Typed `y` and pressed Enter
4. ☐ Ran `M-: (assoc "standalone" org-latex-classes)` and saw non-nil result
5. ☐ Exported with `C-c C-e l p`
6. ☐ Checked generated `.tex` file has `\documentclass{standalone}`
7. ☐ Resulting PDF is content-sized, not letter-sized

If any step fails, that's where the problem is!

---

## Files Provided

1. **`test_standalone.org`** - Simple test file (use this first!)
2. **`EmacsCheatSheet_FRIENDLY.org`** - Full version with local variables
3. **`EmacsCheatSheet_BIND_METHOD.org`** - Alternative using #+BIND

**Recommendation:** 
1. Test with `test_standalone.org` first to verify standalone works
2. Once confirmed, use the full `EmacsCheatSheet_FRIENDLY.org`

---

## Still Not Working?

If you've tried everything and it still compiles to letter size:

### Last Resort Option:

Just use the `.tex` file directly:
```bash
pdflatex EmacsCheatSheet3.tex
```

The `.tex` file already has `\documentclass{standalone}` at the top, so it will always work.

**You don't NEED to use org-mode** - the `.tex` file works perfectly on its own!

---

## Summary

**Most common cause:** Not answering `y` to the local variables prompt

**Quick fix:** 
1. Close and reopen the file
2. Type `y` when prompted
3. Export

**Permanent fix:**
- Add standalone class to your `~/.emacs` config
- Never need to answer the prompt again

**Alternative:**
- Use `EmacsCheatSheet_BIND_METHOD.org` (works without local variables)
- Or just use the `.tex` file directly with `pdflatex`
