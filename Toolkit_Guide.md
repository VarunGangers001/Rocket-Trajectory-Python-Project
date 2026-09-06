# Your Software Toolkit — Plain-English Guide

## Start here: the one idea that unlocks everything

You're juggling five separate tools. None of them talk to each other automatically — none of them "know" you're working on CubeSat vs Rocket vs anything else. Each one just does its own narrow job:

| Tool | Its ONE job | Does NOT do |
|---|---|---|
| **Conda (`aerospace` env)** | Gives you a Python installation + packages (NumPy, SciPy, Pandas, Matplotlib, Jupyter) | Doesn't know or care where your project files are |
| **Your project folder** | Holds your actual work (code, notes, CAD, etc.) | Doesn't run anything by itself |
| **Obsidian** | A nice editor for the Markdown notes sitting in your project folder | Doesn't store anything separately — it just opens your folder |
| **Git** | Keeps a history of changes to your project folder | Only works on files, doesn't touch Conda or Obsidian |
| **GitHub** | An online copy/backup of your Git history | Just storage — you have to explicitly send things to it |

**The single most important sentence in this whole guide:** activating Conda does not decide where your files get saved. Only your *current terminal location* (and any paths you write in your code) decide that. Conda ≠ file location.

Everything below is really just detail on top of that one idea.

---

## The daily routine (memorize this, skip everything else)

This sequence covers ~90% of what you'll actually do, every session:

```bash
conda activate aerospace                                                    # (1)
cd "$HOME/Varun's Folder of Epicness/Projects/CubeSat-Personal-Project"     # (2)
pwd                                                                          # (3)
git status                                                                   # (4)
code .                                                                       # (5)

# ... do your work: edit notes in Obsidian, run scripts, use Jupyter ...

git status                                                                   # (6)
git add .                                                                    # (7)
git commit -m "Describe what you changed"                                   # (8)
git push                                                                     # (9)
conda deactivate                                                             # (10)
```

What each line does:
1. Turns on your Python toolbox for this terminal session
2. Moves your terminal into the CubeSat project (swap the path for Rocket when needed)
3. Confirms where you are ("print working directory")
4. Shows the current state of your Git repo before you start
5. Opens the whole project folder in VS Code
6. Shows what you changed while working
7. Stages everything you changed, ready to save
8. Saves a checkpoint with a description
9. Sends that checkpoint to GitHub
10. Cleanly exits the Python environment

Rocket project uses the exact same steps — just swap the path in line 2 for:
```bash
cd "$HOME/Varun's Folder of Epicness/Projects/Rocket-Trajectory-Python-Project"
```

> Note: paths have spaces and an apostrophe, so always wrap them in quotes as shown above.

You do **not** need `conda activate` just to write Obsidian notes or look at CAD — only when you need Python, Jupyter, or scientific packages.

---

## Reference section — come back here when something's unclear

### 1. Conda — think of it as a labelled toolbox

You have one toolbox called `aerospace`, containing Python 3.13 plus NumPy, SciPy, Pandas, Matplotlib, and Jupyter.

| Command | What it does |
|---|---|
| `conda env list` | Show all toolboxes you have |
| `conda activate aerospace` | Start using this toolbox |
| `conda deactivate` | Stop using it |
| `conda list` | See what's inside the active toolbox |
| `conda install <package>` | Add something to the toolbox |
| `pip install <package>` | Fallback if Conda doesn't have it — use inside the environment, never with `sudo` |
| `which python` | Confirm which Python you're actually running |
| `python --version` | Confirm the version |

`which python` should point somewhere inside `~/miniconda3/envs/aerospace/` when the environment is active. If it doesn't, that's your first troubleshooting clue.

### 2. Where do files actually get saved?

Whatever folder your terminal is sitting in (`pwd`) is where new files land — Python has no idea what "the CubeSat project" is.

Example: if you're in the CubeSat folder and your script has:
```python
plt.savefig("orbit.png")
```
you'll get `CubeSat-Personal-Project/orbit.png` — even if the script itself lives in a `Calculations/` subfolder.

To avoid surprises, be explicit:
```python
plt.savefig("Calculations/figures/orbit.png", dpi=300)
```

### 3. Jupyter vs. `.py` scripts

- **Jupyter notebook** (`.ipynb`) → messing about, exploring, plotting, testing ideas
- **`.py` script** → the "real" reusable version once you know what you're doing

Start Jupyter from inside the project (after activating Conda):
```bash
jupyter lab
```
It's just a file too — `Calculations/Orbit Analysis.ipynb` — so Git tracks it like anything else.

### 4. Obsidian — simpler than it looks

Your CubeSat and Rocket folders **are** your Obsidian vaults. There's no separate "Obsidian storage" — when you edit a note in Obsidian, you're editing a real Markdown file sitting in your project folder, which Git can then track like any other file.

Don't create a second copy of the project just for Obsidian — just open the existing folder as a vault.

### 5. Git vs. GitHub — the actual difference

Think of it like a video game save system:
- **Git** = the save system running on your own laptop. It records checkpoints ("commits") of your project over time, so you can look back.
- **GitHub** = the cloud slot where you upload those saves so they're backed up and accessible elsewhere.

The four commands you'll use constantly:

| Command | What it does |
|---|---|
| `git status` | "What's changed since my last checkpoint?" |
| `git add .` | "Mark all of that as ready to save" |
| `git commit -m "message"` | "Save a checkpoint, with a note describing it" |
| `git push` | "Upload that checkpoint to GitHub" |
| `git pull` | "Download the latest checkpoint from GitHub" (use if you've worked from another machine) |

A commit only exists on your laptop until you `push` it — that's the most common beginner trip-up ("I committed but GitHub didn't change" → you just forgot to push).

Other useful checks:
```bash
git log --oneline -10     # recent commit history
git remote -v             # which GitHub repo you're connected to
```

**Write commit messages that describe the actual change:**

✅ `Add preliminary orbit calculation`, `Fix orbital propagation bug`, `Update power budget assumptions`
❌ `stuff`, `update`, `final final FINAL`

### 6. What should and shouldn't go into Git

**Commit:** notes, scripts, notebooks, specs, figures, CAD source files, reports, diagrams, `README.md`, `environment.yml`.

**Don't commit:** `__pycache__/`, `*.pyc`, `.ipynb_checkpoints/`, `.venv/` — a `.gitignore` file tells Git to ignore these automatically.

**Never commit:** passwords, API keys, or any other secrets.

### 7. Saving your Conda environment (do this occasionally, not constantly)

Once your environment is set up the way you like it:
```bash
conda activate aerospace
conda export --from-history --format=environment-yaml --file=environment.yml
```
This creates `environment.yml` inside your project, which you can commit to Git — it lets you (or anyone else) recreate the exact same environment on another machine later. Only redo this when your dependencies meaningfully change.

---

## Getting un-lost

| Problem | Run this |
|---|---|
| Don't know where your terminal is | `pwd` |
| Don't know what's in the current folder | `ls` |
| "Python can't find NumPy/SciPy" | `conda activate aerospace` then `which python` then `python -c "import numpy, scipy; print('Working')"` |
| "I can't find the file I just made" | `pwd` and `ls` — you're probably in a different folder than you think |
| "Git says nothing changed" | `pwd` then `git status` — you may be in the wrong repository |
| "I committed, but GitHub didn't change" | Run `git push` — a commit is local until pushed |
| "I don't know what repo I'm in" | `git remote -v` |
| "I don't know where Python is coming from" | `which python` |

If Git ever reports a **conflict**: don't panic, don't delete anything — stop and read the message before doing anything else.

---

## Navigating to your project folders

You don't need to type the full path every time:
```bash
cd "$HOME/Varun's Folder of Epicness/Projects"
ls
```
This shows both `CubeSat-Personal-Project` and `Rocket-Trajectory-Python-Project` — then just `cd` into whichever one you need.

Other handy navigation:
```bash
cd ..    # go up one folder
cd ~     # go straight home
pwd      # where am I?
ls       # what's here?
```

Opening a project once you're inside it:
```bash
code .        # open in VS Code
xdg-open .    # open in your file manager
```

---

## Full command cheat sheet

**Navigation**
```bash
pwd
ls
cd "<path>"
cd ..
cd ~
```

**Conda**
```bash
conda env list
conda activate aerospace
conda deactivate
conda list
which python
python --version
```

**Python**
```bash
python script.py
python -c "import numpy; print(numpy.__version__)"
```

**Jupyter**
```bash
jupyter lab
```

**Git**
```bash
git status
git add .
git commit -m "Describe change"
git push
git pull
git log --oneline -10
git remote -v
```

**Environment file**
```bash
conda export --from-history --format=environment-yaml --file=environment.yml
```

---

## The pattern that carries into your MSc

Every future project — MSc included — follows the same shape:

1. `cd` into the project
2. `conda activate <environment>`
3. Work: Obsidian for notes, VS Code for code, Jupyter for exploration, CAD software for CAD, Git for history
4. `git status` to check what changed
5. `git add .` and `git commit -m "..."` to checkpoint it
6. `git push` to back it up

**The five-line mental model, one more time:**
> Conda provides the software.
> Your project folder contains the work.
> Obsidian is your notebook.
> Git records history.
> GitHub stores it remotely.

Once those five click, the rest is just muscle memory.
