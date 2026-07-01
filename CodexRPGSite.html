import { useState, useEffect, useRef, useMemo } from "react";
import {
  Sparkles, Users, BookOpen, ChevronLeft, ChevronRight, X, Plus, Settings,
  ShieldCheck, Swords, Zap, Heart, Flame, Wind, Target, Lock, Unlock, Clock,
  User, ScrollText, Package, Trash2, Edit3, Check, Layers, Gauge, Timer,
  Image as ImageIcon, Key, Shuffle, Copy,
} from "lucide-react";

/* ============================== helpers ============================== */

const uid = () => Math.random().toString(36).slice(2, 10) + Date.now().toString(36).slice(-4);
const clamp = (n, min, max) => Math.min(max, Math.max(min, n));
const fmt = (n) => Math.round(n).toLocaleString("en-US");
const shortNum = (n) => (n >= 1000 ? Math.round(n / 1000) + "K" : String(n));

function genPassword() {
  const chars = "ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
  let out = "";
  for (let i = 0; i < 6; i++) out += chars[Math.floor(Math.random() * chars.length)];
  return out;
}

function timeAgo(ts) {
  const s = Math.floor((Date.now() - ts) / 1000);
  if (s < 60) return "just now";
  const m = Math.floor(s / 60);
  if (m < 60) return `${m}m ago`;
  const h = Math.floor(m / 60);
  if (h < 24) return `${h}h ago`;
  const d = Math.floor(h / 24);
  if (d < 30) return `${d}d ago`;
  const mo = Math.floor(d / 30);
  if (mo < 12) return `${mo}mo ago`;
  const y = Math.floor(mo / 12);
  return `${y}y ago`;
}

function defaultStatCategories() {
  return [
    { id: uid(), name: "Physical", stats: [
      { id: uid(), name: "Strength" },
      { id: uid(), name: "Speed" },
      { id: uid(), name: "Sensory" },
      { id: uid(), name: "Energy" },
    ]},
    { id: uid(), name: "Skill", stats: [
      { id: uid(), name: "Ability" },
    ]},
    { id: uid(), name: "Proficiency", stats: [
      { id: uid(), name: "Light Sword" },
      { id: uid(), name: "Heavy Sword" },
      { id: uid(), name: "Flash Spell" },
      { id: uid(), name: "Energy Spell" },
      { id: uid(), name: "Utility Spell" },
      { id: uid(), name: "Heal Spell" },
    ]},
  ];
}

function defaultMoveCategories() {
  return ["Shiriyoku", "Flash Spell", "Phase Spell", "Heal Spell", "Energy Spell", "Utility Spell"]
    .map((name) => ({ id: uid(), name }));
}

const METER_DEFS = [
  { id: "conviction", name: "Conviction", primary: true, color: "gold" },
  { id: "resolve", name: "Resolve", color: "cyan" },
  { id: "humanity", name: "Humanity", color: "emerald" },
  { id: "stress", name: "Stress", color: "crimson" },
  { id: "trust", name: "Trust", color: "magenta" },
];

function defaultMeters() {
  const m = {};
  METER_DEFS.forEach((d) => (m[d.id] = 5));
  return m;
}

function flattenStats(categories) {
  const out = [];
  (categories || []).forEach((cat) => (cat.stats || []).forEach((s) => out.push({ ...s, categoryId: cat.id, categoryName: cat.name })));
  return out;
}

function updateConfig(world, storyId, fn) {
  return { ...world, storyConfigs: { ...world.storyConfigs, [storyId]: fn(world.storyConfigs[storyId]) } };
}

const STAT_STEPS = [1, 5, 10, 100, 1000];
const ALL_STEPS = [...STAT_STEPS.slice().reverse().map((n) => -n), ...STAT_STEPS];
const PLAYER_SPEND_STEPS = [1, 10000, 25000, 50000, 100000];

/* ============================== styling ============================== */

const CSS = `
@import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@500;600;700&family=Sora:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;600;700&display=swap');

:root{
  --ink:#05060d; --void-1:#0a0d1c; --void-2:#10142b;
  --panel-bg:rgba(17,20,40,0.55); --panel-bg-solid:#12142a; --panel-border:rgba(216,180,99,0.22);
  --gold:#d8b463; --gold-bright:#f5dc9c; --gold-dim:#8a7346;
  --violet:#7c5cd6; --violet-bright:#a78bfa;
  --magenta:#b8467a; --cyan:#3fb6c9; --crimson:#d1495b; --emerald:#4f9d69;
  --text:#eee9f7; --text-dim:#a29fb8; --text-faint:#6b6884;
  --font-display:'Cinzel', Georgia, serif;
  --font-body:'Sora', system-ui, -apple-system, sans-serif;
  --font-mono:'JetBrains Mono', ui-monospace, monospace;
}
*{ box-sizing:border-box; }
.app-root{
  position:relative; min-height:100vh; width:100%; background:var(--ink);
  color:var(--text); font-family:var(--font-body); overflow-x:hidden;
}
.app-root, .app-root *{ -webkit-tap-highlight-color:transparent; }
a,button,input,textarea,select{ font-family:inherit; }
button{ cursor:pointer; }
:focus-visible{ outline:2px solid var(--gold-bright); outline-offset:2px; border-radius:4px; }

/* ---------- cosmic background ---------- */
.cosmic-bg{ position:fixed; inset:0; z-index:0; overflow:hidden; background:
  radial-gradient(ellipse at 20% 10%, #14173a 0%, transparent 55%),
  radial-gradient(ellipse at 80% 85%, #1a1030 0%, transparent 55%),
  linear-gradient(180deg, #05060d 0%, #090b18 45%, #0b0e1e 100%); }
.nebula{ position:absolute; border-radius:50%; filter:blur(70px); mix-blend-mode:screen; opacity:.5; animation:nebulaDrift 26s ease-in-out infinite; }
.nebula-a{ width:52vw; height:52vw; top:-12%; left:-10%; background:radial-gradient(circle, var(--violet), transparent 70%); animation-duration:30s; }
.nebula-b{ width:44vw; height:44vw; bottom:-14%; right:-8%; background:radial-gradient(circle, var(--magenta), transparent 70%); animation-duration:34s; animation-delay:-8s; }
.nebula-c{ width:38vw; height:38vw; top:35%; left:55%; background:radial-gradient(circle, var(--cyan), transparent 70%); opacity:.28; animation-duration:38s; animation-delay:-16s; }
.star-field, .mote-field{ position:absolute; inset:0; }
.star{ position:absolute; border-radius:50%; background:#fff; animation-name:twinkle; animation-iteration-count:infinite; animation-timing-function:ease-in-out; box-shadow:0 0 4px rgba(255,255,255,.7); }
.star-gold{ background:var(--gold-bright); box-shadow:0 0 6px rgba(245,220,156,.85); }
.mote{ position:absolute; border-radius:50%; animation-name:floatUp; animation-timing-function:linear; animation-iteration-count:infinite; }
.vignette{ position:absolute; inset:0; box-shadow:inset 0 0 18vw rgba(0,0,0,.55); pointer-events:none; }
@keyframes twinkle{ 0%,100%{ opacity:.15; transform:scale(.75); } 50%{ opacity:1; transform:scale(1.2); } }
@keyframes nebulaDrift{ 0%,100%{ transform:translate(0,0) scale(1); } 50%{ transform:translate(-3%,3%) scale(1.08); } }
@keyframes floatUp{ 0%{ transform:translateY(0) scale(1); opacity:0; } 10%{ opacity:.75; } 85%{ opacity:.35; } 100%{ transform:translateY(-115vh) scale(1.5); opacity:0; } }

/* ---------- layout ---------- */
.app-header{ position:sticky; top:0; z-index:40; display:flex; align-items:center; justify-content:space-between;
  gap:16px; padding:14px 24px; background:linear-gradient(180deg, rgba(8,9,20,.92), rgba(8,9,20,.75)); backdrop-filter:blur(10px);
  border-bottom:1px solid rgba(216,180,99,.14); flex-wrap:wrap; }
.brand{ display:flex; align-items:center; gap:8px; background:none; border:none; color:var(--gold-bright);
  font-family:var(--font-display); font-size:19px; letter-spacing:.14em; font-weight:600; }
.breadcrumb{ display:flex; align-items:center; gap:6px; color:var(--text-dim); font-size:13px; flex-wrap:wrap; }
.breadcrumb button{ background:none; border:none; color:var(--text-dim); font-size:13px; padding:2px 4px; }
.breadcrumb button:hover{ color:var(--gold-bright); }
.breadcrumb span{ color:var(--text); }
.mode-toggle{ display:flex; gap:4px; background:rgba(255,255,255,.04); padding:4px; border-radius:999px; border:1px solid rgba(255,255,255,.08); }
.mode-btn{ display:flex; align-items:center; gap:6px; background:none; border:none; color:var(--text-faint); font-size:12.5px;
  padding:6px 12px; border-radius:999px; transition:all .25s ease; }
.mode-btn.active{ background:linear-gradient(135deg, var(--gold-dim), var(--gold)); color:#1a1408; font-weight:600; box-shadow:0 0 14px rgba(216,180,99,.4); }
.app-main{ position:relative; z-index:1; padding:32px 24px 90px; max-width:1280px; margin:0 auto; }
.view-transition{ animation:fadeSlideIn .5s cubic-bezier(.2,.8,.2,1); }
@keyframes fadeSlideIn{ from{ opacity:0; transform:translateY(16px); } to{ opacity:1; transform:translateY(0); } }
.save-indicator{ position:fixed; bottom:16px; right:20px; z-index:50; font-size:11px; letter-spacing:.06em; text-transform:uppercase;
  color:var(--text-faint); padding:6px 12px; border-radius:999px; background:rgba(10,11,22,.7); border:1px solid rgba(255,255,255,.08);
  opacity:0; transition:opacity .3s ease; pointer-events:none; }
.save-saving,.save-saved,.save-error{ opacity:1; }
.save-error{ color:var(--crimson); border-color:rgba(209,73,91,.4); }
.loading-screen{ position:relative; z-index:1; min-height:100vh; display:flex; flex-direction:column; align-items:center; justify-content:center; gap:18px; color:var(--text-dim); font-family:var(--font-display); letter-spacing:.08em; }
.loading-sigil{ width:56px; height:56px; border-radius:50%; border:2px solid rgba(216,180,99,.25); border-top-color:var(--gold-bright); animation:ringSpin 1.1s linear infinite; }
@keyframes ringSpin{ from{ transform:rotate(0deg); } to{ transform:rotate(360deg); } }

/* ---------- buttons & inputs ---------- */
.gold-btn{ display:inline-flex; align-items:center; gap:7px; background:linear-gradient(135deg, var(--gold-dim), var(--gold));
  color:#1a1408; border:none; padding:10px 18px; border-radius:10px; font-weight:600; font-size:13.5px; letter-spacing:.02em;
  box-shadow:0 2px 14px rgba(216,180,99,.28); transition:transform .18s ease, box-shadow .18s ease; }
.gold-btn:hover{ transform:translateY(-1px); box-shadow:0 4px 20px rgba(216,180,99,.45); }
.gold-btn.small{ padding:7px 12px; font-size:12px; }
.ghost-btn{ display:inline-flex; align-items:center; gap:7px; background:rgba(255,255,255,.04); color:var(--text-dim);
  border:1px solid rgba(255,255,255,.1); padding:8px 14px; border-radius:10px; font-size:13px; transition:all .2s ease; }
.ghost-btn:hover{ color:var(--gold-bright); border-color:rgba(216,180,99,.35); }
.back-btn{ display:inline-flex; align-items:center; gap:4px; background:none; border:none; color:var(--text-dim); font-size:13px; margin-bottom:18px; padding:4px 0; }
.back-btn:hover{ color:var(--gold-bright); }
.icon-btn{ display:flex; align-items:center; justify-content:center; width:28px; height:28px; border-radius:8px;
  background:rgba(10,11,22,.75); border:1px solid rgba(255,255,255,.1); color:var(--text-dim); transition:all .2s ease; }
.icon-btn:hover{ color:var(--gold-bright); border-color:rgba(216,180,99,.4); }
.icon-btn.danger:hover{ color:var(--crimson); border-color:rgba(209,73,91,.4); }
.danger-btn{ display:inline-flex; align-items:center; gap:5px; background:rgba(209,73,91,.1); border:1px solid rgba(209,73,91,.3);
  color:#e88a95; font-size:11.5px; padding:6px 10px; border-radius:8px; transition:all .2s ease; }
.danger-btn.confirming{ background:var(--crimson); color:#fff; border-color:var(--crimson); }
.chip-btn{ font-family:var(--font-mono); font-size:11px; padding:5px 8px; border-radius:7px; background:rgba(255,255,255,.05);
  border:1px solid rgba(255,255,255,.09); color:var(--text-dim); transition:all .15s ease; }
.chip-btn.chip-pos:hover{ color:#8ee6a8; border-color:rgba(79,157,105,.5); background:rgba(79,157,105,.12); }
.chip-btn.chip-neg:hover{ color:#e8909b; border-color:rgba(209,73,91,.5); background:rgba(209,73,91,.12); }
.spend-btn{ display:inline-flex; align-items:center; gap:5px; background:linear-gradient(135deg, rgba(216,180,99,.22), rgba(216,180,99,.1));
  border:1px solid rgba(216,180,99,.4); color:var(--gold-bright); font-size:12px; padding:7px 12px; border-radius:8px; transition:all .2s ease; }
.spend-btn:hover:not(:disabled){ box-shadow:0 0 14px rgba(216,180,99,.35); transform:translateY(-1px); }
.spend-btn:disabled{ opacity:.35; cursor:not-allowed; }
.unlock-btn{ display:flex; align-items:center; justify-content:center; gap:7px; width:100%; margin-top:10px; padding:9px;
  border-radius:9px; background:linear-gradient(135deg, var(--gold-dim), var(--gold-bright)); color:#1a1408; border:none;
  font-weight:600; font-size:12.5px; animation:glowPulse 2.2s ease-in-out infinite; }
.add-card{ display:flex; flex-direction:column; align-items:center; justify-content:center; gap:8px; min-height:220px;
  border-radius:16px; border:1.5px dashed rgba(216,180,99,.3); background:rgba(216,180,99,.03); color:var(--gold-dim);
  font-size:13px; transition:all .25s ease; }
.add-card:hover{ border-color:var(--gold); color:var(--gold-bright); background:rgba(216,180,99,.07); }
.add-card-large{ min-height:280px; }
.text-input{ width:100%; background:rgba(6,7,15,.6); border:1px solid rgba(255,255,255,.1); color:var(--text);
  padding:9px 12px; border-radius:9px; font-size:13.5px; margin-bottom:12px; transition:border-color .2s ease; }
.text-input:focus{ border-color:rgba(216,180,99,.5); }
.textarea{ min-height:90px; resize:vertical; line-height:1.5; }
.inline-input{ margin-bottom:0; }
.inline-input.small{ font-size:12.5px; padding:6px 10px; }
.field-label{ display:block; font-size:11px; text-transform:uppercase; letter-spacing:.08em; color:var(--text-faint); margin-bottom:6px; }
.checkbox-row{ display:flex; align-items:center; gap:8px; font-size:13px; color:var(--text-dim); }

/* ---------- panels ---------- */
.glow-panel{ position:relative; background:var(--panel-bg); border:1px solid var(--panel-border); border-radius:16px;
  padding:20px 22px; backdrop-filter:blur(8px); box-shadow:0 8px 30px rgba(0,0,0,.25); margin-bottom:18px; }
.glow-panel h3{ display:flex; align-items:center; gap:8px; font-family:var(--font-display); font-size:15px; letter-spacing:.04em;
  color:var(--gold-bright); margin:0 0 14px; font-weight:600; }
.empty-note{ color:var(--text-faint); font-size:13px; font-style:italic; padding:14px 0; }

/* ---------- home / story cards ---------- */
.home-title{ text-align:center; margin-bottom:36px; }
.home-title h1{ font-family:var(--font-display); font-size:42px; letter-spacing:.22em; color:var(--gold-bright);
  text-shadow:0 0 30px rgba(216,180,99,.35); margin:0; }
.home-title p{ color:var(--text-faint); margin-top:8px; font-size:13.5px; letter-spacing:.03em; }
.story-grid{ display:grid; grid-template-columns:repeat(auto-fill, minmax(250px, 1fr)); gap:22px; }
.story-card{ position:relative; border-radius:18px; overflow:hidden; cursor:pointer; background:var(--panel-bg-solid);
  border:1px solid var(--panel-border); transform:perspective(800px) rotateX(var(--rx,0deg)) rotateY(var(--ry,0deg));
  transition:transform .25s ease, box-shadow .25s ease; }
.story-card:hover{ box-shadow:0 0 0 1px rgba(216,180,99,.4), 0 16px 40px rgba(216,180,99,.15); }
.story-card-cover{ height:150px; background:linear-gradient(135deg, var(--void-2), var(--void-1)); overflow:hidden; position:relative; }
.story-card-cover img{ width:100%; height:100%; object-fit:cover; }
.story-card-fallback{ width:100%; height:100%; display:flex; align-items:center; justify-content:center; color:var(--gold-dim); }
.story-card-body{ padding:16px 18px 18px; }
.story-card-body h2{ font-family:var(--font-display); font-size:18px; color:var(--text); margin:0 0 4px; }
.story-card-body p{ color:var(--text-faint); font-size:12.5px; margin:0 0 10px; }
.story-count{ display:inline-flex; align-items:center; gap:6px; font-size:11.5px; color:var(--gold-dim); font-family:var(--font-mono); }

/* ---------- roster / character cards ---------- */
.roster-head{ margin-bottom:26px; display:flex; align-items:flex-end; justify-content:space-between; flex-wrap:wrap; gap:12px; }
.roster-head h1{ font-family:var(--font-display); font-size:30px; color:var(--gold-bright); margin:0 0 4px; }
.roster-head p{ color:var(--text-faint); margin:0; font-size:13px; }
.char-grid{ display:grid; grid-template-columns:repeat(auto-fill, minmax(190px, 1fr)); gap:20px; }
.char-card{ position:relative; border-radius:16px; overflow:hidden; cursor:pointer; aspect-ratio:3/4.3;
  background:linear-gradient(160deg, var(--void-2), var(--void-1)); border:1.5px solid var(--panel-border);
  transform:perspective(700px) rotateX(var(--rx,0deg)) rotateY(var(--ry,0deg)); transition:transform .2s ease, box-shadow .25s ease; }
.char-card:hover{ box-shadow:0 0 0 1.5px var(--gold), 0 18px 34px rgba(216,180,99,.2); }
.char-card-art{ position:absolute; inset:0; }
.char-card-art img{ width:100%; height:100%; object-fit:cover; }
.char-card-fallback{ width:100%; height:100%; display:flex; align-items:center; justify-content:center; color:var(--gold-dim); }
.char-card-shine{ position:absolute; inset:0; background:linear-gradient(115deg, transparent 40%, rgba(245,220,156,.35) 50%, transparent 60%);
  background-size:250% 250%; background-position:-150% 0; opacity:0; transition:opacity .3s ease; }
.char-card:hover .char-card-shine{ opacity:1; animation:shimmerSweep 1.1s ease; }
@keyframes shimmerSweep{ from{ background-position:-150% 0; } to{ background-position:250% 0; } }
.char-card-plate{ position:absolute; left:0; right:0; bottom:0; padding:12px 12px 10px; background:linear-gradient(0deg, rgba(4,5,10,.92), rgba(4,5,10,0)); }
.char-card-plate h3{ font-family:var(--font-display); font-size:15px; color:var(--gold-bright); margin:0; }
.char-card-plate p{ font-size:11px; color:var(--text-dim); margin:2px 0 0; }
.card-admin-controls{ position:absolute; top:8px; right:8px; z-index:3; display:flex; gap:6px; }

/* ---------- profile ---------- */
.profile-hero{ display:flex; gap:26px; align-items:flex-start; margin-bottom:26px; flex-wrap:wrap; }
.portrait-frame{ position:relative; width:150px; height:190px; border-radius:16px; overflow:hidden; flex-shrink:0;
  background:linear-gradient(160deg, var(--void-2), var(--void-1)); border:2px solid var(--gold-dim); box-shadow:0 0 24px rgba(216,180,99,.18); }
.portrait-frame img{ width:100%; height:100%; object-fit:cover; }
.portrait-fallback{ width:100%; height:100%; display:flex; align-items:center; justify-content:center; color:var(--gold-dim); }
.portrait-ring{ position:absolute; inset:-1px; border-radius:16px; box-shadow:inset 0 0 0 1px rgba(245,220,156,.25); pointer-events:none; }
.hero-info{ flex:1; min-width:220px; padding-top:4px; }
.hero-story{ font-size:11px; letter-spacing:.1em; text-transform:uppercase; color:var(--text-faint); }
.hero-info h1{ font-family:var(--font-display); font-size:32px; color:var(--gold-bright); margin:4px 0 2px; text-shadow:0 0 20px rgba(216,180,99,.25); }
.hero-name-input{ font-family:var(--font-display); font-size:30px; color:var(--gold-bright); background:transparent; border:none;
  border-bottom:1px dashed rgba(216,180,99,.35); padding:2px 0; margin:4px 0 2px; width:100%; max-width:420px; }
.hero-subtitle{ color:var(--text-dim); font-size:14px; margin:0 0 10px; font-style:italic; }
.hero-subtitle-input{ background:transparent; border:none; border-bottom:1px dashed rgba(255,255,255,.15); color:var(--text-dim);
  font-size:13.5px; font-style:italic; padding:3px 0; margin-bottom:10px; width:100%; max-width:340px; }
.hero-admin-fields{ width:170px; }
.tag-list{ display:flex; flex-wrap:wrap; gap:6px; align-items:center; }
.tag-list.readonly{ margin-top:8px; }
.tag-pill{ display:inline-flex; align-items:center; gap:5px; background:rgba(216,180,99,.1); border:1px solid rgba(216,180,99,.28);
  color:var(--gold-bright); font-size:11px; padding:4px 9px; border-radius:999px; }
.tag-pill button{ background:none; border:none; color:var(--gold-dim); display:flex; }
.tag-pill.editable{ padding:2px 4px 2px 9px; }
.pill-input{ background:transparent; border:none; color:var(--gold-bright); font-size:11px; width:70px; }
.tag-input{ background:rgba(255,255,255,.04); border:1px dashed rgba(255,255,255,.15); color:var(--text-dim); font-size:11px;
  padding:4px 9px; border-radius:999px; width:70px; }

.tab-rail{ display:flex; gap:6px; margin-bottom:22px; overflow-x:auto; padding-bottom:6px; border-bottom:1px solid rgba(255,255,255,.08); }
.tab-btn{ display:flex; align-items:center; gap:7px; background:none; border:none; color:var(--text-faint); font-size:13px;
  padding:10px 16px; border-radius:10px 10px 0 0; white-space:nowrap; position:relative; transition:color .2s ease; }
.tab-btn:hover{ color:var(--text-dim); }
.tab-btn-active{ color:var(--gold-bright); }
.tab-btn-active::after{ content:''; position:absolute; left:10px; right:10px; bottom:-7px; height:2px;
  background:linear-gradient(90deg, transparent, var(--gold-bright), transparent); box-shadow:0 0 10px var(--gold-bright); }
.tab-content{ animation:fadeSlideIn .35s ease; }

.overview-grid{ display:grid; grid-template-columns:1.3fr 1fr; gap:18px; }
.points-panel{ grid-column:1 / -1; }
.points-display{ text-align:center; padding:6px 0 4px; }
.points-number{ font-family:var(--font-mono); font-size:38px; color:var(--gold-bright); text-shadow:0 0 20px rgba(216,180,99,.4); }
.increment-row{ display:flex; flex-wrap:wrap; gap:6px; justify-content:center; margin-top:10px; }
.increment-row.small{ justify-content:flex-end; }
.lore-textarea{ min-height:160px; }
.lore-text{ color:var(--text-dim); line-height:1.7; font-size:13.5px; white-space:pre-wrap; }
.points-reminder{ display:inline-flex; align-items:center; gap:7px; color:var(--gold-bright); font-size:12.5px;
  background:rgba(216,180,99,.08); border:1px solid rgba(216,180,99,.25); padding:8px 14px; border-radius:10px; margin-bottom:16px; }

/* ---------- meters ---------- */
.meter-block{ margin-bottom:16px; }
.meter-block:last-child{ margin-bottom:0; }
.meter-block-primary{ margin-bottom:22px; }
.meter-head{ display:flex; justify-content:space-between; align-items:baseline; margin-bottom:6px; }
.meter-name{ font-size:12.5px; letter-spacing:.03em; color:var(--text-dim); }
.meter-block-primary .meter-name{ font-family:var(--font-display); font-size:16px; }
.meter-value{ font-family:var(--font-mono); font-size:13px; }
.meter-block-primary .meter-value{ font-size:20px; }
.meter-gold{ color:var(--gold-bright); } .meter-cyan{ color:var(--cyan); } .meter-emerald{ color:var(--emerald); }
.meter-crimson{ color:var(--crimson); } .meter-magenta{ color:var(--magenta); }
.meter-slider{ -webkit-appearance:none; appearance:none; width:100%; height:8px; border-radius:999px; outline:none;
  background:rgba(255,255,255,.08); cursor:pointer; }
.meter-slider:disabled{ cursor:default; opacity:.85; }
.meter-slider::-webkit-slider-thumb{ -webkit-appearance:none; width:16px; height:16px; border-radius:50%; background:#fff;
  box-shadow:0 0 8px rgba(0,0,0,.4); border:2px solid var(--gold-bright); }
.meter-slider::-moz-range-thumb{ width:14px; height:14px; border-radius:50%; background:#fff; border:2px solid var(--gold-bright); }
.meter-slider-gold{ background:linear-gradient(to right, var(--gold) var(--pct), rgba(255,255,255,.08) var(--pct)); }
.meter-slider-cyan{ background:linear-gradient(to right, var(--cyan) var(--pct), rgba(255,255,255,.08) var(--pct)); }
.meter-slider-emerald{ background:linear-gradient(to right, var(--emerald) var(--pct), rgba(255,255,255,.08) var(--pct)); }
.meter-slider-crimson{ background:linear-gradient(to right, var(--crimson) var(--pct), rgba(255,255,255,.08) var(--pct)); }
.meter-slider-magenta{ background:linear-gradient(to right, var(--magenta) var(--pct), rgba(255,255,255,.08) var(--pct)); }

/* ---------- stats ---------- */
.stats-tab{ display:flex; flex-direction:column; gap:16px; }
.stat-category-panel h3{ font-family:var(--font-display); }
.stat-rows{ display:flex; flex-direction:column; gap:12px; }
.stat-row{ display:flex; align-items:center; gap:14px; flex-wrap:wrap; padding:10px 0; border-bottom:1px dashed rgba(255,255,255,.06); }
.stat-row:last-child{ border-bottom:none; }
.stat-name{ min-width:120px; font-size:13.5px; color:var(--text); }
.stat-value{ font-family:var(--font-mono); font-size:18px; color:var(--gold-bright); min-width:70px; }
.stat-number{ font-family:var(--font-mono); }
.stat-number-flash{ animation:numberFlash .6s ease; }
@keyframes numberFlash{ 0%{ text-shadow:0 0 16px rgba(245,220,156,.95), 0 0 3px #fff; } 100%{ text-shadow:none; } }

/* ---------- schema editor ---------- */
.settings-section{ margin-bottom:22px; }
.settings-heading{ display:flex; align-items:center; gap:7px; font-size:13px; text-transform:uppercase; letter-spacing:.06em;
  color:var(--gold-dim); margin:0 0 12px; }
.settings-heading.danger{ color:#e8909b; }
.schema-category{ background:rgba(255,255,255,.03); border:1px solid rgba(255,255,255,.07); border-radius:12px; padding:12px 14px; margin-bottom:10px; }
.schema-category-head{ display:flex; gap:8px; align-items:center; margin-bottom:8px; }
.schema-stat-list{ display:flex; flex-direction:column; gap:6px; }
.schema-stat-row{ display:flex; gap:8px; align-items:center; }
.add-row{ opacity:.8; }
.add-category-row{ display:flex; gap:8px; align-items:center; }
.pill-editor{ display:flex; flex-wrap:wrap; gap:8px; margin-bottom:12px; }
.form-grid-2{ display:grid; grid-template-columns:1fr 1fr; gap:20px; margin-bottom:20px; }
.form-row-2{ display:grid; grid-template-columns:1fr 1fr; gap:10px; }
.req-grid{ display:grid; grid-template-columns:repeat(auto-fill, minmax(160px,1fr)); gap:8px; }
.req-chip{ display:flex; align-items:center; justify-content:space-between; gap:6px; background:rgba(255,255,255,.03);
  border:1px solid rgba(255,255,255,.08); border-radius:9px; padding:7px 10px; font-size:12px; color:var(--text-faint); }
.req-chip label{ display:flex; align-items:center; gap:7px; }
.req-chip-active{ border-color:rgba(216,180,99,.35); color:var(--text); background:rgba(216,180,99,.06); }
.req-value{ width:54px; background:rgba(6,7,15,.7); border:1px solid rgba(255,255,255,.12); color:var(--gold-bright);
  border-radius:6px; padding:3px 5px; font-family:var(--font-mono); font-size:12px; }
.modal-actions{ display:flex; justify-content:flex-end; align-items:center; gap:14px; margin-top:6px; }
.danger-zone{ border-top:1px solid rgba(209,73,91,.2); padding-top:16px; }

/* ---------- gem rating ---------- */
.gem-rating-row{ display:flex; align-items:center; gap:12px; margin-bottom:9px; }
.gem-rating-row:last-child{ margin-bottom:0; }
.gem-rating-label{ display:flex; align-items:center; gap:5px; font-size:11px; color:var(--text-faint); min-width:44px;
  text-transform:uppercase; letter-spacing:.05em; }
.gem-rating{ display:flex; gap:5px; }
.gem{ width:14px; height:14px; background:rgba(255,255,255,.08); border:1px solid rgba(255,255,255,.15);
  transform:rotate(45deg); border-radius:3px; transition:all .15s ease; }
.gem-rating:not(.gem-rating-readonly) .gem{ cursor:pointer; }
.gem-rating:not(.gem-rating-readonly) .gem:hover{ transform:rotate(45deg) scale(1.25); }
.gem-filled{ background:linear-gradient(135deg, var(--gold), var(--gold-bright)); border-color:var(--gold-bright);
  box-shadow:0 0 8px rgba(245,220,156,.55); }

/* ---------- moves ---------- */
.section-toolbar{ display:flex; justify-content:flex-end; margin-bottom:16px; }
.move-grid{ display:grid; grid-template-columns:repeat(auto-fill, minmax(260px, 1fr)); gap:18px; }
.move-card{ position:relative; background:var(--panel-bg); border:1px solid var(--panel-border); border-radius:16px;
  overflow:hidden; display:flex; flex-direction:column; transition:box-shadow .25s ease, transform .2s ease; }
.move-card:hover{ transform:translateY(-2px); box-shadow:0 14px 30px rgba(0,0,0,.3); }
.move-card-unlockable{ border-color:rgba(216,180,99,.55); animation:glowPulse 2.4s ease-in-out infinite; }
.move-card-art{ position:relative; height:120px; background:linear-gradient(150deg, var(--void-2), var(--void-1)); }
.move-card-art img{ width:100%; height:100%; object-fit:cover; }
.move-card-art-fallback{ width:100%; height:100%; display:flex; align-items:center; justify-content:center; color:var(--gold-dim); }
.move-card-locked .move-card-art img{ filter:grayscale(1) brightness(.4); }
.move-lock-overlay{ position:absolute; inset:0; display:flex; align-items:center; justify-content:center; color:var(--gold-dim);
  background:rgba(4,5,10,.4); }
.move-card-body{ padding:14px 16px 16px; flex:1; display:flex; flex-direction:column; }
.move-card-top{ display:flex; justify-content:space-between; align-items:flex-start; gap:8px; margin-bottom:6px; }
.move-card-top h4{ font-family:var(--font-display); font-size:15.5px; color:var(--text); margin:0; }
.move-category-tag{ font-size:10px; text-transform:uppercase; letter-spacing:.05em; color:var(--cyan); white-space:nowrap;
  background:rgba(63,182,201,.1); border:1px solid rgba(63,182,201,.25); padding:2px 7px; border-radius:999px; }
.move-desc{ font-size:12.5px; color:var(--text-dim); line-height:1.5; margin:0 0 10px; }
.move-ratings{ display:flex; flex-direction:column; gap:4px; margin-bottom:8px; }
.move-meta-row{ display:flex; gap:14px; font-size:11.5px; color:var(--text-faint); font-family:var(--font-mono); margin-bottom:8px; }
.move-meta-row span{ display:flex; align-items:center; gap:4px; }
.req-progress-list{ display:flex; flex-direction:column; gap:8px; margin-top:6px; }
.req-progress{ display:grid; grid-template-columns:70px 1fr 50px; align-items:center; gap:8px; font-size:11px; color:var(--text-faint); }
.req-progress.req-met{ color:#8ee6a8; }
.req-bar{ height:5px; border-radius:999px; background:rgba(255,255,255,.08); overflow:hidden; }
.req-bar-fill{ height:100%; background:linear-gradient(90deg, var(--gold-dim), var(--gold-bright)); transition:width .5s ease; }
.req-nums{ font-family:var(--font-mono); text-align:right; }

/* ---------- equipment ---------- */
.equipment-grid{ display:grid; grid-template-columns:repeat(auto-fill, minmax(220px, 1fr)); gap:18px; }
.equipment-card{ position:relative; background:var(--panel-bg); border:1px solid var(--panel-border); border-radius:16px; padding:16px; }
.equipment-art{ height:110px; border-radius:12px; overflow:hidden; margin-bottom:12px; background:linear-gradient(150deg, var(--void-2), var(--void-1)); }
.equipment-art img{ width:100%; height:100%; object-fit:cover; }
.equipment-art-fallback{ width:100%; height:100%; display:flex; align-items:center; justify-content:center; color:var(--gold-dim); }
.equipment-card h4{ font-family:var(--font-display); font-size:15px; color:var(--text); margin:0 0 6px; }
.equip-desc{ font-size:12.5px; color:var(--text-dim); line-height:1.5; margin:0 0 8px; }
.equip-effects{ display:flex; align-items:center; gap:6px; font-size:11.5px; color:var(--gold-bright); margin-bottom:6px; }
.equip-notes{ font-size:11.5px; color:var(--text-faint); font-style:italic; margin:0; }

/* ---------- history ---------- */
.history-timeline{ display:flex; flex-direction:column; gap:0; position:relative; padding-left:18px; }
.history-timeline::before{ content:''; position:absolute; left:4px; top:6px; bottom:6px; width:1px; background:linear-gradient(180deg, rgba(216,180,99,.5), transparent); }
.history-item{ position:relative; padding:0 0 18px 14px; }
.history-dot{ position:absolute; left:-18px; top:4px; width:9px; height:9px; border-radius:50%; background:var(--gold-bright); box-shadow:0 0 8px rgba(245,220,156,.6); }
.history-content p{ margin:0; font-size:13px; color:var(--text); }
.history-time{ font-size:10.5px; color:var(--text-faint); font-family:var(--font-mono); }

/* ---------- modal ---------- */
.modal-overlay{ position:fixed; inset:0; z-index:100; background:rgba(3,4,9,.72); backdrop-filter:blur(4px);
  display:flex; align-items:center; justify-content:center; padding:24px; animation:fadeIn .2s ease; }
@keyframes fadeIn{ from{ opacity:0; } to{ opacity:1; } }
.modal{ width:100%; max-width:460px; max-height:86vh; overflow-y:auto; background:var(--panel-bg-solid);
  border:1px solid var(--panel-border); border-radius:18px; padding:22px 24px 24px; box-shadow:0 30px 70px rgba(0,0,0,.5);
  animation:popIn .28s cubic-bezier(.2,.9,.3,1.1); }
.modal-wide{ max-width:680px; }
@keyframes popIn{ from{ opacity:0; transform:scale(.94) translateY(8px); } to{ opacity:1; transform:scale(1) translateY(0); } }
.modal-head{ display:flex; justify-content:space-between; align-items:center; margin-bottom:18px; }
.modal-head h3{ font-family:var(--font-display); font-size:18px; color:var(--gold-bright); margin:0; }

/* ---------- auth / passwords ---------- */
.auth-hint{ color:var(--text-dim); font-size:13px; line-height:1.5; margin:0 0 14px; }
.auth-error{ color:#e8909b; font-size:12.5px; margin:-4px 0 10px; }
.password-field-row{ display:flex; gap:8px; align-items:center; margin-bottom:6px; }
.password-field-row .inline-input{ margin-bottom:0; }
.copied-hint{ color:#8ee6a8; font-size:11.5px; margin:0 0 8px; }
.field-hint{ color:var(--text-faint); font-size:11.5px; font-style:italic; margin:0 0 12px; line-height:1.5; }
.char-card-lock-badge{ position:absolute; top:8px; left:8px; z-index:3; display:flex; align-items:center;
  justify-content:center; width:24px; height:24px; border-radius:50%; background:rgba(6,7,15,.75);
  border:1px solid rgba(216,180,99,.4); color:var(--gold-bright); }

/* ---------- image field ---------- */
.image-field{ margin-bottom:14px; }
.image-preview{ width:100%; max-width:220px; border-radius:12px; overflow:hidden; background:linear-gradient(150deg, var(--void-2), var(--void-1));
  border:1px solid rgba(255,255,255,.1); margin-bottom:8px; }
.image-preview img{ width:100%; height:100%; object-fit:cover; }
.image-placeholder{ width:100%; height:100%; min-height:90px; display:flex; align-items:center; justify-content:center; color:var(--gold-dim); }

@keyframes glowPulse{ 0%,100%{ box-shadow:0 0 8px rgba(216,180,99,.28); } 50%{ box-shadow:0 0 22px rgba(216,180,99,.55); } }

/* ---------- responsive ---------- */
@media (max-width:720px){
  .app-header{ padding:12px 16px; }
  .app-main{ padding:22px 14px 90px; }
  .home-title h1{ font-size:30px; }
  .overview-grid{ grid-template-columns:1fr; }
  .form-grid-2{ grid-template-columns:1fr; }
  .profile-hero{ flex-direction:column; align-items:center; text-align:center; }
  .hero-info{ text-align:center; }
  .tag-list{ justify-content:center; }
}

@media (prefers-reduced-motion: reduce){
  *{ animation-duration:.01ms !important; animation-iteration-count:1 !important; transition-duration:.01ms !important; }
}
`;

/* ============================== small components ============================== */

function CosmicBackground() {
  const stars = useMemo(() => Array.from({ length: 110 }).map((_, i) => ({
    id: i, top: Math.random() * 100, left: Math.random() * 100,
    size: Math.random() * 2 + 0.6, delay: Math.random() * 6, dur: Math.random() * 3 + 2.5,
    gold: Math.random() > 0.82,
  })), []);
  const motes = useMemo(() => Array.from({ length: 16 }).map((_, i) => ({
    id: i, left: Math.random() * 100, size: Math.random() * 3 + 2,
    dur: Math.random() * 16 + 18, delay: Math.random() * 30,
  })), []);
  return (
    <div className="cosmic-bg" aria-hidden="true">
      <div className="nebula nebula-a" />
      <div className="nebula nebula-b" />
      <div className="nebula nebula-c" />
      <div className="star-field">
        {stars.map((s) => (
          <span key={s.id} className={"star" + (s.gold ? " star-gold" : "")}
            style={{ top: s.top + "%", left: s.left + "%", width: s.size + "px", height: s.size + "px", animationDelay: s.delay + "s", animationDuration: s.dur + "s" }} />
        ))}
      </div>
      <div className="mote-field">
        {motes.map((m) => (
          <span key={m.id} className="mote"
            style={{ left: m.left + "%", width: m.size + "px", height: m.size + "px", animationDuration: m.dur + "s", animationDelay: "-" + m.delay + "s" }} />
        ))}
      </div>
      <div className="vignette" />
    </div>
  );
}

function GlowPanel({ children, className = "" }) {
  return <section className={"glow-panel " + className}>{children}</section>;
}

function AnimatedNumber({ value, className = "" }) {
  const [display, setDisplay] = useState(value);
  const prevRef = useRef(value);
  const [flash, setFlash] = useState(false);
  const rafRef = useRef(null);

  useEffect(() => {
    const from = prevRef.current;
    const to = value;
    if (from === to) return;
    const start = performance.now();
    const dur = 550;
    setFlash(true);
    cancelAnimationFrame(rafRef.current);
    const step = (now) => {
      const t = clamp((now - start) / dur, 0, 1);
      const eased = 1 - Math.pow(1 - t, 3);
      setDisplay(from + (to - from) * eased);
      if (t < 1) {
        rafRef.current = requestAnimationFrame(step);
      } else {
        setDisplay(to);
        prevRef.current = to;
        setTimeout(() => setFlash(false), 250);
      }
    };
    rafRef.current = requestAnimationFrame(step);
    return () => cancelAnimationFrame(rafRef.current);
  }, [value]);

  return <span className={"stat-number " + (flash ? "stat-number-flash " : "") + className}>{fmt(display)}</span>;
}

function GemRating({ value = 0, max = 7, onChange, readOnly, label, Icon }) {
  const [hover, setHover] = useState(null);
  const shown = hover ?? value;
  return (
    <div className="gem-rating-row">
      {label && <span className="gem-rating-label">{Icon && <Icon size={12} />} {label}</span>}
      <div className={"gem-rating" + (readOnly ? " gem-rating-readonly" : "")} onMouseLeave={() => setHover(null)}>
        {Array.from({ length: max }).map((_, i) => {
          const idx = i + 1;
          const filled = idx <= shown;
          return (
            <span
              key={i}
              className={"gem" + (filled ? " gem-filled" : "")}
              onMouseEnter={() => !readOnly && setHover(idx)}
              onClick={() => !readOnly && onChange && onChange(idx)}
            />
          );
        })}
      </div>
    </div>
  );
}

function MeterSlider({ meterDef, value, onChange, readOnly, primary }) {
  return (
    <div className={"meter-block" + (primary ? " meter-block-primary" : "")}>
      <div className="meter-head">
        <span className={"meter-name meter-" + meterDef.color}>{meterDef.name}</span>
        <AnimatedNumber value={value} className={"meter-value meter-" + meterDef.color} />
      </div>
      <input
        type="range" min={0} max={10} step={1} value={value}
        disabled={readOnly}
        onChange={(e) => onChange(Number(e.target.value))}
        className={"meter-slider meter-slider-" + meterDef.color}
        style={{ "--pct": (value / 10) * 100 + "%" }}
      />
    </div>
  );
}

function Modal({ title, onClose, children, wide }) {
  useEffect(() => {
    const onKey = (e) => { if (e.key === "Escape") onClose(); };
    window.addEventListener("keydown", onKey);
    return () => window.removeEventListener("keydown", onKey);
  }, [onClose]);
  return (
    <div className="modal-overlay" onClick={onClose}>
      <div className={"modal" + (wide ? " modal-wide" : "")} onClick={(e) => e.stopPropagation()}>
        <div className="modal-head">
          <h3>{title}</h3>
          <button className="icon-btn" onClick={onClose}><X size={17} /></button>
        </div>
        <div>{children}</div>
      </div>
    </div>
  );
}

function ConfirmButton({ onConfirm, label = "Delete", confirmLabel = "Confirm?", Icon = Trash2 }) {
  const [confirming, setConfirming] = useState(false);
  useEffect(() => {
    if (!confirming) return;
    const t = setTimeout(() => setConfirming(false), 3000);
    return () => clearTimeout(t);
  }, [confirming]);
  if (confirming) {
    return (
      <button className="danger-btn confirming" onClick={(e) => { e.stopPropagation(); onConfirm(); }}>
        {confirmLabel}
      </button>
    );
  }
  return (
    <button className="danger-btn" onClick={(e) => { e.stopPropagation(); setConfirming(true); }}>
      <Icon size={13} /> {label}
    </button>
  );
}

function ImageUrlField({ value, onChange, placeholder = "Paste image URL…", ratio = "1/1" }) {
  const [broken, setBroken] = useState(false);
  return (
    <div className="image-field">
      <div className="image-preview" style={{ aspectRatio: ratio }}>
        {value && !broken ? (
          <img src={value} alt="" onError={() => setBroken(true)} onLoad={() => setBroken(false)} />
        ) : (
          <div className="image-placeholder"><ImageIcon size={26} /></div>
        )}
      </div>
      <input
        type="text" value={value || ""} placeholder={placeholder}
        onChange={(e) => { setBroken(false); onChange(e.target.value); }}
        className="text-input"
      />
    </div>
  );
}

function TagList({ tags = [], onChange, readOnly }) {
  const [draft, setDraft] = useState("");
  const add = () => {
    const t = draft.trim();
    if (!t) return;
    if (!tags.includes(t)) onChange([...tags, t]);
    setDraft("");
  };
  return (
    <div className="tag-list">
      {tags.map((t) => (
        <span key={t} className="tag-pill">
          {t}
          {!readOnly && <button onClick={() => onChange(tags.filter((x) => x !== t))}><X size={11} /></button>}
        </span>
      ))}
      {!readOnly && (
        <input
          className="tag-input" value={draft} placeholder="+ tag"
          onChange={(e) => setDraft(e.target.value)}
          onKeyDown={(e) => { if (e.key === "Enter") { e.preventDefault(); add(); } }}
          onBlur={add}
        />
      )}
    </div>
  );
}

function HistoryList({ entries = [] }) {
  const sorted = [...entries].sort((a, b) => b.timestamp - a.timestamp);
  if (!sorted.length) return <div className="empty-note">No history yet. Actions will appear here as this character grows.</div>;
  return (
    <div className="history-timeline">
      {sorted.map((e) => (
        <div key={e.id} className="history-item">
          <span className="history-dot" />
          <div className="history-content">
            <p>{e.text}</p>
            <span className="history-time">{timeAgo(e.timestamp)}</span>
          </div>
        </div>
      ))}
    </div>
  );
}

/* ============================== auth modals ============================== */

function PasswordGateModal({ mode, label, onValidate, onSuccess, onClose }) {
  const [pw, setPw] = useState("");
  const [confirm, setConfirm] = useState("");
  const [error, setError] = useState("");
  const isCreate = mode === "admin-create";
  const title = isCreate ? "Create Admin Password" : mode === "admin-enter" ? "Admin Access" : "Locked Character";

  const submit = () => {
    if (isCreate) {
      if (pw.trim().length < 4) { setError("Use at least 4 characters."); return; }
      if (pw !== confirm) { setError("Passwords don't match."); return; }
      onSuccess(pw);
      return;
    }
    if (!onValidate(pw)) { setError("Incorrect password."); setPw(""); return; }
    onSuccess(pw);
  };

  return (
    <Modal title={title} onClose={onClose}>
      {mode === "character-enter" && <p className="auth-hint">Enter the password for <strong>{label}</strong> to view this character.</p>}
      {mode === "admin-enter" && <p className="auth-hint">Enter the Admin password to continue.</p>}
      {isCreate && <p className="auth-hint">Set a password to protect the Admin panel. You can change it later.</p>}
      <input
        type="password" className="text-input" autoFocus placeholder="Password"
        value={pw} onChange={(e) => { setPw(e.target.value); setError(""); }}
        onKeyDown={(e) => { if (e.key === "Enter" && !isCreate) submit(); }}
      />
      {isCreate && (
        <input
          type="password" className="text-input" placeholder="Confirm password"
          value={confirm} onChange={(e) => { setConfirm(e.target.value); setError(""); }}
          onKeyDown={(e) => { if (e.key === "Enter") submit(); }}
        />
      )}
      {error && <p className="auth-error">{error}</p>}
      <div className="modal-actions">
        <button className="gold-btn" onClick={submit}><Check size={15} /> {isCreate ? "Set Password" : "Unlock"}</button>
      </div>
    </Modal>
  );
}

function ChangeAdminPasswordModal({ currentPassword, onSave, onClose }) {
  const [current, setCurrent] = useState("");
  const [next, setNext] = useState("");
  const [confirm, setConfirm] = useState("");
  const [error, setError] = useState("");

  const submit = () => {
    if (current !== currentPassword) { setError("Current password is incorrect."); return; }
    if (next.trim().length < 4) { setError("New password must be at least 4 characters."); return; }
    if (next !== confirm) { setError("New passwords don't match."); return; }
    onSave(next);
  };

  return (
    <Modal title="Change Admin Password" onClose={onClose}>
      <label className="field-label">Current Password</label>
      <input type="password" className="text-input" value={current} onChange={(e) => { setCurrent(e.target.value); setError(""); }} />
      <label className="field-label">New Password</label>
      <input type="password" className="text-input" value={next} onChange={(e) => { setNext(e.target.value); setError(""); }} />
      <label className="field-label">Confirm New Password</label>
      <input type="password" className="text-input" value={confirm} onChange={(e) => { setConfirm(e.target.value); setError(""); }} />
      {error && <p className="auth-error">{error}</p>}
      <div className="modal-actions">
        <button className="gold-btn" onClick={submit}><Check size={15} /> Save Password</button>
      </div>
    </Modal>
  );
}

/* ============================== editor modals ============================== */

function StoryEditorModal({ initial, onSave, onClose }) {
  const [s, setS] = useState(() => initial
    ? { title: initial.title, subtitle: initial.subtitle || "", coverImage: initial.coverImage || "" }
    : { title: "", subtitle: "", coverImage: "" });
  const set = (p) => setS((prev) => ({ ...prev, ...p }));
  return (
    <Modal title={initial ? "Edit Story" : "New Story"} onClose={onClose}>
      <label className="field-label">Title</label>
      <input className="text-input" value={s.title} onChange={(e) => set({ title: e.target.value })} placeholder="Story title" />
      <label className="field-label">Subtitle</label>
      <input className="text-input" value={s.subtitle} onChange={(e) => set({ subtitle: e.target.value })} placeholder="A short tagline" />
      <label className="field-label">Cover Image</label>
      <ImageUrlField value={s.coverImage} onChange={(v) => set({ coverImage: v })} ratio="16/9" />
      <div className="modal-actions">
        <button className="gold-btn" onClick={() => { if (s.title.trim()) onSave(s); }}><Check size={15} /> Save</button>
      </div>
    </Modal>
  );
}

function CharacterEditorModal({ initial, onSave, onClose }) {
  const [c, setC] = useState(() => initial
    ? { name: initial.name, subtitle: initial.subtitle || "", portrait: initial.portrait || "", password: initial.password || "" }
    : { name: "", subtitle: "", portrait: "", password: "" });
  const [copied, setCopied] = useState(false);
  const set = (p) => setC((prev) => ({ ...prev, ...p }));
  const copyPw = async () => {
    if (!c.password) return;
    try {
      await navigator.clipboard.writeText(c.password);
      setCopied(true);
      setTimeout(() => setCopied(false), 1500);
    } catch (e) { /* clipboard unavailable in this context */ }
  };
  return (
    <Modal title={initial ? "Edit Character" : "New Character"} onClose={onClose}>
      <label className="field-label">Name</label>
      <input className="text-input" value={c.name} onChange={(e) => set({ name: e.target.value })} placeholder="Character name" />
      <label className="field-label">Subtitle</label>
      <input className="text-input" value={c.subtitle} onChange={(e) => set({ subtitle: e.target.value })} placeholder="e.g. The Fallen Blade" />
      <label className="field-label">Portrait</label>
      <ImageUrlField value={c.portrait} onChange={(v) => set({ portrait: v })} ratio="3/4" />
      <label className="field-label">Player Password (optional)</label>
      <div className="password-field-row">
        <input className="text-input inline-input" value={c.password}
          onChange={(e) => set({ password: e.target.value })} placeholder="Leave blank for open access" />
        <button type="button" className="icon-btn" title="Generate password" onClick={() => set({ password: genPassword() })}><Shuffle size={14} /></button>
        <button type="button" className="icon-btn" title="Copy password" onClick={copyPw}><Copy size={14} /></button>
      </div>
      {copied && <p className="copied-hint">Copied to clipboard</p>}
      <p className="field-hint">Give this password to the player who owns {c.name.trim() || "this character"}. Leave it blank so anyone can open the card freely.</p>
      <div className="modal-actions">
        <button className="gold-btn" onClick={() => { if (c.name.trim()) onSave(c); }}><Check size={15} /> Save</button>
      </div>
    </Modal>
  );
}

function StorySettingsModal({ story, config, actions, onDeleteStory, onClose }) {
  const [newCatName, setNewCatName] = useState("");
  const [newStatDrafts, setNewStatDrafts] = useState({});
  const [newMoveCat, setNewMoveCat] = useState("");

  return (
    <Modal title={"Configure \"" + story.title + "\""} onClose={onClose} wide>
      <div className="settings-section">
        <label className="field-label">Story Title</label>
        <input className="text-input" value={story.title} onChange={(e) => actions.renameStory(e.target.value)} />
        <label className="field-label">Subtitle</label>
        <input className="text-input" value={story.subtitle || ""} onChange={(e) => actions.updateSubtitle(e.target.value)} />
        <label className="field-label">Cover Image</label>
        <ImageUrlField value={story.coverImage} onChange={actions.updateCover} ratio="16/9" />
      </div>

      <div className="settings-section">
        <h4 className="settings-heading"><Layers size={14} /> Stat Categories</h4>
        {config.statCategories.map((cat) => (
          <div key={cat.id} className="schema-category">
            <div className="schema-category-head">
              <input className="text-input inline-input" value={cat.name}
                onChange={(e) => actions.renameCategory(cat.id, e.target.value)} />
              <ConfirmButton label="" confirmLabel="Sure?" onConfirm={() => actions.deleteCategory(cat.id)} />
            </div>
            <div className="schema-stat-list">
              {cat.stats.map((s) => (
                <div key={s.id} className="schema-stat-row">
                  <input className="text-input inline-input small" value={s.name}
                    onChange={(e) => actions.renameStat(cat.id, s.id, e.target.value)} />
                  <button className="icon-btn danger" onClick={() => actions.deleteStat(cat.id, s.id)}><X size={13} /></button>
                </div>
              ))}
              <div className="schema-stat-row add-row">
                <input className="text-input inline-input small" placeholder="New stat…"
                  value={newStatDrafts[cat.id] || ""}
                  onChange={(e) => setNewStatDrafts({ ...newStatDrafts, [cat.id]: e.target.value })}
                  onKeyDown={(e) => {
                    if (e.key === "Enter" && (newStatDrafts[cat.id] || "").trim()) {
                      actions.addStat(cat.id, newStatDrafts[cat.id].trim());
                      setNewStatDrafts({ ...newStatDrafts, [cat.id]: "" });
                    }
                  }}
                />
                <button className="icon-btn" onClick={() => {
                  if ((newStatDrafts[cat.id] || "").trim()) {
                    actions.addStat(cat.id, newStatDrafts[cat.id].trim());
                    setNewStatDrafts({ ...newStatDrafts, [cat.id]: "" });
                  }
                }}><Plus size={13} /></button>
              </div>
            </div>
          </div>
        ))}
        <div className="add-category-row">
          <input className="text-input" placeholder="New category name…" value={newCatName}
            onChange={(e) => setNewCatName(e.target.value)}
            onKeyDown={(e) => { if (e.key === "Enter" && newCatName.trim()) { actions.addCategory(newCatName.trim()); setNewCatName(""); } }} />
          <button className="gold-btn small" onClick={() => { if (newCatName.trim()) { actions.addCategory(newCatName.trim()); setNewCatName(""); } }}>
            <Plus size={14} /> Add
          </button>
        </div>
      </div>

      <div className="settings-section">
        <h4 className="settings-heading"><Swords size={14} /> Move Categories</h4>
        <div className="pill-editor">
          {config.moveCategories.map((mc) => (
            <span key={mc.id} className="tag-pill editable">
              <input className="pill-input" value={mc.name} onChange={(e) => actions.renameMoveCategory(mc.id, e.target.value)} />
              <button onClick={() => actions.deleteMoveCategory(mc.id)}><X size={11} /></button>
            </span>
          ))}
        </div>
        <div className="add-category-row">
          <input className="text-input" placeholder="New move category…" value={newMoveCat}
            onChange={(e) => setNewMoveCat(e.target.value)}
            onKeyDown={(e) => { if (e.key === "Enter" && newMoveCat.trim()) { actions.addMoveCategory(newMoveCat.trim()); setNewMoveCat(""); } }} />
          <button className="gold-btn small" onClick={() => { if (newMoveCat.trim()) { actions.addMoveCategory(newMoveCat.trim()); setNewMoveCat(""); } }}>
            <Plus size={14} /> Add
          </button>
        </div>
      </div>

      <div className="settings-section danger-zone">
        <h4 className="settings-heading danger"><Trash2 size={14} /> Danger Zone</h4>
        <ConfirmButton label="Delete Story" confirmLabel="Really delete? This removes all its characters." onConfirm={onDeleteStory} />
      </div>
    </Modal>
  );
}

function MoveEditorModal({ initial, moveCategories, statOptions, onSave, onClose }) {
  const [m, setM] = useState(() => initial || {
    id: uid(), name: "", image: "", categoryId: moveCategories[0]?.id || "", description: "", notes: "",
    power: 1, range: 1, speed: 1, startup: 1, energyCost: "", cooldown: "", tags: [],
    unlockRequirements: {}, unlocked: false,
  });
  const set = (patch) => setM((prev) => ({ ...prev, ...patch }));

  const toggleReq = (statId) => {
    setM((prev) => {
      const req = { ...prev.unlockRequirements };
      if (statId in req) delete req[statId]; else req[statId] = 10;
      return { ...prev, unlockRequirements: req };
    });
  };
  const setReqValue = (statId, val) => {
    setM((prev) => ({ ...prev, unlockRequirements: { ...prev.unlockRequirements, [statId]: val } }));
  };

  return (
    <Modal title={initial ? "Edit Move" : "New Move"} onClose={onClose} wide>
      <div className="form-grid-2">
        <div>
          <label className="field-label">Name</label>
          <input className="text-input" value={m.name} onChange={(e) => set({ name: e.target.value })} placeholder="Heavenly Slash" />
          <label className="field-label">Category</label>
          <select className="text-input" value={m.categoryId} onChange={(e) => set({ categoryId: e.target.value })}>
            {moveCategories.map((c) => <option key={c.id} value={c.id}>{c.name}</option>)}
          </select>
          <label className="field-label">Image URL</label>
          <ImageUrlField value={m.image} onChange={(v) => set({ image: v })} ratio="4/3" />
          <label className="field-label">Tags (comma separated)</label>
          <input className="text-input" value={(m.tags || []).join(", ")}
            onChange={(e) => set({ tags: e.target.value.split(",").map((t) => t.trim()).filter(Boolean) })} />
          <div className="form-row-2">
            <div>
              <label className="field-label">Energy Cost</label>
              <input className="text-input" type="number" value={m.energyCost} onChange={(e) => set({ energyCost: e.target.value })} />
            </div>
            <div>
              <label className="field-label">Cooldown</label>
              <input className="text-input" type="number" value={m.cooldown} onChange={(e) => set({ cooldown: e.target.value })} />
            </div>
          </div>
        </div>
        <div>
          <label className="field-label">Description</label>
          <textarea className="text-input textarea" value={m.description} onChange={(e) => set({ description: e.target.value })} />
          <label className="field-label">Notes</label>
          <textarea className="text-input textarea" value={m.notes} onChange={(e) => set({ notes: e.target.value })} />
        </div>
      </div>

      <div className="settings-section">
        <h4 className="settings-heading"><Gauge size={14} /> Ratings</h4>
        <GemRating label="Power" Icon={Flame} value={m.power} onChange={(v) => set({ power: v })} />
        <GemRating label="Range" Icon={Target} value={m.range} onChange={(v) => set({ range: v })} />
        <GemRating label="Speed" Icon={Wind} value={m.speed} onChange={(v) => set({ speed: v })} />
        <GemRating label="Startup" Icon={Timer} value={m.startup} onChange={(v) => set({ startup: v })} />
      </div>

      <div className="settings-section">
        <h4 className="settings-heading"><Lock size={14} /> Unlock Requirements</h4>
        <div className="req-grid">
          {statOptions.map((s) => {
            const active = s.id in m.unlockRequirements;
            return (
              <div key={s.id} className={"req-chip" + (active ? " req-chip-active" : "")}>
                <label>
                  <input type="checkbox" checked={active} onChange={() => toggleReq(s.id)} />
                  {s.name}
                </label>
                {active && (
                  <input type="number" className="req-value" value={m.unlockRequirements[s.id]}
                    onChange={(e) => setReqValue(s.id, Number(e.target.value))} />
                )}
              </div>
            );
          })}
        </div>
      </div>

      <div className="modal-actions">
        <label className="checkbox-row">
          <input type="checkbox" checked={m.unlocked} onChange={(e) => set({ unlocked: e.target.checked })} />
          Force unlocked
        </label>
        <button className="gold-btn" onClick={() => { if (m.name.trim()) onSave(m); }}><Check size={15} /> Save Move</button>
      </div>
    </Modal>
  );
}

function EquipmentEditorModal({ initial, onSave, onClose }) {
  const [eq, setEq] = useState(() => initial || { id: uid(), name: "", image: "", description: "", effects: "", notes: "" });
  const set = (p) => setEq((prev) => ({ ...prev, ...p }));
  return (
    <Modal title={initial ? "Edit Equipment" : "New Equipment"} onClose={onClose}>
      <label className="field-label">Name</label>
      <input className="text-input" value={eq.name} onChange={(e) => set({ name: e.target.value })} />
      <label className="field-label">Image URL</label>
      <ImageUrlField value={eq.image} onChange={(v) => set({ image: v })} ratio="1/1" />
      <label className="field-label">Description</label>
      <textarea className="text-input textarea" value={eq.description} onChange={(e) => set({ description: e.target.value })} />
      <label className="field-label">Effects</label>
      <textarea className="text-input textarea" value={eq.effects} onChange={(e) => set({ effects: e.target.value })} />
      <label className="field-label">Notes</label>
      <textarea className="text-input textarea" value={eq.notes} onChange={(e) => set({ notes: e.target.value })} />
      <div className="modal-actions">
        <button className="gold-btn" onClick={() => { if (eq.name.trim()) onSave(eq); }}><Check size={15} /> Save Equipment</button>
      </div>
    </Modal>
  );
}

/* ============================== cards ============================== */

function StoryCard({ story, count, onOpen, admin, onEdit, onDelete }) {
  const ref = useRef(null);
  const onMove = (e) => {
    const el = ref.current; if (!el) return;
    const r = el.getBoundingClientRect();
    const x = (e.clientX - r.left) / r.width - 0.5;
    const y = (e.clientY - r.top) / r.height - 0.5;
    el.style.setProperty("--rx", -y * 6 + "deg");
    el.style.setProperty("--ry", x * 6 + "deg");
  };
  const onLeave = () => {
    const el = ref.current; if (!el) return;
    el.style.setProperty("--rx", "0deg"); el.style.setProperty("--ry", "0deg");
  };
  return (
    <div className="story-card" ref={ref} onMouseMove={onMove} onMouseLeave={onLeave} onClick={onOpen}>
      {admin && (
        <div className="card-admin-controls" onClick={(e) => e.stopPropagation()}>
          <button className="icon-btn" onClick={onEdit}><Edit3 size={13} /></button>
          <ConfirmButton label="" confirmLabel="Sure?" onConfirm={onDelete} />
        </div>
      )}
      <div className="story-card-cover">
        {story.coverImage ? <img src={story.coverImage} alt="" /> : <div className="story-card-fallback"><BookOpen size={34} /></div>}
      </div>
      <div className="story-card-body">
        <h2>{story.title}</h2>
        {story.subtitle && <p>{story.subtitle}</p>}
        <span className="story-count"><Users size={13} /> {count} {count === 1 ? "Character" : "Characters"}</span>
      </div>
    </div>
  );
}

function CharacterCard({ character, onOpen, admin, onEdit, onDelete }) {
  const ref = useRef(null);
  const onMove = (e) => {
    const el = ref.current; if (!el) return;
    const r = el.getBoundingClientRect();
    const x = (e.clientX - r.left) / r.width - 0.5;
    const y = (e.clientY - r.top) / r.height - 0.5;
    el.style.setProperty("--rx", -y * 10 + "deg");
    el.style.setProperty("--ry", x * 10 + "deg");
  };
  const onLeave = () => {
    const el = ref.current; if (!el) return;
    el.style.setProperty("--rx", "0deg"); el.style.setProperty("--ry", "0deg");
  };
  return (
    <div className="char-card" ref={ref} onMouseMove={onMove} onMouseLeave={onLeave} onClick={onOpen}>
      {admin && (
        <div className="card-admin-controls" onClick={(e) => e.stopPropagation()}>
          <button className="icon-btn" onClick={onEdit}><Edit3 size={13} /></button>
          <ConfirmButton label="" confirmLabel="Sure?" onConfirm={onDelete} />
        </div>
      )}
      {character.password && <span className="char-card-lock-badge"><Lock size={12} /></span>}
      <div className="char-card-art">
        {character.portrait ? <img src={character.portrait} alt="" /> : <div className="char-card-fallback"><User size={38} /></div>}
        <div className="char-card-shine" />
      </div>
      <div className="char-card-plate">
        <h3>{character.name}</h3>
        {character.subtitle && <p>{character.subtitle}</p>}
      </div>
    </div>
  );
}

function MoveCard({ move, category, statOptions, admin, character, onUnlock, onEdit, onDelete }) {
  const req = move.unlockRequirements || {};
  const reqEntries = Object.entries(req).map(([statId, need]) => {
    const stat = statOptions.find((s) => s.id === statId);
    const have = character.stats[statId] || 0;
    return { statId, name: stat ? stat.name : "Unknown", have, need, met: have >= need };
  });
  const allMet = reqEntries.every((r) => r.met);
  const locked = !move.unlocked;
  const unlockable = locked && allMet;

  return (
    <div className={"move-card" + (locked ? " move-card-locked" : "") + (unlockable ? " move-card-unlockable" : "")}>
      {admin && (
        <div className="card-admin-controls">
          <button className="icon-btn" onClick={() => onEdit(move)}><Edit3 size={13} /></button>
          <ConfirmButton label="" confirmLabel="Sure?" onConfirm={() => onDelete(move.id)} />
        </div>
      )}
      <div className="move-card-art">
        {move.image ? <img src={move.image} alt="" /> : <div className="move-card-art-fallback"><Swords size={28} /></div>}
        {locked && <div className="move-lock-overlay"><Lock size={20} /></div>}
      </div>
      <div className="move-card-body">
        <div className="move-card-top">
          <h4>{move.name}</h4>
          {category && <span className="move-category-tag">{category.name}</span>}
        </div>
        {!locked && move.description && <p className="move-desc">{move.description}</p>}
        {!locked && (
          <div className="move-ratings">
            <GemRating label="PWR" Icon={Flame} value={move.power} readOnly />
            <GemRating label="RNG" Icon={Target} value={move.range} readOnly />
            <GemRating label="SPD" Icon={Wind} value={move.speed} readOnly />
            <GemRating label="STU" Icon={Timer} value={move.startup} readOnly />
          </div>
        )}
        {!locked && (move.energyCost || move.cooldown) && (
          <div className="move-meta-row">
            {move.energyCost && <span><Zap size={12} /> {move.energyCost}</span>}
            {move.cooldown && <span><Clock size={12} /> {move.cooldown}</span>}
          </div>
        )}
        {!locked && move.tags && move.tags.length > 0 && (
          <div className="tag-list readonly">{move.tags.map((t) => <span key={t} className="tag-pill">{t}</span>)}</div>
        )}
        {locked && reqEntries.length > 0 && (
          <div className="req-progress-list">
            {reqEntries.map((r) => (
              <div key={r.statId} className={"req-progress" + (r.met ? " req-met" : "")}>
                <span>{r.name}</span>
                <div className="req-bar"><div className="req-bar-fill" style={{ width: clamp((r.have / r.need) * 100, 0, 100) + "%" }} /></div>
                <span className="req-nums">{fmt(r.have)}/{fmt(r.need)}</span>
              </div>
            ))}
          </div>
        )}
        {unlockable && <button className="unlock-btn" onClick={() => onUnlock(move.id)}><Unlock size={14} /> Unlock</button>}
      </div>
    </div>
  );
}

function EquipmentCard({ eq, admin, onEdit, onDelete }) {
  return (
    <div className="equipment-card">
      {admin && (
        <div className="card-admin-controls">
          <button className="icon-btn" onClick={() => onEdit(eq)}><Edit3 size={13} /></button>
          <ConfirmButton label="" confirmLabel="Sure?" onConfirm={() => onDelete(eq.id)} />
        </div>
      )}
      <div className="equipment-art">
        {eq.image ? <img src={eq.image} alt="" /> : <div className="equipment-art-fallback"><Package size={24} /></div>}
      </div>
      <h4>{eq.name}</h4>
      {eq.description && <p className="equip-desc">{eq.description}</p>}
      {eq.effects && <div className="equip-effects"><Sparkles size={12} /> {eq.effects}</div>}
      {eq.notes && <p className="equip-notes">{eq.notes}</p>}
    </div>
  );
}

/* ============================== screens ============================== */

function HomeScreen({ stories, characters, admin, actions, onOpenStory }) {
  const [creating, setCreating] = useState(false);
  const [editingStory, setEditingStory] = useState(null);
  const countFor = (storyId) => Object.values(characters).filter((c) => c.storyId === storyId).length;
  return (
    <div className="home-screen">
      <div className="home-title">
        <h1>CODEX</h1>
        <p>Choose a chronicle to enter</p>
      </div>
      <div className="story-grid">
        {stories.map((s) => (
          <StoryCard key={s.id} story={s} count={countFor(s.id)} onOpen={() => onOpenStory(s.id)}
            admin={admin} onEdit={() => setEditingStory(s)} onDelete={() => actions.deleteStory(s.id)} />
        ))}
        {admin && (
          <button className="add-card add-card-large" onClick={() => setCreating(true)}>
            <Plus size={32} /><span>New Story</span>
          </button>
        )}
        {stories.length === 0 && !admin && <div className="empty-note">No stories yet. Ask your Admin to add one.</div>}
      </div>
      {(creating || editingStory) && (
        <StoryEditorModal
          initial={editingStory}
          onSave={(data) => {
            if (editingStory) actions.updateStoryMeta(editingStory.id, data); else actions.addStory(data);
            setCreating(false); setEditingStory(null);
          }}
          onClose={() => { setCreating(false); setEditingStory(null); }}
        />
      )}
    </div>
  );
}

function RosterScreen({ story, config, characters, admin, actions, storySettingsActionsFor, onOpenCharacter, onBack }) {
  const [creating, setCreating] = useState(false);
  const [editingChar, setEditingChar] = useState(null);
  const [settingsOpen, setSettingsOpen] = useState(false);

  return (
    <div className="roster-screen">
      <button className="back-btn" onClick={onBack}><ChevronLeft size={16} /> Stories</button>
      <div className="roster-head">
        <div>
          <h1>{story.title}</h1>
          {story.subtitle && <p>{story.subtitle}</p>}
        </div>
        {admin && <button className="ghost-btn" onClick={() => setSettingsOpen(true)}><Settings size={15} /> Configure Story</button>}
      </div>
      <div className="char-grid">
        {characters.map((c) => (
          <CharacterCard key={c.id} character={c}
            onOpen={() => onOpenCharacter(c.id)} admin={admin}
            onEdit={() => setEditingChar(c)}
            onDelete={() => actions.deleteCharacter(c.id)} />
        ))}
        {admin && (
          <button className="add-card" onClick={() => setCreating(true)}>
            <Plus size={28} /><span>New Character</span>
          </button>
        )}
        {characters.length === 0 && !admin && <div className="empty-note">No characters here yet.</div>}
      </div>

      {(creating || editingChar) && (
        <CharacterEditorModal
          initial={editingChar}
          onSave={(data) => {
            if (editingChar) actions.updateCharacter(editingChar.id, data); else actions.addCharacter(story.id, data);
            setCreating(false); setEditingChar(null);
          }}
          onClose={() => { setCreating(false); setEditingChar(null); }}
        />
      )}
      {settingsOpen && (
        <StorySettingsModal story={story} config={config} actions={storySettingsActionsFor(story.id)}
          onDeleteStory={() => actions.deleteStory(story.id)}
          onClose={() => setSettingsOpen(false)} />
      )}
    </div>
  );
}

function CharacterProfileScreen({ character, story, config, admin, actions, onBack }) {
  const [tab, setTab] = useState("overview");
  const statFlat = flattenStats(config.statCategories);
  const [editingMove, setEditingMove] = useState(null);
  const [editingEquipment, setEditingEquipment] = useState(null);

  const tabs = [
    { id: "overview", label: "Overview", Icon: User },
    { id: "stats", label: "Stats", Icon: Gauge },
    { id: "moves", label: "Moves", Icon: Swords },
    { id: "equipment", label: "Equipment", Icon: Package },
    { id: "history", label: "History", Icon: Clock },
  ];

  return (
    <div className="profile-screen">
      <button className="back-btn" onClick={onBack}><ChevronLeft size={16} /> {story.title}</button>

      <div className="profile-hero">
        <div className="portrait-frame">
          {character.portrait ? <img src={character.portrait} alt="" /> : <div className="portrait-fallback"><User size={52} /></div>}
          <div className="portrait-ring" />
        </div>
        <div className="hero-info">
          <span className="hero-story">{story.title}</span>
          {admin ? (
            <input className="hero-name-input" value={character.name}
              onChange={(e) => actions.updateCharacter(character.id, { name: e.target.value })} />
          ) : <h1>{character.name}</h1>}
          {admin ? (
            <input className="hero-subtitle-input" value={character.subtitle || ""} placeholder="Subtitle…"
              onChange={(e) => actions.updateCharacter(character.id, { subtitle: e.target.value })} />
          ) : (character.subtitle && <p className="hero-subtitle">{character.subtitle}</p>)}
          <TagList tags={character.tags || []} onChange={(tags) => actions.updateCharacter(character.id, { tags })} readOnly={!admin} />
        </div>
        {admin && (
          <div className="hero-admin-fields">
            <label className="field-label">Portrait URL</label>
            <ImageUrlField value={character.portrait} onChange={(v) => actions.updateCharacter(character.id, { portrait: v })} ratio="3/4" />
          </div>
        )}
      </div>

      <div className="tab-rail">
        {tabs.map((t) => (
          <button key={t.id} className={"tab-btn" + (tab === t.id ? " tab-btn-active" : "")} onClick={() => setTab(t.id)}>
            <t.Icon size={15} /> {t.label}
          </button>
        ))}
      </div>

      <div className="tab-content" key={tab}>
        {tab === "overview" && (
          <div className="overview-grid">
            <GlowPanel className="notes-panel">
              <h3><ScrollText size={15} /> Notes &amp; Lore</h3>
              {admin ? (
                <textarea className="text-input textarea lore-textarea" value={character.notes || ""}
                  onChange={(e) => actions.updateCharacter(character.id, { notes: e.target.value })}
                  placeholder="Write this character's story…" />
              ) : character.notes ? <p className="lore-text">{character.notes}</p> : <div className="empty-note">No lore recorded yet.</div>}
            </GlowPanel>
            <GlowPanel className="meters-panel">
              <h3><Heart size={15} /> Progress Meters</h3>
              {METER_DEFS.map((md) => (
                <MeterSlider key={md.id} meterDef={md} value={character.meters?.[md.id] ?? 5}
                  primary={md.primary} readOnly={!admin}
                  onChange={(v) => actions.setMeter(character.id, md.id, v)} />
              ))}
            </GlowPanel>
            <GlowPanel className="points-panel">
              <h3><Sparkles size={15} /> Available Stat Points</h3>
              <div className="points-display">
                <AnimatedNumber value={character.statPoints?.available || 0} className="points-number" />
              </div>
              {admin && (
                <div className="increment-row">
                  {ALL_STEPS.map((d) => (
                    <button key={d} className={"chip-btn" + (d < 0 ? " chip-neg" : " chip-pos")}
                      onClick={() => actions.adjustStatPoints(character.id, d)}>{d > 0 ? "+" + d : d}</button>
                  ))}
                </div>
              )}
            </GlowPanel>
          </div>
        )}

        {tab === "stats" && (
          <div className="stats-tab">
            {!admin && (
              <div className="points-reminder">
                <Sparkles size={13} /> {fmt(character.statPoints?.available || 0)} points available to spend
              </div>
            )}
            {config.statCategories.map((cat) => (
              <GlowPanel key={cat.id} className="stat-category-panel">
                <h3>{cat.name}</h3>
                <div className="stat-rows">
                  {cat.stats.map((s) => {
                    const val = character.stats[s.id] || 0;
                    const available = character.statPoints?.available || 0;
                    return (
                      <div key={s.id} className="stat-row">
                        <span className="stat-name">{s.name}</span>
                        <AnimatedNumber value={val} className="stat-value" />
                        {admin ? (
                          <div className="increment-row small">
                            {ALL_STEPS.map((d) => (
                              <button key={d} className={"chip-btn" + (d < 0 ? " chip-neg" : " chip-pos")}
                                onClick={() => actions.adjustStat(character.id, s.id, d, s.name)}>{d > 0 ? "+" + d : d}</button>
                            ))}
                          </div>
                        ) : (
                          <div className="increment-row small">
                            {PLAYER_SPEND_STEPS.map((amt) => (
                              <button key={amt} className="spend-btn" disabled={available < amt}
                                onClick={() => actions.spendPoint(character.id, s.id, amt, s.name)}>
                                +{shortNum(amt)}
                              </button>
                            ))}
                          </div>
                        )}
                      </div>
                    );
                  })}
                  {cat.stats.length === 0 && <div className="empty-note">No stats in this category yet.</div>}
                </div>
              </GlowPanel>
            ))}
            {config.statCategories.length === 0 && <div className="empty-note">No stat categories configured for this story yet.</div>}
          </div>
        )}

        {tab === "moves" && (
          <div className="moves-tab">
            <div className="section-toolbar">
              {admin && <button className="gold-btn" onClick={() => setEditingMove("new")}><Plus size={15} /> New Move</button>}
            </div>
            <div className="move-grid">
              {(character.moves || []).map((mv) => (
                <MoveCard key={mv.id} move={mv}
                  category={config.moveCategories.find((c) => c.id === mv.categoryId)}
                  statOptions={statFlat} admin={admin} character={character}
                  onUnlock={(id) => actions.unlockMove(character.id, id)}
                  onEdit={(m) => setEditingMove(m)}
                  onDelete={(id) => actions.deleteMove(character.id, id)} />
              ))}
              {(character.moves || []).length === 0 && <div className="empty-note">No moves yet.</div>}
            </div>
          </div>
        )}

        {tab === "equipment" && (
          <div className="equipment-tab">
            <div className="section-toolbar">
              {admin && <button className="gold-btn" onClick={() => setEditingEquipment("new")}><Plus size={15} /> New Equipment</button>}
            </div>
            <div className="equipment-grid">
              {(character.equipment || []).map((eq) => (
                <EquipmentCard key={eq.id} eq={eq} admin={admin}
                  onEdit={(e) => setEditingEquipment(e)}
                  onDelete={(id) => actions.deleteEquipment(character.id, id)} />
              ))}
              {(character.equipment || []).length === 0 && <div className="empty-note">No equipment yet.</div>}
            </div>
          </div>
        )}

        {tab === "history" && (
          <GlowPanel>
            <HistoryList entries={character.history || []} />
          </GlowPanel>
        )}
      </div>

      {editingMove && (
        <MoveEditorModal
          initial={editingMove === "new" ? null : editingMove}
          moveCategories={config.moveCategories}
          statOptions={statFlat}
          onSave={(m) => {
            if (editingMove === "new") actions.addMove(character.id, m); else actions.updateMove(character.id, m.id, m);
            setEditingMove(null);
          }}
          onClose={() => setEditingMove(null)}
        />
      )}
      {editingEquipment && (
        <EquipmentEditorModal
          initial={editingEquipment === "new" ? null : editingEquipment}
          onSave={(eq) => {
            if (editingEquipment === "new") actions.addEquipment(character.id, eq); else actions.updateEquipment(character.id, eq.id, eq);
            setEditingEquipment(null);
          }}
          onClose={() => setEditingEquipment(null)}
        />
      )}
    </div>
  );
}

function Header({ admin, onSwitchPlayer, onRequestAdmin, onOpenPasswordSettings, story, character, onHome, onStory }) {
  return (
    <header className="app-header">
      <button className="brand" onClick={onHome}><Sparkles size={16} /> CODEX</button>
      <div className="breadcrumb">
        <button onClick={onHome}>Home</button>
        {story && <><ChevronRight size={13} /><button onClick={onStory}>{story.title}</button></>}
        {character && <><ChevronRight size={13} /><span>{character.name}</span></>}
      </div>
      <div className="mode-toggle">
        <button className={"mode-btn" + (!admin ? " active" : "")} onClick={onSwitchPlayer}><User size={14} /> Player</button>
        <button className={"mode-btn" + (admin ? " active" : "")} onClick={onRequestAdmin}><ShieldCheck size={14} /> Admin</button>
      </div>
      {admin && (
        <button className="icon-btn" title="Change admin password" onClick={onOpenPasswordSettings}><Key size={14} /></button>
      )}
    </header>
  );
}

/* ============================== app root ============================== */

export default function App() {
  const [world, setWorld] = useState(null);
  const [characters, setCharacters] = useState(null);
  const [ready, setReady] = useState(false);
  const [admin, setAdmin] = useState(false);
  const [adminUnlocked, setAdminUnlocked] = useState(false);
  const [unlockedCharIds, setUnlockedCharIds] = useState(() => new Set());
  const [authRequest, setAuthRequest] = useState(null);
  const [changePasswordOpen, setChangePasswordOpen] = useState(false);
  const [view, setView] = useState("home");
  const [storyId, setStoryId] = useState(null);
  const [charId, setCharId] = useState(null);
  const [saveState, setSaveState] = useState("idle");

  const worldTimer = useRef(null);
  const charTimer = useRef(null);
  const loadedRef = useRef(false);

  useEffect(() => {
    let mounted = true;
    (async () => {
      let w = { stories: [], storyConfigs: {}, adminPassword: null };
      let c = {};
      try {
        const r = await window.storage.get("world", true);
        if (r && r.value) w = { ...w, ...JSON.parse(r.value) };
      } catch (e) { /* no data yet */ }
      try {
        const r = await window.storage.get("characters", true);
        if (r && r.value) c = JSON.parse(r.value);
      } catch (e) { /* no data yet */ }
      if (!mounted) return;
      setWorld(w);
      setCharacters(c);
      setReady(true);
      loadedRef.current = true;
    })();
    return () => { mounted = false; };
  }, []);

  useEffect(() => {
    if (!loadedRef.current || !world) return;
    setSaveState("saving");
    clearTimeout(worldTimer.current);
    worldTimer.current = setTimeout(async () => {
      try { await window.storage.set("world", JSON.stringify(world), true); setSaveState("saved"); }
      catch (e) { setSaveState("error"); }
    }, 500);
    return () => clearTimeout(worldTimer.current);
  }, [world]);

  useEffect(() => {
    if (!loadedRef.current || !characters) return;
    setSaveState("saving");
    clearTimeout(charTimer.current);
    charTimer.current = setTimeout(async () => {
      try { await window.storage.set("characters", JSON.stringify(characters), true); setSaveState("saved"); }
      catch (e) { setSaveState("error"); }
    }, 500);
    return () => clearTimeout(charTimer.current);
  }, [characters]);

  const requestAdmin = () => {
    if (adminUnlocked) { setAdmin(true); return; }
    setAuthRequest({ mode: world.adminPassword ? "admin-enter" : "admin-create" });
  };

  const attemptOpenCharacter = (id) => {
    const ch = characters[id];
    if (!ch) return;
    if (admin || !ch.password || unlockedCharIds.has(id)) {
      setCharId(id); setView("profile");
    } else {
      setAuthRequest({ mode: "character-enter", charId: id });
    }
  };

  const storySettingsActionsFor = (sid) => ({
    renameStory: (title) => setWorld((prev) => ({ ...prev, stories: prev.stories.map((s) => (s.id === sid ? { ...s, title } : s)) })),
    updateSubtitle: (subtitle) => setWorld((prev) => ({ ...prev, stories: prev.stories.map((s) => (s.id === sid ? { ...s, subtitle } : s)) })),
    updateCover: (coverImage) => setWorld((prev) => ({ ...prev, stories: prev.stories.map((s) => (s.id === sid ? { ...s, coverImage } : s)) })),
    renameCategory: (catId, name) => setWorld((prev) => updateConfig(prev, sid, (cfg) => ({ ...cfg, statCategories: cfg.statCategories.map((c) => (c.id === catId ? { ...c, name } : c)) }))),
    addCategory: (name) => setWorld((prev) => updateConfig(prev, sid, (cfg) => ({ ...cfg, statCategories: [...cfg.statCategories, { id: uid(), name, stats: [] }] }))),
    deleteCategory: (catId) => setWorld((prev) => updateConfig(prev, sid, (cfg) => ({ ...cfg, statCategories: cfg.statCategories.filter((c) => c.id !== catId) }))),
    renameStat: (catId, statId, name) => setWorld((prev) => updateConfig(prev, sid, (cfg) => ({ ...cfg, statCategories: cfg.statCategories.map((c) => (c.id === catId ? { ...c, stats: c.stats.map((s) => (s.id === statId ? { ...s, name } : s)) } : c)) }))),
    addStat: (catId, name) => setWorld((prev) => updateConfig(prev, sid, (cfg) => ({ ...cfg, statCategories: cfg.statCategories.map((c) => (c.id === catId ? { ...c, stats: [...c.stats, { id: uid(), name }] } : c)) }))),
    deleteStat: (catId, statId) => setWorld((prev) => updateConfig(prev, sid, (cfg) => ({ ...cfg, statCategories: cfg.statCategories.map((c) => (c.id === catId ? { ...c, stats: c.stats.filter((s) => s.id !== statId) } : c)) }))),
    renameMoveCategory: (mcId, name) => setWorld((prev) => updateConfig(prev, sid, (cfg) => ({ ...cfg, moveCategories: cfg.moveCategories.map((m) => (m.id === mcId ? { ...m, name } : m)) }))),
    addMoveCategory: (name) => setWorld((prev) => updateConfig(prev, sid, (cfg) => ({ ...cfg, moveCategories: [...cfg.moveCategories, { id: uid(), name }] }))),
    deleteMoveCategory: (mcId) => setWorld((prev) => updateConfig(prev, sid, (cfg) => ({ ...cfg, moveCategories: cfg.moveCategories.filter((m) => m.id !== mcId) }))),
  });

  const actions = useMemo(() => ({
    addStory: (data) => {
      const id = uid();
      setWorld((prev) => ({
        ...prev,
        stories: [...prev.stories, { id, title: data.title, subtitle: data.subtitle, coverImage: data.coverImage, createdAt: Date.now() }],
        storyConfigs: { ...prev.storyConfigs, [id]: { statCategories: defaultStatCategories(), moveCategories: defaultMoveCategories() } },
      }));
    },
    updateStoryMeta: (id, data) => {
      setWorld((prev) => ({ ...prev, stories: prev.stories.map((s) => (s.id === id ? { ...s, ...data } : s)) }));
    },
    deleteStory: (id) => {
      setWorld((prev) => {
        const restConfigs = { ...prev.storyConfigs };
        delete restConfigs[id];
        return { ...prev, stories: prev.stories.filter((s) => s.id !== id), storyConfigs: restConfigs };
      });
      setCharacters((prev) => {
        const next = { ...prev };
        Object.keys(next).forEach((cid) => { if (next[cid].storyId === id) delete next[cid]; });
        return next;
      });
      setView("home"); setStoryId(null); setCharId(null);
    },
    addCharacter: (sid, data) => {
      const id = uid();
      setCharacters((prev) => ({
        ...prev,
        [id]: {
          id, storyId: sid, name: data.name, subtitle: data.subtitle || "", portrait: data.portrait || "",
          password: data.password || "", tags: [],
          notes: "", stats: {}, statPoints: { available: 0 }, meters: defaultMeters(), moves: [], equipment: [],
          history: [{ id: uid(), text: data.name + " entered the chronicle", timestamp: Date.now() }],
          createdAt: Date.now(),
        },
      }));
    },
    updateCharacter: (id, patch) => {
      setCharacters((prev) => ({ ...prev, [id]: { ...prev[id], ...patch } }));
    },
    deleteCharacter: (id) => {
      setCharacters((prev) => { const next = { ...prev }; delete next[id]; return next; });
      setView("roster"); setCharId(null);
    },
    adjustStat: (cid, statId, delta, statName) => {
      setCharacters((prev) => {
        const ch = prev[cid]; if (!ch) return prev;
        const cur = ch.stats[statId] || 0;
        const next = clamp(cur + delta, 0, 999999999);
        const entry = { id: uid(), text: (delta > 0 ? "+" : "") + delta + " " + (statName || "Stat"), timestamp: Date.now() };
        return { ...prev, [cid]: { ...ch, stats: { ...ch.stats, [statId]: next }, history: [...(ch.history || []), entry] } };
      });
    },
    spendPoint: (cid, statId, amount, statName) => {
      setCharacters((prev) => {
        const ch = prev[cid]; if (!ch) return prev;
        const avail = ch.statPoints?.available || 0;
        const spend = Math.min(amount, avail);
        if (spend <= 0) return prev;
        const cur = ch.stats[statId] || 0;
        const entry = { id: uid(), text: "+" + fmt(spend) + " " + (statName || "Stat") + " (spent points)", timestamp: Date.now() };
        return { ...prev, [cid]: { ...ch, stats: { ...ch.stats, [statId]: cur + spend }, statPoints: { ...ch.statPoints, available: avail - spend }, history: [...(ch.history || []), entry] } };
      });
    },
    adjustStatPoints: (cid, delta) => {
      setCharacters((prev) => {
        const ch = prev[cid]; if (!ch) return prev;
        const avail = clamp((ch.statPoints?.available || 0) + delta, 0, 999999999);
        const entry = { id: uid(), text: (delta > 0 ? "Granted " : "Removed ") + fmt(Math.abs(delta)) + " stat point" + (Math.abs(delta) === 1 ? "" : "s"), timestamp: Date.now() };
        return { ...prev, [cid]: { ...ch, statPoints: { ...ch.statPoints, available: avail }, history: [...(ch.history || []), entry] } };
      });
    },
    setMeter: (cid, meterId, value) => {
      setCharacters((prev) => {
        const ch = prev[cid]; if (!ch) return prev;
        const old = ch.meters?.[meterId] ?? 5;
        if (old === value) return prev;
        const meterDef = METER_DEFS.find((m) => m.id === meterId);
        const up = value > old;
        let text;
        if (meterId === "humanity") text = up ? "Gained Humanity" : "Lost Humanity";
        else text = (up ? "Increased " : "Decreased ") + meterDef.name;
        const entry = { id: uid(), text, timestamp: Date.now() };
        return { ...prev, [cid]: { ...ch, meters: { ...ch.meters, [meterId]: value }, history: [...(ch.history || []), entry] } };
      });
    },
    unlockMove: (cid, moveId) => {
      setCharacters((prev) => {
        const ch = prev[cid]; if (!ch) return prev;
        let name = "";
        const moves = ch.moves.map((m) => { if (m.id === moveId) { name = m.name; return { ...m, unlocked: true }; } return m; });
        const entry = { id: uid(), text: "Unlocked " + name, timestamp: Date.now() };
        return { ...prev, [cid]: { ...ch, moves, history: [...(ch.history || []), entry] } };
      });
    },
    addMove: (cid, move) => {
      setCharacters((prev) => {
        const ch = prev[cid]; if (!ch) return prev;
        const entry = { id: uid(), text: "Added move: " + move.name, timestamp: Date.now() };
        return { ...prev, [cid]: { ...ch, moves: [...(ch.moves || []), move], history: [...(ch.history || []), entry] } };
      });
    },
    updateMove: (cid, moveId, patch) => {
      setCharacters((prev) => {
        const ch = prev[cid]; if (!ch) return prev;
        return { ...prev, [cid]: { ...ch, moves: ch.moves.map((m) => (m.id === moveId ? { ...m, ...patch } : m)) } };
      });
    },
    deleteMove: (cid, moveId) => {
      setCharacters((prev) => {
        const ch = prev[cid]; if (!ch) return prev;
        return { ...prev, [cid]: { ...ch, moves: ch.moves.filter((m) => m.id !== moveId) } };
      });
    },
    addEquipment: (cid, eq) => {
      setCharacters((prev) => {
        const ch = prev[cid]; if (!ch) return prev;
        const entry = { id: uid(), text: "Added equipment: " + eq.name, timestamp: Date.now() };
        return { ...prev, [cid]: { ...ch, equipment: [...(ch.equipment || []), eq], history: [...(ch.history || []), entry] } };
      });
    },
    updateEquipment: (cid, eqId, patch) => {
      setCharacters((prev) => {
        const ch = prev[cid]; if (!ch) return prev;
        return { ...prev, [cid]: { ...ch, equipment: ch.equipment.map((e) => (e.id === eqId ? { ...e, ...patch } : e)) } };
      });
    },
    deleteEquipment: (cid, eqId) => {
      setCharacters((prev) => {
        const ch = prev[cid]; if (!ch) return prev;
        return { ...prev, [cid]: { ...ch, equipment: ch.equipment.filter((e) => e.id !== eqId) } };
      });
    },
  }), []);

  if (!ready) {
    return (
      <div className="app-root">
        <style>{CSS}</style>
        <CosmicBackground />
        <div className="loading-screen">
          <div className="loading-sigil" />
          <p>Opening the codex…</p>
        </div>
      </div>
    );
  }

  const currentStory = storyId ? world.stories.find((s) => s.id === storyId) : null;
  const currentConfig = storyId ? world.storyConfigs[storyId] : null;
  const currentCharacter = charId ? characters[charId] : null;
  const storyCharacters = storyId ? Object.values(characters).filter((c) => c.storyId === storyId) : [];

  return (
    <div className="app-root">
      <style>{CSS}</style>
      <CosmicBackground />
      <Header admin={admin} onSwitchPlayer={() => setAdmin(false)} onRequestAdmin={requestAdmin}
        onOpenPasswordSettings={() => setChangePasswordOpen(true)}
        story={currentStory} character={currentCharacter}
        onHome={() => { setView("home"); setStoryId(null); setCharId(null); }}
        onStory={() => { setView("roster"); setCharId(null); }} />
      <main className="app-main">
        <div className="view-transition" key={view + "-" + (storyId || "") + "-" + (charId || "")}>
          {view === "home" && (
            <HomeScreen stories={world.stories} characters={characters} admin={admin} actions={actions}
              onOpenStory={(id) => { setStoryId(id); setView("roster"); }} />
          )}
          {view === "roster" && currentStory && (
            <RosterScreen story={currentStory} config={currentConfig} characters={storyCharacters} admin={admin}
              actions={actions} storySettingsActionsFor={storySettingsActionsFor}
              onOpenCharacter={attemptOpenCharacter}
              onBack={() => { setView("home"); setStoryId(null); }} />
          )}
          {view === "profile" && currentCharacter && currentStory && (
            <CharacterProfileScreen character={currentCharacter} story={currentStory} config={currentConfig}
              admin={admin} actions={actions}
              onBack={() => { setView("roster"); setCharId(null); }} />
          )}
        </div>
      </main>
      <div className={"save-indicator save-" + saveState}>
        {saveState === "saving" && <>Saving…</>}
        {saveState === "saved" && <>Saved</>}
        {saveState === "error" && <>Save failed — check connection</>}
      </div>

      {authRequest && (
        <PasswordGateModal
          mode={authRequest.mode}
          label={authRequest.charId ? characters[authRequest.charId]?.name : undefined}
          onValidate={(pw) => {
            if (authRequest.mode === "admin-enter") return pw === world.adminPassword;
            if (authRequest.mode === "character-enter") return pw === (characters[authRequest.charId]?.password || "");
            return true;
          }}
          onSuccess={(pw) => {
            if (authRequest.mode === "admin-create") {
              setWorld((prev) => ({ ...prev, adminPassword: pw }));
              setAdminUnlocked(true); setAdmin(true);
            } else if (authRequest.mode === "admin-enter") {
              setAdminUnlocked(true); setAdmin(true);
            } else if (authRequest.mode === "character-enter") {
              setUnlockedCharIds((prev) => new Set(prev).add(authRequest.charId));
              setCharId(authRequest.charId); setView("profile");
            }
            setAuthRequest(null);
          }}
          onClose={() => setAuthRequest(null)}
        />
      )}

      {changePasswordOpen && (
        <ChangeAdminPasswordModal
          currentPassword={world.adminPassword}
          onSave={(newPw) => { setWorld((prev) => ({ ...prev, adminPassword: newPw })); setChangePasswordOpen(false); }}
          onClose={() => setChangePasswordOpen(false)}
        />
      )}
    </div>
  );
}
