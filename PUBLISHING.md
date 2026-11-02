# Publishing notes to the website

Live site: https://henrykgo.github.io/software-engineering-notes

## After editing notes in Obsidian

**1. Copy the vault into the site folder**

```bash
rsync -a --delete --exclude '.obsidian' --exclude '.DS_Store' --exclude 'index.md' ~/Desktop/"Software Engineering Notes"/"Software Engineering"/ ~/Desktop/software-engineering-notes/content/
```

- `--delete` removes notes you deleted or renamed in Obsidian.
- `--exclude 'index.md'` protects the home page, which only exists in `content/`.

**2. (Optional) Preview locally**

```bash
cd ~/Desktop/software-engineering-notes && npx quartz build --serve
```

Open http://localhost:8080 and press `Ctrl+C` to stop.

**3. Push to GitHub**

```bash
cd ~/Desktop/software-engineering-notes && git add . && git commit -m "Update notes" && git push
```

Or use `npx quartz sync`, which does the same with an automatic commit message.

**4. Check the deploy**

Open the repo's **Actions** tab on GitHub. When "Deploy to GitHub Pages" is green (about 1 minute), the site is updated. If the page looks unchanged, hard-refresh with `Cmd+Shift+R`.

## After changing how the site looks

Edit `quartz.config.yaml` (title, colours, plugins) or `quartz/styles/custom.scss` (CSS). Then do steps 2 to 4 above.

## If something goes wrong

| Problem | Check |
|---|---|
| Site didn't change | Did step 1 run? Is the Actions run green? |
| Actions run is red | Click it, open the failed step, and read the error (it names the file and line). |
| `git push` fails | Run `git remote -v`. `origin` must be `Henrykgo/software-engineering-notes`. |
| "nothing to commit" | rsync found no changes. Did you save in Obsidian? |
