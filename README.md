<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Your Name – Photography</title>
<meta name="description" content="Photography portfolio of Your Name.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500&family=Newsreader:opsz,wght@6..72,400;6..72,500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #fafaf9;
    --text: #1c1c1c;
    --muted: #6b6b6b;
    --line: #e4e4e1;
    --accent: #2f5d62;
    --overlay: rgba(10,10,10,.94);
  }
  @media (prefers-color-scheme: dark) {
    :root {
      --bg: #141414;
      --text: #ececea;
      --muted: #9a9a96;
      --line: #2a2a2a;
      --accent: #8fbfc4;
    }
  }
  * { box-sizing: border-box; }
  html { scroll-behavior: smooth; scroll-padding-top: 70px; }
  body {
    margin: 0;
    background: var(--bg);
    color: var(--text);
    font: 400 16px/1.6 Inter, system-ui, -apple-system, "Segoe UI", sans-serif;
    -webkit-font-smoothing: antialiased;
  }
  a { color: inherit; }
  :focus-visible { outline: 2px solid var(--accent); outline-offset: 3px; }

  /* Header */
  header {
    position: sticky; top: 0; z-index: 10;
    background: color-mix(in srgb, var(--bg) 92%, transparent);
    backdrop-filter: blur(8px);
    border-bottom: 1px solid var(--line);
  }
  .bar {
    max-width: 1200px; margin: 0 auto; padding: 14px 24px;
    display: flex; justify-content: space-between; align-items: center; gap: 16px;
  }
  .brand {
    font: 500 22px/1 Newsreader, Georgia, serif;
    text-decoration: none; letter-spacing: .01em;
  }
  nav { display: flex; gap: 22px; font-size: 14px; }
  nav a { text-decoration: none; color: var(--muted); }
  nav a:hover { color: var(--text); }

  main { max-width: 1200px; margin: 0 auto; padding: 0 24px; }

  /* Intro */
  .intro { padding: 72px 0 40px; max-width: 640px; }
  .intro h1 {
    font: 400 clamp(32px, 6vw, 52px)/1.15 Newsreader, Georgia, serif;
    margin: 0 0 16px; letter-spacing: -.01em;
  }
  .intro p { margin: 0; color: var(--muted); font-size: 17px; }

  /* Filters */
  .filters { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 28px; }
  .filters button {
    font: 500 13px/1 Inter, sans-serif;
    padding: 9px 16px; border-radius: 999px; cursor: pointer;
    background: transparent; color: var(--muted);
    border: 1px solid var(--line);
  }
  .filters button:hover { color: var(--text); border-color: var(--muted); }
  .filters button[aria-pressed="true"] {
    background: var(--text); color: var(--bg); border-color: var(--text);
  }

  /* Gallery */
  .gallery { columns: 3 280px; column-gap: 14px; }
  .item {
    break-inside: avoid; margin: 0 0 14px; display: block; width: 100%;
    padding: 0; border: 0; background: none; cursor: zoom-in; position: relative;
  }
  .item img, .item .ph { width: 100%; display: block; border-radius: 2px; }
  .item .ph { background: linear-gradient(135deg, var(--c1), var(--c2)); }
  .item .cap {
    position: absolute; inset: auto 0 0 0; padding: 28px 14px 12px;
    background: linear-gradient(transparent, rgba(0,0,0,.6));
    color: #fff; font-size: 13px; text-align: left;
    opacity: 0; transition: opacity .2s;
  }
  .item:hover .cap, .item:focus-visible .cap { opacity: 1; }

  /* About + contact */
  section.block {
    display: grid; grid-template-columns: 1fr 2fr; gap: 40px;
    padding: 72px 0; margin-top: 56px; border-top: 1px solid var(--line);
  }
  section.block h2 { font: 500 24px/1.2 Newsreader, Georgia, serif; margin: 0; }
  section.block p { margin: 0 0 14px; max-width: 60ch; }
  .muted { color: var(--muted); }
  .links a { text-decoration-color: var(--line); text-underline-offset: 4px; }
  .links a:hover { text-decoration-color: var(--accent); }

  footer {
    max-width: 1200px; margin: 0 auto; padding: 28px 24px 48px;
    font-size: 13px; color: var(--muted); border-top: 1px solid var(--line);
  }

  /* Lightbox */
  .lb {
    position: fixed; inset: 0; z-index: 50; background: var(--overlay);
    display: none; align-items: center; justify-content: center; flex-direction: column;
    padding: 24px;
  }
  .lb.open { display: flex; }
  .lb .stage { max-width: 100%; max-height: 80vh; display: flex; }
  .lb img { max-width: 100%; max-height: 80vh; object-fit: contain; }
  .lb .ph { width: min(80vw, 900px); max-height: 75vh; background: linear-gradient(135deg, var(--c1), var(--c2)); }
  .lb .meta { color: #ddd; font-size: 14px; margin-top: 14px; text-align: center; }
  .lb button {
    position: absolute; background: none; border: 0; color: #fff;
    font-size: 32px; line-height: 1; cursor: pointer; padding: 14px; opacity: .8;
  }
  .lb button:hover { opacity: 1; }
  .lb .close { top: 8px; right: 12px; }
  .lb .prev { left: 4px; top: 50%; }
  .lb .next { right: 4px; top: 50%; }

  @media (max-width: 720px) {
    .bar { padding: 12px 18px; }
    main { padding: 0 18px; }
    .intro { padding: 44px 0 28px; }
    section.block { grid-template-columns: 1fr; gap: 16px; padding: 48px 0; }
    .item .cap { opacity: 1; }
  }
  @media (prefers-reduced-motion: reduce) {
    html { scroll-behavior: auto; }
    .item .cap { transition: none; }
  }
</style>
</head>
<body>

<header>
  <div class="bar">
    <a class="brand" href="#top">Your Name</a>
    <nav aria-label="Main">
      <a href="#work">Work</a>
      <a href="#about">About</a>
      <a href="#contact">Contact</a>
    </nav>
  </div>
</header>

<main id="top">
  <div class="intro">
    <h1>Photography by Your Name</h1>
    <p>Landscapes, street, and portraits. Based in Your City.</p>
  </div>

  <div id="work">
    <div class="filters" id="filters" role="group" aria-label="Filter photos"></div>
    <div class="gallery" id="gallery"></div>
  </div>

  <section class="block" id="about">
    <h2>About</h2>
    <div>
      <p>Write two or three sentences about yourself here: how you started, what you like to shoot, and what you’re working on now.</p>
      <p class="muted">Gear: Camera body, favorite lens, film stock or editing software.</p>
    </div>
  </section>

  <section class="block" id="contact">
    <h2>Contact</h2>
    <div class="links">
      <p>For prints, licensing, or collaborations, email <a href="mailto:you@example.com">you@example.com</a>.</p>
      <p class="muted">
        <a href="https://instagram.com/yourhandle">Instagram</a> &nbsp;·&nbsp;
        <a href="https://flickr.com/photos/yourhandle">Flickr</a>
      </p>
    </div>
  </section>
</main>

<footer>© <span id="yr"></span> Your Name. All photographs are copyrighted and may not be used without permission.</footer>

<div class="lb" id="lb" role="dialog" aria-modal="true" aria-label="Photo viewer">
  <button class="close" aria-label="Close">×</button>
  <button class="prev" aria-label="Previous photo">‹</button>
  <button class="next" aria-label="Next photo">›</button>
  <div class="stage" id="stage"></div>
  <div class="meta" id="meta"></div>
</div>

<script>
  /* ============ EDIT YOUR PHOTOS HERE ============
     1. Put image files in a "photos" folder in your repo.
     2. Add one line per photo. w and h are the pixel size
        (used to avoid layout jumping while images load).
     3. Entries with an empty src show a color placeholder. */
  const PHOTOS = [
    { src: "", w: 1600, h: 1067, title: "Placeholder one",   cat: "Landscape", c1: "#6d8a96", c2: "#c9d6d2" },
    { src: "", w: 1067, h: 1600, title: "Placeholder two",   cat: "Portrait",  c1: "#b08968", c2: "#e6ccb2" },
    { src: "", w: 1600, h: 1067, title: "Placeholder three", cat: "Street",    c1: "#4a4e69", c2: "#9a8c98" },
    { src: "", w: 1200, h: 1200, title: "Placeholder four",  cat: "Landscape", c1: "#52796f", c2: "#cad2c5" },
    { src: "", w: 1067, h: 1600, title: "Placeholder five",  cat: "Street",    c1: "#8d99ae", c2: "#edf2f4" },
    { src: "", w: 1600, h: 1067, title: "Placeholder six",   cat: "Portrait",  c1: "#7f5539", c2: "#ddb892" }
  ];
  /* =============================================== */

  const gallery = document.getElementById("gallery");
  const filters = document.getElementById("filters");
  const lb = document.getElementById("lb");
  const stage = document.getElementById("stage");
  const meta = document.getElementById("meta");
  let current = "All", visible = [], idx = 0, lastFocus = null;

  document.getElementById("yr").textContent = new Date().getFullYear();

  function media(p, cls) {
    if (p.src) {
      const i = new Image();
      i.src = p.src; i.alt = p.title || ""; i.width = p.w; i.height = p.h;
      i.loading = "lazy"; if (cls) i.className = cls;
      return i;
    }
    const d = document.createElement("div");
    d.className = "ph";
    d.style.cssText = `--c1:${p.c1};--c2:${p.c2};aspect-ratio:${p.w}/${p.h}`;
    d.setAttribute("role", "img"); d.setAttribute("aria-label", p.title || "");
    return d;
  }

  function renderFilters() {
    const cats = ["All", ...new Set(PHOTOS.map(p => p.cat).filter(Boolean))];
    filters.innerHTML = "";
    cats.forEach(c => {
      const b = document.createElement("button");
      b.textContent = c;
      b.setAttribute("aria-pressed", c === current);
      b.onclick = () => { current = c; renderFilters(); renderGallery(); };
      filters.appendChild(b);
    });
  }

  function renderGallery() {
    visible = PHOTOS.filter(p => current === "All" || p.cat === current);
    gallery.innerHTML = "";
    visible.forEach((p, i) => {
      const b = document.createElement("button");
      b.className = "item";
      b.setAttribute("aria-label", "View " + (p.title || "photo"));
      b.appendChild(media(p));
      const cap = document.createElement("span");
      cap.className = "cap"; cap.textContent = p.title || "";
      b.appendChild(cap);
      b.onclick = () => openLb(i, b);
      gallery.appendChild(b);
    });
  }

  function showLb() {
    const p = visible[idx];
    stage.innerHTML = "";
    stage.appendChild(media(p));
    meta.textContent = [p.title, p.cat].filter(Boolean).join(" – ");
  }
  function openLb(i, trigger) {
    idx = i; lastFocus = trigger; showLb();
    lb.classList.add("open"); document.body.style.overflow = "hidden";
    lb.querySelector(".close").focus();
  }
  function closeLb() {
    lb.classList.remove("open"); document.body.style.overflow = "";
    if (lastFocus) lastFocus.focus();
  }
  function step(d) { idx = (idx + d + visible.length) % visible.length; showLb(); }

  lb.querySelector(".close").onclick = closeLb;
  lb.querySelector(".prev").onclick = () => step(-1);
  lb.querySelector(".next").onclick = () => step(1);
  lb.addEventListener("click", e => { if (e.target === lb) closeLb(); });
  document.addEventListener("keydown", e => {
    if (!lb.classList.contains("open")) return;
    if (e.key === "Escape") closeLb();
    if (e.key === "ArrowLeft") step(-1);
    if (e.key === "ArrowRight") step(1);
  });

  renderFilters();
  renderGallery();
</script>
</body>
</html>
