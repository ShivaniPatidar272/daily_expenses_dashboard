# Daily Expense Manager

A personal expense tracker built with React, TypeScript, Vite and Tailwind CSS (originally generated with Figma Make).
Everything runs in the browser: your data is saved in `localStorage` on your own device. There is no server, login or database.

**Live site (after you deploy):** https://shivanipatidar272.github.io/daily_expenses_manager/

## Features

- Dashboard: today / week / month / year totals, expense overview chart (weekly, monthly, yearly), spending by category, top categories, recent expenses, monthly comparison
- Add expenses: date defaults to today (changeable), several items per expense, product autocomplete from previous entries, optional category, amounts in ₹ (INR)
- Expense history: search, filters (dates, category, product, amount), view / edit / delete, CSV export
- Categories: add, rename, delete (renaming updates your history)
- Products: saved product library used for autocomplete, add / rename / remove
- Reports: week / month / year / custom range, average per day, highest day, top category and product, charts
- Settings: your name, JSON backup download and restore, delete all data
- Works on desktop and mobile

## Run it on your computer

You need [Node.js 22](https://nodejs.org) and [pnpm](https://pnpm.io/installation) (`npm install -g pnpm`).

```bash
pnpm install          # install dependencies (uses pnpm-lock.yaml)
pnpm dev              # start the dev server, then open the URL it prints
pnpm typecheck        # check the TypeScript
pnpm build            # production build into dist/
pnpm preview          # serve the production build locally
```

Locally the app runs at `/`. Production builds use the base path `/daily_expenses_manager/`
(set in `vite.config.ts`) so the files load correctly on GitHub Pages.
To deploy under a different repository name, change that one string, or build with `VITE_BASE_PATH=/other-name/ pnpm build`.

## Deploy to GitHub Pages

The workflow in `.github/workflows/deploy.yml` installs dependencies with pnpm, type-checks, builds, and publishes the `dist` folder.

1. Push this project to your repository's `main` branch (see "Uploading" below).
2. On GitHub open **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **GitHub Actions** (not "Deploy from a branch").
4. Open the **Actions** tab and wait for "Deploy to GitHub Pages" to finish (about a minute). You can also start it with **Run workflow**.
5. Visit https://shivanipatidar272.github.io/daily_expenses_manager/

> **Why the page was blank:** with "Deploy from a branch" GitHub serves the *source* `index.html`, which points to `/src/main.tsx`.
> Browsers can't run that file, so nothing renders. The site must be built first and the built `dist` folder published, which is what the workflow does.

## Uploading to your existing repository

**Using the GitHub website (no git needed)**
1. Unzip this project.
2. Open https://github.com/ShivaniPatidar272/daily_expenses_manager and click **Add file → Upload files**.
3. Drag in **everything inside the unzipped folder**, including the hidden `.github` and `.figma` folders. If your file picker hides folders starting with a dot, enable "show hidden files" first (Mac: `Cmd+Shift+.`, Windows: View → Show → Hidden items).
4. Commit directly to `main`.
5. Delete old files that no longer exist in this project if you see leftovers (for example an old `src/App.tsx` is simply replaced; nothing else needs deleting).

**Using git**
```bash
git clone https://github.com/ShivaniPatidar272/daily_expenses_manager.git
cd daily_expenses_manager
# copy the project files over the clone (including .github and .figma), then:
git add -A
git commit -m "Fix GitHub Pages deployment and make the expense manager functional"
git push origin main
```

Then follow "Deploy to GitHub Pages" steps 2–5 above.

## Project structure

```
index.html                    HTML shell (mounts #root, loads src/main.tsx)
vite.config.ts                Vite config, base path for GitHub Pages
.github/workflows/deploy.yml  Build + deploy to GitHub Pages
src/main.tsx                  Entry point (with an error boundary)
src/App.tsx                   App shell, navigation, drawers
src/store.tsx                 App state + automatic saving to localStorage
src/pages/                    Dashboard, AddExpense, Expenses, Categories, Products, Reports, Settings
src/components/               Shared UI (buttons, inputs, modals, charts)
src/lib/                      Dates, INR formatting, statistics, filters, storage + validation
src/index.css                 Styles
```

## Your data

Data lives in your browser's `localStorage` (key `daily-expenses-manager:v1`). Clearing site data or using a different browser/device
starts empty. Use **Settings → Download backup** regularly, and **Restore from backup** to move data between devices.

## Testing checklist (manual)

1. Add an expense with two items, then refresh the page. It should still be there.
2. Type `mi` in a product field after saving "Milk": Milk should be suggested.
3. Edit an expense from **Expenses**, then delete another one.
4. Rename a category and confirm your history shows the new name.
5. Open Reports and switch between Week / Month / Year.
