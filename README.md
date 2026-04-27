<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Protokol 0 Grawitacji</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Mono:wght@400;500&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0a;
    --surface: #111111;
    --surface2: #181818;
    --border: #242424;
    --accent: #e8ff00;
    --accent2: #ff4d00;
    --text: #f0f0f0;
    --muted: #666;
    --card: #141414;
  }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    line-height: 1.6;
    min-height: 100vh;
  }

  /* HEADER */
  header {
    position: sticky; top: 0; z-index: 100;
    background: rgba(10,10,10,0.95);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
    padding: 0 2rem;
  }
  .header-inner {
    max-width: 1300px; margin: auto;
    display: flex; align-items: center; gap: 2rem;
  }
  .logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.6rem;
    letter-spacing: 0.05em;
    color: var(--accent);
    white-space: nowrap;
    padding: 1rem 0;
    text-decoration: none;
  }
  .logo span { color: var(--text); }
  nav { display: flex; gap: 0; overflow-x: auto; flex: 1; }
  nav::-webkit-scrollbar { display: none; }
  nav a {
    color: var(--muted);
    text-decoration: none;
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 1.2rem 1rem;
    white-space: nowrap;
    border-bottom: 2px solid transparent;
    transition: color 0.2s, border-color 0.2s;
  }
  nav a:hover, nav a.active {
    color: var(--accent);
    border-bottom-color: var(--accent);
  }

  /* HERO */
  .hero {
    background: var(--surface);
    border-bottom: 1px solid var(--border);
    padding: 4rem 2rem 3rem;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .hero::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(ellipse 80% 60% at 50% 0%, rgba(232,255,0,0.05) 0%, transparent 70%);
    pointer-events: none;
  }
  .hero h1 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(3rem, 8vw, 6rem);
    letter-spacing: 0.04em;
    line-height: 1;
    color: var(--text);
  }
  .hero h1 em { color: var(--accent); font-style: normal; }
  .hero p {
    color: var(--muted);
    font-size: 1rem;
    margin-top: 0.75rem;
    font-family: 'DM Mono', monospace;
    letter-spacing: 0.05em;
  }
  .tag-row {
    display: flex; flex-wrap: wrap; gap: 0.5rem;
    justify-content: center; margin-top: 1.5rem;
  }
  .tag {
    background: var(--border);
    border: 1px solid var(--border);
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 0.3rem 0.8rem;
    border-radius: 2px;
  }
  .tag.accent { background: rgba(232,255,0,0.1); border-color: rgba(232,255,0,0.3); color: var(--accent); }

  /* TABS */
  .tabs {
    background: var(--bg);
    border-bottom: 1px solid var(--border);
    display: flex; gap: 0;
    overflow-x: auto;
    padding: 0 2rem;
    max-width: 100%;
  }
  .tabs::-webkit-scrollbar { display: none; }
  .tab-btn {
    background: none; border: none; cursor: pointer;
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.72rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 1rem 1.2rem;
    white-space: nowrap;
    border-bottom: 2px solid transparent;
    transition: all 0.2s;
  }
  .tab-btn:hover { color: var(--text); }
  .tab-btn.active { color: var(--accent); border-bottom-color: var(--accent); }

  /* MAIN */
  main { max-width: 1300px; margin: auto; padding: 2rem; }
  .tab-panel { display: none; }
  .tab-panel.active { display: block; }

  /* SECTIONS */
  .section-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2rem;
    letter-spacing: 0.05em;
    color: var(--text);
    margin-bottom: 1.5rem;
    border-left: 3px solid var(--accent);
    padding-left: 1rem;
  }
  .section-title small {
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    color: var(--muted);
    letter-spacing: 0.1em;
    display: block;
    font-weight: 400;
    margin-top: 0.2rem;
  }

  /* KALKULATOR */
  .calc-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5rem;
  }
  @media(max-width: 768px) { .calc-grid { grid-template-columns: 1fr; } }
  .calc-box {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 1.5rem;
  }
  .calc-box h3 {
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 1.2rem;
    padding-bottom: 0.7rem;
    border-bottom: 1px solid var(--border);
  }
  .input-row {
    display: grid;
    grid-template-columns: 1fr 1fr 1.2fr;
    gap: 0.5rem;
    align-items: center;
    padding: 0.5rem 0;
    border-bottom: 1px solid rgba(255,255,255,0.04);
    font-size: 0.875rem;
  }
  .input-row:last-child { border-bottom: none; }
  .input-row label { color: var(--muted); font-size: 0.82rem; }
  .input-row input, .input-row select {
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--text);
    padding: 0.4rem 0.6rem;
    font-family: 'DM Mono', monospace;
    font-size: 0.82rem;
    border-radius: 2px;
    outline: none;
    transition: border-color 0.2s;
  }
  .input-row input:focus, .input-row select:focus { border-color: var(--accent); }
  .input-row .desc { color: var(--muted); font-size: 0.72rem; font-family: 'DM Mono', monospace; }
  .result-row {
    display: grid;
    grid-template-columns: 1fr auto auto 1fr;
    gap: 0.5rem;
    align-items: center;
    padding: 0.6rem 0;
    border-bottom: 1px solid rgba(255,255,255,0.04);
    font-size: 0.875rem;
  }
  .result-row:last-child { border-bottom: none; }
  .result-row .label { color: var(--muted); }
  .result-row .val {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.4rem;
    color: var(--accent);
    letter-spacing: 0.05em;
  }
  .result-row .unit { color: var(--muted); font-size: 0.75rem; font-family: 'DM Mono', monospace; }
  .result-row .interp { color: var(--text); font-size: 0.8rem; text-align: right; }
  .macro-bar-row { margin: 0.8rem 0; }
  .macro-bar-row label {
    display: flex; justify-content: space-between;
    font-size: 0.8rem; color: var(--muted);
    margin-bottom: 0.3rem;
  }
  .macro-bar-row label span { color: var(--text); font-family: 'DM Mono', monospace; font-size: 0.78rem; }
  .bar { height: 6px; background: var(--border); border-radius: 3px; overflow: hidden; }
  .bar-fill { height: 100%; border-radius: 3px; transition: width 0.4s ease; }
  .bar-p { background: #4fc3f7; }
  .bar-c { background: #81c784; }
  .bar-f { background: #ffb74d; }
  .calc-btn {
    background: var(--accent);
    color: #000;
    border: none;
    padding: 0.8rem 2rem;
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.1rem;
    letter-spacing: 0.1em;
    cursor: pointer;
    border-radius: 2px;
    margin-top: 1rem;
    transition: opacity 0.2s;
    width: 100%;
  }
  .calc-btn:hover { opacity: 0.85; }

  /* ACTIVITY TABLE */
  .activity-table { width: 100%; border-collapse: collapse; margin-top: 1rem; font-size: 0.85rem; }
  .activity-table th {
    background: var(--surface2);
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.68rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 0.7rem 1rem;
    text-align: left;
    border-bottom: 1px solid var(--border);
  }
  .activity-table td {
    padding: 0.65rem 1rem;
    border-bottom: 1px solid rgba(255,255,255,0.04);
    color: var(--text);
  }
  .activity-table tr:hover td { background: rgba(255,255,255,0.02); }
  .mono { font-family: 'DM Mono', monospace; color: var(--muted); font-size: 0.82rem; }

  /* PRODUKTY */
  .product-filters {
    display: flex; flex-wrap: wrap; gap: 0.5rem;
    margin-bottom: 1.5rem;
  }
  .filter-btn {
    background: var(--card); border: 1px solid var(--border);
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 0.4rem 0.9rem;
    cursor: pointer;
    border-radius: 2px;
    transition: all 0.2s;
  }
  .filter-btn:hover, .filter-btn.active {
    background: rgba(232,255,0,0.1);
    border-color: rgba(232,255,0,0.4);
    color: var(--accent);
  }
  .search-box {
    width: 100%; max-width: 400px;
    background: var(--card);
    border: 1px solid var(--border);
    color: var(--text);
    padding: 0.6rem 1rem;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.9rem;
    border-radius: 2px;
    outline: none;
    margin-bottom: 1rem;
    transition: border-color 0.2s;
  }
  .search-box:focus { border-color: var(--accent); }
  .product-table-wrap { overflow-x: auto; }
  .product-table { width: 100%; border-collapse: collapse; font-size: 0.85rem; }
  .product-table th {
    background: var(--surface2);
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.68rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 0.7rem 1rem;
    text-align: left;
    border-bottom: 1px solid var(--border);
    cursor: pointer;
    user-select: none;
    white-space: nowrap;
  }
  .product-table th:hover { color: var(--accent); }
  .product-table td {
    padding: 0.6rem 1rem;
    border-bottom: 1px solid rgba(255,255,255,0.04);
  }
  .product-table tr:hover td { background: rgba(255,255,255,0.02); }
  .product-table .num { font-family: 'DM Mono', monospace; color: var(--muted); text-align: right; }
  .product-table .num-hi { font-family: 'DM Mono', monospace; color: var(--accent); font-weight: 500; text-align: right; }
  .cat-badge {
    display: inline-block;
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 0.2rem 0.5rem;
    border-radius: 2px;
    background: var(--border);
    color: var(--muted);
    white-space: nowrap;
  }

  /* SUPLEMENTY */
  .supp-grid { display: grid; gap: 1rem; }
  .supp-category {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
  }
  .supp-cat-header {
    padding: 0.9rem 1.2rem;
    background: var(--surface2);
    border-bottom: 1px solid var(--border);
    display: flex; align-items: center; gap: 0.8rem;
    cursor: pointer;
  }
  .supp-cat-header h3 {
    font-family: 'DM Mono', monospace;
    font-size: 0.72rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--text);
    flex: 1;
  }
  .supp-cat-header .badge {
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    padding: 0.2rem 0.6rem;
    border-radius: 2px;
  }
  .badge-red { background: rgba(255,77,0,0.15); color: #ff4d00; border: 1px solid rgba(255,77,0,0.3); }
  .badge-orange { background: rgba(255,165,0,0.12); color: #ffa500; border: 1px solid rgba(255,165,0,0.3); }
  .badge-yellow { background: rgba(232,255,0,0.1); color: var(--accent); border: 1px solid rgba(232,255,0,0.3); }
  .badge-blue { background: rgba(79,195,247,0.1); color: #4fc3f7; border: 1px solid rgba(79,195,247,0.3); }
  .badge-green { background: rgba(129,199,132,0.1); color: #81c784; border: 1px solid rgba(129,199,132,0.3); }
  .badge-purple { background: rgba(186,104,200,0.1); color: #ba68c8; border: 1px solid rgba(186,104,200,0.3); }
  .supp-table { width: 100%; border-collapse: collapse; font-size: 0.83rem; }
  .supp-table th {
    background: transparent;
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 0.6rem 1rem;
    text-align: left;
    border-bottom: 1px solid var(--border);
  }
  .supp-table td {
    padding: 0.65rem 1rem;
    border-bottom: 1px solid rgba(255,255,255,0.04);
    vertical-align: top;
  }
  .supp-table tr:last-child td { border-bottom: none; }
  .supp-table tr:hover td { background: rgba(255,255,255,0.015); }
  .supp-table .name { font-weight: 500; color: var(--text); }
  .supp-table .dose { font-family: 'DM Mono', monospace; color: var(--accent); font-size: 0.78rem; }
  .supp-table .when { color: var(--muted); font-size: 0.78rem; }
  .supp-table .note { color: var(--muted); font-size: 0.75rem; font-style: italic; }
  .supp-collapsed .supp-table-wrap { display: none; }

  /* PERIODYZACJA */
  .period-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; }
  @media(max-width: 900px) { .period-grid { grid-template-columns: 1fr; } }
  .period-box {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 1.5rem;
  }
  .period-box h3 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.4rem;
    letter-spacing: 0.05em;
    margin-bottom: 1rem;
  }
  .period-box.linear { border-top: 3px solid #4fc3f7; }
  .period-box.linear h3 { color: #4fc3f7; }
  .period-box.wave { border-top: 3px solid var(--accent); }
  .period-box.wave h3 { color: var(--accent); }
  .compare-table { width: 100%; border-collapse: collapse; font-size: 0.82rem; }
  .compare-table td {
    padding: 0.55rem 0;
    border-bottom: 1px solid rgba(255,255,255,0.05);
    vertical-align: top;
  }
  .compare-table td:first-child { color: var(--muted); width: 40%; padding-right: 1rem; }
  .compare-table tr:last-child td { border-bottom: none; }
  .concept-grid { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 1rem; margin-top: 1.5rem; }
  @media(max-width: 768px) { .concept-grid { grid-template-columns: 1fr 1fr; } }
  .concept-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 1.2rem;
  }
  .concept-card h4 {
    font-family: 'DM Mono', monospace;
    font-size: 0.72rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 0.5rem;
  }
  .concept-card p { color: var(--muted); font-size: 0.82rem; }
  .concept-card .example { color: var(--text); font-size: 0.78rem; margin-top: 0.5rem; font-style: italic; }
  .rules-list { list-style: none; margin-top: 1rem; }
  .rules-list li {
    display: flex; gap: 0.8rem;
    padding: 0.7rem 0;
    border-bottom: 1px solid rgba(255,255,255,0.05);
    font-size: 0.85rem;
    align-items: flex-start;
  }
  .rules-list li:last-child { border-bottom: none; }
  .rules-list .icon { font-size: 1rem; flex-shrink: 0; margin-top: 0.1rem; }
  .rules-list .rule-text { color: var(--text); }
  .rules-list .rule-text b { color: var(--accent); }

  /* KALKULATOR 1RM */
  .rm-grid { display: grid; grid-template-columns: 1fr 1.2fr; gap: 1.5rem; }
  @media(max-width: 768px) { .rm-grid { grid-template-columns: 1fr; } }
  .rm-input-table { width: 100%; border-collapse: collapse; font-size: 0.85rem; }
  .rm-input-table th {
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.68rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 0.6rem 0.8rem;
    text-align: left;
    border-bottom: 1px solid var(--border);
  }
  .rm-input-table td { padding: 0.5rem 0.8rem; border-bottom: 1px solid rgba(255,255,255,0.04); }
  .rm-input-table input {
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--text);
    padding: 0.4rem 0.6rem;
    font-family: 'DM Mono', monospace;
    font-size: 0.82rem;
    border-radius: 2px;
    outline: none;
    width: 70px;
    transition: border-color 0.2s;
  }
  .rm-input-table input:focus { border-color: var(--accent); }
  .rm-result { font-family: 'Bebas Neue', sans-serif; font-size: 1.3rem; color: var(--accent); letter-spacing: 0.05em; }
  .pct-table { width: 100%; border-collapse: collapse; font-size: 0.83rem; }
  .pct-table th {
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.68rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 0.6rem 0.8rem;
    text-align: left;
    border-bottom: 1px solid var(--border);
  }
  .pct-table td { padding: 0.5rem 0.8rem; border-bottom: 1px solid rgba(255,255,255,0.04); }
  .pct-table tr:hover td { background: rgba(255,255,255,0.02); }
  .pct-bar-cell { width: 100px; }
  .pct-bar { height: 4px; background: var(--border); border-radius: 2px; }
  .pct-bar-fill { height: 100%; background: var(--accent); border-radius: 2px; }
  .zone-max { color: var(--accent2); }
  .zone-heavy { color: #ffa500; }
  .zone-mod { color: #81c784; }
  .zone-light { color: #4fc3f7; }

  /* WAGA */
  .waga-info {
    background: var(--card);
    border: 1px solid var(--border);
    border-left: 3px solid var(--accent);
    border-radius: 4px;
    padding: 1rem 1.5rem;
    margin-bottom: 1.5rem;
    font-size: 0.85rem;
    color: var(--muted);
  }
  .month-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1.5rem;
    margin-bottom: 2rem;
  }
  @media(max-width: 900px) { .month-grid { grid-template-columns: 1fr 1fr; } }
  @media(max-width: 600px) { .month-grid { grid-template-columns: 1fr; } }
  .month-box {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
  }
  .month-box h3 {
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--accent);
    padding: 0.7rem 1rem;
    background: var(--surface2);
    border-bottom: 1px solid var(--border);
  }
  .month-days { max-height: 280px; overflow-y: auto; }
  .month-days::-webkit-scrollbar { width: 4px; }
  .month-days::-webkit-scrollbar-thumb { background: var(--border); border-radius: 2px; }
  .day-row {
    display: grid;
    grid-template-columns: auto 1fr auto;
    align-items: center;
    gap: 0.5rem;
    padding: 0.35rem 0.8rem;
    border-bottom: 1px solid rgba(255,255,255,0.03);
    font-size: 0.8rem;
  }
  .day-row .day-num { color: var(--muted); font-family: 'DM Mono', monospace; font-size: 0.72rem; width: 40px; }
  .day-row input {
    background: transparent;
    border: none;
    border-bottom: 1px solid transparent;
    color: var(--text);
    font-family: 'DM Mono', monospace;
    font-size: 0.82rem;
    outline: none;
    width: 100%;
    transition: border-color 0.2s;
  }
  .day-row input:focus { border-bottom-color: var(--accent); }
  .day-row input::placeholder { color: var(--muted); font-size: 0.72rem; }
  .day-row .day-unit { color: var(--muted); font-family: 'DM Mono', monospace; font-size: 0.7rem; }

  /* TRENING */
  .blok-selector {
    display: flex; gap: 0.5rem; margin-bottom: 1.5rem; flex-wrap: wrap;
  }
  .blok-btn {
    background: var(--card); border: 1px solid var(--border);
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 0.5rem 1rem;
    cursor: pointer;
    border-radius: 2px;
    transition: all 0.2s;
  }
  .blok-btn:hover, .blok-btn.active {
    background: rgba(232,255,0,0.1);
    border-color: rgba(232,255,0,0.4);
    color: var(--accent);
  }
  .week-selector {
    display: flex; gap: 0.5rem; margin-bottom: 1.5rem; flex-wrap: wrap;
  }
  .week-btn {
    background: var(--card); border: 1px solid var(--border);
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.68rem;
    letter-spacing: 0.06em;
    text-transform: uppercase;
    padding: 0.4rem 0.8rem;
    cursor: pointer;
    border-radius: 2px;
    transition: all 0.2s;
  }
  .week-btn:hover, .week-btn.active {
    back
