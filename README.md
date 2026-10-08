# PersonalPortfolio

Personal engineering portfolio for Sam Heller. Plain static site: hand-written HTML, one CSS file, and a few lines of JS. No build step, no frameworks, no Jekyll (`.nojekyll` at the root turns Jekyll off).

All paths are relative, so the site works on GitHub Pages and when you open `index.html` straight from disk.

```
index.html                home page
projects/*.html           one page per project
css/style.css             the only stylesheet
js/main.js                mobile nav toggle
favicon.svg               "SH" favicon
images/<project>/         photos, one folder per project
images/headshot/          headshot
resume/                   Sam_Heller_Resume.pdf goes here
```

## Preparing photos

- Resize to about **1600 to 2000 px wide** before committing (the headshot can be ~800 px wide).
- Save as **JPG** (quality ~80) or **WebP**. Aim for under ~400 KB per photo.
- Use the exact file names below. If you use WebP, change the extension in the HTML too.
- Crop roughly to the ratio listed. Images are center-cropped to fit (`object-fit: cover`), so off-ratio photos still work but may lose edges.

## Swapping a placeholder for a photo

Every placeholder is a gray `<div class="ph ...">` with a comment directly above it containing the exact `<img>` tag to use. To swap one in:

1. Put the photo in the folder named in the placeholder (e.g. `images/chiropter/hero.jpg`).
2. Delete the `<div class="ph ...">...</div>` block.
3. Uncomment the `<img>` tag from the `REPLACE WITH:` comment above it (remove `<!-- REPLACE WITH:` and `-->`).
4. Edit the `alt` text so it describes what is actually in the photo.
5. Update `width`/`height` to your photo's real pixel size (this prevents layout jumps while loading).

Example:

```html
<!-- before -->
<!-- REPLACE WITH: <img class="ratio-16x9" src="../images/chiropter/hero.jpg" alt="Chiropter flapping-wing drone prototype" width="1920" height="1080"> -->
<div class="ph ratio-16x9" role="img" aria-label="Placeholder for Chiropter hero image">
  <span>Chiropter: hero image, 16:9</span>
  <code>images/chiropter/hero.jpg</code>
</div>

<!-- after -->
<img class="ratio-16x9" src="../images/chiropter/hero.jpg" alt="Chiropter prototype on the test stand" width="1920" height="1080">
```

Gallery and home-page card images already include `loading="lazy"` in their replacement tags.

## Placeholder checklist

### Images

Each project's `hero.jpg` is used twice: as the 16:9 hero on its project page and as the 3:2 card image on the home page. It is also the `og:image` for link previews.

| Page | Placeholder | File | Ratio |
|---|---|---|---|
| Home | Headshot (About section) | `images/headshot/headshot.jpg` | 4:5 portrait |
| Home + Chiropter | Hero / card | `images/chiropter/hero.jpg` | 16:9 |
| Chiropter | Gallery 1: flapping drive | `images/chiropter/gallery-1.jpg` | 4:3 |
| Chiropter | Gallery 2: folding drive | `images/chiropter/gallery-2.jpg` | 4:3 |
| Chiropter | Gallery 3: chassis | `images/chiropter/gallery-3.jpg` | 4:3 |
| Chiropter | Gallery 4: carbon fiber and nylon parts | `images/chiropter/gallery-4.jpg` | 4:3 |
| Home + EasySDS | Hero / card | `images/easysds/hero.jpg` | 16:9 |
| EasySDS | Gallery 1: generated label | `images/easysds/gallery-1.jpg` | 4:3 |
| EasySDS | Gallery 2: approval queue | `images/easysds/gallery-2.jpg` | 4:3 |
| EasySDS | Gallery 3: admin inventory | `images/easysds/gallery-3.jpg` | 4:3 |
| EasySDS | Gallery 4: printed label on vinyl stock | `images/easysds/gallery-4.jpg` | 4:3 |

That is 11 images total (1 headshot + 2 heroes + 8 gallery).

### Other files and text

- **Resume:** `resume/Sam_Heller_Resume.pdf` (the nav link and the Download Resume button point here).
- **About bio** in `index.html`: marked `<!-- DRAFT: Sam to edit -->`.
- **Bracketed notes** like `[Add: test results]` on the project pages. They show highlighted in orange so they are easy to spot. Search the HTML for `[Add:` to find them all, then delete the `<span class="todo">...</span>` wrapper along with the text once filled in.
- **Footer year** is hard-coded as 2026 on every page. Update it in all three HTML files when it changes.

### Parked projects (Kayak Paddle, Glider, DockBloxx)

These pages are drafted but not published. They live outside the repo in `C:\Users\atlan\portfolio-parked\`, each with its placeholders and `[Add: ...]` notes. To bring one back:

1. Move `portfolio-parked/projects/<name>.html` into `projects/`, and `portfolio-parked/images/<name>/` into `images/`.
2. Add its card back to the `#projects` grid in `index.html` (see "Adding a new project" below). The original card text: Kayak Paddle, "A paddle that passively filters microplastics during a normal stroke, taken from concept to functional prototype."; Glider, "A flying wing designed in Fusion 360, Wing Helper, and Ansys, built from balsa and carbon fiber, and flight tested."; DockBloxx, "Modeled and animated a catalog of 20+ dock accessories and designed a new modular product from concept to prototype."

**DockBloxx: public work only.** Only put publicly released DockBloxx work on its page: products and renders/animations that already appear on the DockBloxx website. Nothing unreleased, internal, or under NDA.

### EasySDS screenshots

Before adding EasySDS screenshots, make sure they don't show any internal facility, inventory, or chemical data from Rhenus Automotive. Use demo data.

## Adding a new project

1. **Copy a project page.** Duplicate an existing page in `projects/` (e.g. `projects/chiropter.html`) and rename it, e.g. `projects/new-project.html`. Use lowercase with hyphens.
2. **Edit the new page:**
   - `<title>`, `<meta name="description">`, and the `og:title`, `og:description`, `og:image`, and `og:url` tags in the `<head>`.
   - The `<h1>`, the `.lede` one-liner, and the facts row (`Role`, `Timeframe`, `Where`, `Tools`).
   - The Overview, My Role, and What I Built / Key Details sections.
   - Every placeholder's label and `images/...` path to point at the new folder.
3. **Create its image folder:** `images/new-project/`, and add `hero.jpg` plus `gallery-1.jpg` through `gallery-4.jpg` (or keep the placeholders until you have photos). Add an empty `.gitkeep` if the folder is empty, since Git does not track empty folders.
4. **Add a card to `index.html`.** Copy one `<article class="card">...</article>` block inside the `#projects` grid, paste it where you want it in the order, then update the image path, the link (`projects/new-project.html`), the title, the one-line summary, and 2 to 4 tags. Software projects go in the smaller "Software Tools" grid below.
5. Open `index.html` locally, click through to the new page, and check it at phone width.

## Publishing

1. Commit and push to the `main` branch of `sam-j-heller/PersonalPortfolio`.
2. On GitHub: **Settings > Pages**, set Source to **Deploy from a branch**, Branch **main**, folder **/ (root)**, and save.
3. After a minute or two the site is live at https://sam-j-heller.github.io/PersonalPortfolio/. The **Actions** tab shows deploy progress.

## Notes

- The one exception to relative paths is the `og:image` / `og:url` meta tags. Link previews (LinkedIn, Slack, iMessage) require absolute URLs there, so they point at `https://sam-j-heller.github.io/PersonalPortfolio/...`.
- Colors live as CSS variables at the top of `css/style.css`. Maroon `#861F41` is the main accent; Burnt Orange `#E5751F` is only used for small highlights (hover states, tags, notes), since it is too light for body text.
