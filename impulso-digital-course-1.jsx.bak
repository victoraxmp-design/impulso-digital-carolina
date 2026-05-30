import { useState, useEffect, useRef } from "react";

// ─────────────────────────────────────────────
// STYLES
// ─────────────────────────────────────────────
const STYLES = `
@import url('https://fonts.googleapis.com/css2?family=Sora:wght@300;400;600;700;800&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,600;1,9..40,400&display=swap');

*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#06091A;--sidebar:#0C1228;--card:#111827;--card2:#1A2540;
  --gold:#F59E0B;--gold-l:#FCD34D;--teal:#0D9488;--purple:#7C3AED;
  --coral:#F97316;--green:#10B981;
  --txt:#F0F4FF;--txt2:#94A3B8;--txt3:#475569;
  --border:rgba(255,255,255,0.07);--border2:rgba(255,255,255,0.13);
  --radius:14px;--radius-lg:20px;
  --gold-glow:0 0 30px rgba(245,158,11,0.25);
}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--txt);overflow-x:hidden}
h1,h2,h3,h4,h5{font-family:'Sora',sans-serif}

/* ── Scrollbar ── */
::-webkit-scrollbar{width:5px;height:5px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--border2);border-radius:99px}

/* ── Layout ── */
.app{display:flex;min-height:100vh}

/* ── Sidebar ── */
.sidebar{
  width:270px;min-height:100vh;background:var(--sidebar);
  border-right:1px solid var(--border);display:flex;flex-direction:column;
  position:fixed;left:0;top:0;bottom:0;z-index:50;
  transition:transform .35s cubic-bezier(.4,0,.2,1);
  overflow-y:auto;
}
.sidebar.closed{transform:translateX(-100%)}
.sidebar-logo{
  padding:28px 24px 20px;display:flex;align-items:center;gap:12px;
  border-bottom:1px solid var(--border);
}
.logo-badge{
  width:38px;height:38px;border-radius:10px;
  background:linear-gradient(135deg,var(--gold),var(--coral));
  display:flex;align-items:center;justify-content:center;
  font-size:18px;flex-shrink:0;box-shadow:var(--gold-glow);
}
.logo-text{font-family:'Sora',sans-serif;font-size:13px;font-weight:700;color:var(--txt);line-height:1.2}
.logo-sub{font-size:10px;color:var(--txt2);font-weight:400}

.sidebar-progress{padding:18px 24px;border-bottom:1px solid var(--border)}
.prog-label{font-size:11px;color:var(--txt2);margin-bottom:8px;display:flex;justify-content:space-between}
.prog-bar{height:4px;background:var(--border2);border-radius:99px;overflow:hidden}
.prog-fill{height:100%;border-radius:99px;background:linear-gradient(90deg,var(--gold),var(--coral));transition:width .6s cubic-bezier(.4,0,.2,1)}

.sidebar-nav{padding:12px 12px;flex:1}
.nav-section-label{font-size:10px;font-weight:600;color:var(--txt3);letter-spacing:.08em;text-transform:uppercase;padding:8px 12px 6px}

.module-btn{
  width:100%;text-align:left;padding:10px 12px;border-radius:10px;
  border:none;background:transparent;cursor:pointer;
  display:flex;align-items:center;gap:10px;
  transition:all .2s ease;margin-bottom:2px;color:var(--txt2);
}
.module-btn:hover{background:rgba(255,255,255,0.05);color:var(--txt)}
.module-btn.active{background:rgba(245,158,11,0.12);color:var(--gold)}
.module-btn.done{color:var(--green)}
.module-icon{
  width:32px;height:32px;border-radius:8px;display:flex;align-items:center;
  justify-content:center;font-size:14px;flex-shrink:0;
  background:rgba(255,255,255,0.05);transition:all .2s;
}
.module-btn.active .module-icon{background:rgba(245,158,11,0.2)}
.module-btn.done .module-icon{background:rgba(16,185,129,0.15)}
.module-info{flex:1;min-width:0}
.module-num{font-size:10px;opacity:.6;margin-bottom:1px}
.module-name{font-size:12.5px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;font-family:'Sora',sans-serif}
.module-check{font-size:12px;flex-shrink:0}

/* ── Main ── */
.main{margin-left:270px;flex:1;min-height:100vh;display:flex;flex-direction:column}
.topbar{
  position:sticky;top:0;z-index:40;
  background:rgba(6,9,26,0.85);backdrop-filter:blur(20px);
  border-bottom:1px solid var(--border);
  padding:0 32px;height:60px;display:flex;align-items:center;justify-content:space-between;
}
.menu-btn{
  background:none;border:1px solid var(--border2);color:var(--txt2);
  padding:6px 10px;border-radius:8px;cursor:pointer;font-size:16px;
  transition:all .2s;display:none;
}
.menu-btn:hover{border-color:var(--gold);color:var(--gold)}
.breadcrumb{font-size:13px;color:var(--txt2);display:flex;align-items:center;gap:8px}
.breadcrumb span{color:var(--txt3)}
.topbar-right{display:flex;align-items:center;gap:12px}
.badge-count{
  background:rgba(245,158,11,.15);color:var(--gold);
  font-size:11px;font-weight:600;padding:3px 10px;border-radius:99px;
  border:1px solid rgba(245,158,11,.25);
}

/* ── Content area ── */
.content{flex:1;padding:40px 40px 80px;max-width:900px}

/* ── Fade animation ── */
.fade-in{animation:fadeUp .45s cubic-bezier(.4,0,.2,1) both}
@keyframes fadeUp{from{opacity:0;transform:translateY(18px)}to{opacity:1;transform:translateY(0)}}
.fade-in-delay-1{animation-delay:.05s}
.fade-in-delay-2{animation-delay:.1s}
.fade-in-delay-3{animation-delay:.15s}
.fade-in-delay-4{animation-delay:.2s}
.fade-in-delay-5{animation-delay:.25s}

/* ── Home ── */
.home-hero{
  padding:48px 0 40px;animation:fadeUp .5s ease both;
}
.hero-eyebrow{
  display:inline-flex;align-items:center;gap:8px;
  background:rgba(245,158,11,.1);border:1px solid rgba(245,158,11,.2);
  border-radius:99px;padding:5px 14px;font-size:12px;color:var(--gold);
  font-weight:600;margin-bottom:20px;letter-spacing:.03em;
}
.hero-dot{width:6px;height:6px;border-radius:50%;background:var(--gold);animation:pulse 2s infinite}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.5;transform:scale(.8)}}
.hero-title{
  font-size:42px;font-weight:800;line-height:1.15;color:var(--txt);
  margin-bottom:16px;
}
.hero-title span{
  background:linear-gradient(135deg,var(--gold),var(--coral));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
}
.hero-desc{font-size:17px;color:var(--txt2);line-height:1.7;max-width:600px;margin-bottom:32px}
.hero-stats{display:flex;gap:24px;flex-wrap:wrap;margin-bottom:40px}
.stat-card{
  background:var(--card);border:1px solid var(--border);border-radius:12px;
  padding:16px 20px;text-align:center;min-width:100px;
}
.stat-val{font-family:'Sora',sans-serif;font-size:24px;font-weight:700;color:var(--gold)}
.stat-lbl{font-size:11px;color:var(--txt2);margin-top:2px}

.modules-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:16px}
.mod-card{
  background:var(--card);border:1px solid var(--border);border-radius:var(--radius-lg);
  padding:24px;cursor:pointer;transition:all .3s cubic-bezier(.4,0,.2,1);
  position:relative;overflow:hidden;
}
.mod-card::before{
  content:'';position:absolute;inset:0;
  background:linear-gradient(135deg,transparent 60%,rgba(245,158,11,.04));
  opacity:0;transition:opacity .3s;
}
.mod-card:hover{border-color:var(--border2);transform:translateY(-3px);box-shadow:0 16px 40px rgba(0,0,0,.35)}
.mod-card:hover::before{opacity:1}
.mod-card-top{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:16px}
.mod-card-icon{
  width:46px;height:46px;border-radius:12px;display:flex;align-items:center;
  justify-content:center;font-size:22px;background:rgba(255,255,255,.05);
}
.mod-card-num{font-family:'Sora',sans-serif;font-size:11px;font-weight:700;color:var(--txt3);letter-spacing:.05em}
.mod-card-title{font-family:'Sora',sans-serif;font-size:15px;font-weight:700;margin-bottom:6px;line-height:1.3}
.mod-card-sub{font-size:12.5px;color:var(--txt2);line-height:1.5;margin-bottom:16px}
.mod-card-footer{display:flex;align-items:center;justify-content:space-between}
.mod-card-meta{font-size:11px;color:var(--txt3);display:flex;align-items:center;gap:6px}
.mod-card-arrow{font-size:16px;color:var(--txt3);transition:all .3s}
.mod-card:hover .mod-card-arrow{color:var(--gold);transform:translateX(3px)}
.mod-progress-mini{height:3px;background:var(--border2);border-radius:99px;overflow:hidden;margin-top:12px}
.mod-progress-mini-fill{height:100%;border-radius:99px;transition:width .5s ease}

/* ── Module view ── */
.module-header{
  margin-bottom:32px;padding-bottom:28px;border-bottom:1px solid var(--border);
}
.module-header-top{display:flex;align-items:center;gap:16px;margin-bottom:16px}
.module-big-icon{
  width:58px;height:58px;border-radius:16px;display:flex;align-items:center;
  justify-content:center;font-size:28px;background:rgba(245,158,11,.1);
  border:1px solid rgba(245,158,11,.2);
}
.module-eyebrow{font-size:11px;font-weight:700;color:var(--gold);text-transform:uppercase;letter-spacing:.08em;margin-bottom:6px}
.module-title{font-size:26px;font-weight:800;margin-bottom:8px}
.module-subtitle{font-size:15px;color:var(--txt2);line-height:1.6}
.lesson-list{display:flex;flex-direction:column;gap:10px}
.lesson-item{
  background:var(--card);border:1px solid var(--border);border-radius:var(--radius);
  padding:18px 20px;cursor:pointer;display:flex;align-items:center;gap:14px;
  transition:all .25s cubic-bezier(.4,0,.2,1);
}
.lesson-item:hover{border-color:var(--border2);background:var(--card2);transform:translateX(4px)}
.lesson-item.active-lesson{border-color:rgba(245,158,11,.4);background:rgba(245,158,11,.06)}
.lesson-item.completed-lesson .lesson-num{background:rgba(16,185,129,.2);color:var(--green)}
.lesson-num{
  width:36px;height:36px;border-radius:9px;background:rgba(255,255,255,.06);
  display:flex;align-items:center;justify-content:center;
  font-family:'Sora',sans-serif;font-size:12px;font-weight:700;color:var(--txt2);flex-shrink:0;
}
.lesson-info{flex:1}
.lesson-title{font-size:14px;font-weight:600;font-family:'Sora',sans-serif;margin-bottom:3px}
.lesson-meta{font-size:12px;color:var(--txt3);display:flex;gap:12px}
.lesson-arrow{color:var(--txt3);font-size:16px;transition:all .25s}
.lesson-item:hover .lesson-arrow{color:var(--gold);transform:translateX(2px)}

/* ── Lesson view ── */
.lesson-header{margin-bottom:32px}
.lesson-back-btn{
  background:none;border:1px solid var(--border);color:var(--txt2);
  padding:7px 14px;border-radius:8px;cursor:pointer;font-size:13px;
  display:inline-flex;align-items:center;gap:6px;
  transition:all .2s;margin-bottom:20px;font-family:'DM Sans',sans-serif;
}
.lesson-back-btn:hover{border-color:var(--gold);color:var(--gold)}
.lesson-tag{
  display:inline-flex;align-items:center;gap:6px;font-size:11px;font-weight:700;
  padding:4px 12px;border-radius:99px;margin-bottom:12px;
  background:rgba(245,158,11,.1);color:var(--gold);border:1px solid rgba(245,158,11,.2);
  text-transform:uppercase;letter-spacing:.06em;
}
.lesson-h1{font-size:28px;font-weight:800;line-height:1.25;margin-bottom:10px}
.lesson-desc{font-size:16px;color:var(--txt2);line-height:1.65;margin-bottom:20px}
.lesson-duration{
  display:inline-flex;align-items:center;gap:6px;font-size:12px;color:var(--txt3);
  background:var(--card);border:1px solid var(--border);padding:5px 12px;border-radius:99px;
}

/* ── Content blocks ── */
.content-body{display:flex;flex-direction:column;gap:0}
.cb-section{margin-bottom:28px}
.cb-h2{font-size:19px;font-weight:700;color:var(--txt);margin-bottom:14px;display:flex;align-items:center;gap:8px}
.cb-h2::before{content:'';width:3px;height:20px;background:var(--gold);border-radius:2px;flex-shrink:0}
.cb-h3{font-size:15px;font-weight:600;color:var(--txt);margin-bottom:10px}
.cb-p{font-size:15px;color:var(--txt2);line-height:1.75;margin-bottom:12px}
.cb-list{list-style:none;display:flex;flex-direction:column;gap:7px;margin-bottom:14px}
.cb-list li{
  font-size:14.5px;color:var(--txt2);line-height:1.6;padding-left:20px;position:relative;
}
.cb-list li::before{content:'›';position:absolute;left:0;color:var(--gold);font-weight:700}

.cb-table{width:100%;border-collapse:separate;border-spacing:0;border-radius:12px;overflow:hidden;border:1px solid var(--border);margin-bottom:14px}
.cb-table th{background:rgba(245,158,11,.1);color:var(--gold);font-size:11.5px;font-weight:700;text-transform:uppercase;letter-spacing:.05em;padding:11px 14px;text-align:left;border-bottom:1px solid var(--border)}
.cb-table td{padding:10px 14px;font-size:13.5px;color:var(--txt2);border-bottom:1px solid var(--border)}
.cb-table tr:last-child td{border-bottom:none}
.cb-table tr:nth-child(even) td{background:rgba(255,255,255,.015)}

.cb-callout{
  border-radius:12px;padding:16px 18px;margin-bottom:14px;
  display:flex;gap:12px;align-items:flex-start;
}
.cb-callout.tip{background:rgba(13,148,136,.1);border:1px solid rgba(13,148,136,.25)}
.cb-callout.warning{background:rgba(249,115,22,.1);border:1px solid rgba(249,115,22,.25)}
.cb-callout.important{background:rgba(245,158,11,.1);border:1px solid rgba(245,158,11,.25)}
.cb-callout.info{background:rgba(124,58,237,.1);border:1px solid rgba(124,58,237,.25)}
.cb-callout-icon{font-size:18px;flex-shrink:0;margin-top:1px}
.cb-callout-text{font-size:14px;line-height:1.65;color:var(--txt2)}
.cb-callout.tip .cb-callout-text{color:rgba(94,234,212,.9)}
.cb-callout.warning .cb-callout-text{color:rgba(253,186,116,.9)}
.cb-callout.important .cb-callout-text{color:rgba(253,211,77,.9)}
.cb-callout.info .cb-callout-text{color:rgba(196,181,253,.9)}

.cb-code{
  background:#0D1225;border:1px solid var(--border2);border-radius:12px;
  padding:18px 20px;font-family:'DM Mono',monospace;font-size:13px;
  color:#A5F3FC;line-height:1.7;overflow-x:auto;white-space:pre-wrap;
  word-break:break-word;margin-bottom:14px;
}

.cb-exercise{
  background:rgba(16,185,129,.08);border:1px solid rgba(16,185,129,.2);
  border-radius:12px;padding:18px 20px;margin-bottom:14px;
}
.cb-exercise-label{
  font-size:11px;font-weight:700;color:var(--green);text-transform:uppercase;
  letter-spacing:.06em;margin-bottom:8px;display:flex;align-items:center;gap:6px;
}
.cb-exercise-text{font-size:14px;color:rgba(167,243,208,.85);line-height:1.65}

.cb-checklist{display:flex;flex-direction:column;gap:8px;margin-bottom:14px}
.cb-check-item{
  display:flex;align-items:flex-start;gap:10px;font-size:14px;color:var(--txt2);
  padding:10px 14px;background:var(--card);border:1px solid var(--border);
  border-radius:9px;cursor:pointer;transition:all .2s;line-height:1.55;
}
.cb-check-item:hover{border-color:var(--border2);background:var(--card2)}
.cb-check-item.checked{border-color:rgba(16,185,129,.3);background:rgba(16,185,129,.06);color:rgba(167,243,208,.8)}
.cb-check-box{
  width:20px;height:20px;border-radius:5px;border:2px solid var(--txt3);
  display:flex;align-items:center;justify-content:center;flex-shrink:0;
  transition:all .2s;margin-top:1px;
}
.cb-check-item.checked .cb-check-box{background:var(--green);border-color:var(--green);color:#fff;font-size:11px}

.cb-prompt{
  background:#0A0E1F;border:1px solid rgba(124,58,237,.3);border-radius:12px;
  padding:18px 20px;margin-bottom:14px;position:relative;overflow:hidden;
}
.cb-prompt::before{
  content:'PROMPT';position:absolute;top:12px;right:14px;
  font-size:9px;font-weight:700;color:rgba(196,181,253,.6);letter-spacing:.1em;
}
.cb-prompt-text{
  font-family:'DM Mono',monospace;font-size:13px;color:rgba(196,181,253,.9);
  line-height:1.7;white-space:pre-wrap;word-break:break-word;
}

.cb-flow{
  background:var(--card);border:1px solid var(--border);border-radius:12px;
  padding:20px;margin-bottom:14px;font-family:'DM Mono',monospace;
  font-size:12.5px;color:var(--txt2);line-height:1.8;white-space:pre-wrap;
  overflow-x:auto;
}

.cb-divider{height:1px;background:var(--border);margin:20px 0}

/* ── Level cards (Escalera) ── */
.level-card{
  border-radius:var(--radius-lg);padding:24px;margin-bottom:16px;
  border:1px solid var(--border);background:var(--card);
  transition:all .3s;cursor:default;
}
.level-card:hover{border-color:var(--border2);transform:translateY(-2px)}
.level-header{display:flex;align-items:center;gap:14px;margin-bottom:16px}
.level-badge{
  width:48px;height:48px;border-radius:12px;display:flex;align-items:center;
  justify-content:center;font-family:'Sora',sans-serif;font-size:18px;font-weight:800;
}
.level-title{font-family:'Sora',sans-serif;font-size:17px;font-weight:700}
.level-subtitle{font-size:13px;color:var(--txt2);margin-top:2px}

/* ── Quiz (Prueba) ── */
.quiz-card{
  background:var(--card);border:1px solid var(--border);border-radius:var(--radius-lg);
  padding:24px;margin-bottom:16px;
}
.quiz-num{
  font-size:11px;font-weight:700;color:var(--gold);text-transform:uppercase;
  letter-spacing:.06em;margin-bottom:10px;
}
.quiz-q{font-size:16px;font-weight:600;font-family:'Sora',sans-serif;margin-bottom:16px;line-height:1.45}
.quiz-reveal-btn{
  background:rgba(245,158,11,.12);border:1px solid rgba(245,158,11,.25);
  color:var(--gold);padding:8px 18px;border-radius:8px;cursor:pointer;
  font-size:13px;font-weight:600;font-family:'DM Sans',sans-serif;
  transition:all .2s;
}
.quiz-reveal-btn:hover{background:rgba(245,158,11,.2)}
.quiz-answer{
  margin-top:16px;padding-top:16px;border-top:1px solid var(--border);
  animation:fadeUp .35s ease both;
}

/* ── Resource cards ── */
.resource-card{
  background:var(--card);border:1px solid var(--border);border-radius:var(--radius-lg);
  padding:24px;margin-bottom:16px;transition:all .3s;
}
.resource-card:hover{border-color:var(--border2);transform:translateY(-2px)}
.resource-num{
  width:36px;height:36px;border-radius:9px;
  background:linear-gradient(135deg,var(--gold),var(--coral));
  display:flex;align-items:center;justify-content:center;
  font-family:'Sora',sans-serif;font-size:14px;font-weight:800;color:#000;
  margin-bottom:12px;
}
.resource-title{font-family:'Sora',sans-serif;font-size:16px;font-weight:700;margin-bottom:6px}
.resource-subtitle{font-size:13px;color:var(--gold);font-weight:600;margin-bottom:10px}

/* ── Nav buttons ── */
.lesson-nav{
  display:flex;gap:12px;margin-top:40px;padding-top:28px;
  border-top:1px solid var(--border);
}
.nav-btn{
  flex:1;padding:13px 20px;border-radius:12px;border:1px solid var(--border);
  background:var(--card);color:var(--txt2);cursor:pointer;
  font-family:'DM Sans',sans-serif;font-size:14px;font-weight:500;
  transition:all .25s;display:flex;align-items:center;gap:8px;
}
.nav-btn:hover{border-color:var(--border2);color:var(--txt);background:var(--card2)}
.nav-btn.primary{
  background:linear-gradient(135deg,var(--gold),var(--coral));
  border-color:transparent;color:#000;font-weight:700;
}
.nav-btn.primary:hover{opacity:.9;transform:translateY(-1px);box-shadow:var(--gold-glow)}
.nav-btn-right{margin-left:auto}

/* ── Complete btn ── */
.complete-btn{
  display:inline-flex;align-items:center;gap:8px;
  background:rgba(16,185,129,.12);border:1px solid rgba(16,185,129,.25);
  color:var(--green);padding:9px 18px;border-radius:9px;cursor:pointer;
  font-size:13px;font-weight:600;font-family:'DM Sans',sans-serif;
  transition:all .2s;margin-top:8px;
}
.complete-btn:hover{background:rgba(16,185,129,.2)}
.complete-btn.done{opacity:.6;cursor:default}

/* ── Feynman ── */
.feynman-round{
  background:var(--card);border:1px solid var(--border);border-radius:var(--radius-lg);
  padding:24px;margin-bottom:20px;
}
.feynman-badge{
  display:inline-flex;align-items:center;gap:6px;font-size:11px;font-weight:700;
  padding:4px 12px;border-radius:99px;margin-bottom:14px;
  background:rgba(124,58,237,.15);color:#C4B5FD;border:1px solid rgba(124,58,237,.25);
  text-transform:uppercase;letter-spacing:.05em;
}

/* ── Responsive ── */
@media(max-width:768px){
  .main{margin-left:0}
  .sidebar{transform:translateX(-100%)}
  .sidebar.open{transform:translateX(0)}
  .content{padding:24px 20px 60px}
  .hero-title{font-size:28px}
  .modules-grid{grid-template-columns:1fr}
  .menu-btn{display:flex}
  .lesson-nav{flex-direction:column}
}
`;

// ─────────────────────────────────────────────
// COURSE DATA
// ─────────────────────────────────────────────
const MODULES_DATA = [
  {
    id:"m1", icon:"📅", number:"01",
    title:"Plan de Aprendizaje 20 Horas",
    subtitle:"El 20% que genera el 80% de resultados",
    accent:"#F59E0B", lessons: [
      { id:"m1-l1", title:"Sesión 1: Ecosistema de Herramientas IA", duration:"2 horas", icon:"🛠️",
        tag:"Módulo 1", desc:"Entiende qué hace cada herramienta y cómo se conectan entre sí para crear tu base de operaciones.",
        sections:[
          { type:"heading", text:"Objetivo de la sesión" },
          { type:"text", text:"El error más común del principiante es acumular herramientas sin saber para qué sirve cada una. Antes de tocar un solo anuncio o publicar un solo post, necesitas tener claro el ecosistema completo." },
          { type:"heading", text:"El ecosistema de herramientas" },
          { type:"table", headers:["Herramienta","Para qué sirve en tu proyecto","Costo inicial"],
            rows:[
              ["ChatGPT / Gemini","Investigación, copies, guiones, emails","Gratis"],
              ["Canva AI","Diseño de piezas visuales y videos cortos","$13 USD/mes"],
              ["CapCut","Edición de Reels con subtítulos automáticos","Gratis"],
              ["Metricool","Programación y analítica de redes","Gratis (básico)"],
              ["Mailchimp","Email marketing automatizado","Gratis hasta 500"],
              ["Google Analytics 4","Comportamiento de usuarios en web","Gratis"],
              ["Meta Ads Manager","Publicidad pagada con IA predictiva","Desde $5/día"]
            ]},
          { type:"callout", variant:"important", icon:"⚡", text:"Regla de oro: domina una herramienta antes de agregar otra. Canva + ChatGPT + Metricool son suficientes para el primer mes completo." },
          { type:"heading", text:"Recursos recomendados" },
          { type:"list", items:["Video: 'Herramientas de IA para Marketing 2024' — Vilma Núñez (YouTube)","Guía de bienvenida de HubSpot Academia en español (gratuita)","Canal oficial de Canva en Español"] },
          { type:"exercise", text:"Crea cuentas gratuitas en las 7 herramientas de la tabla. Luego escribe en una hoja: ¿Qué problema resuelve Impulso Digital? ¿A quién? ¿Por qué alguien te elegiría a ti y no a otro? Este perfil será el insumo base que le darás a la IA en todas las sesiones siguientes." }
        ]
      },
      { id:"m1-l2", title:"Sesión 2: Investigación de Cliente Ideal con IA", duration:"2 horas", icon:"🔍",
        tag:"Módulo 1", desc:"Construye el perfil de tu cliente ideal usando ChatGPT como tu investigador de mercado 24/7.",
        sections:[
          { type:"heading", text:"¿Por qué importa este paso?" },
          { type:"text", text:"La IA no conoce a tu cliente. Tú tampoco lo conoces bien todavía. Pero juntos pueden construir una hipótesis sólida que guíe cada decisión de contenido y publicidad." },
          { type:"heading", text:"Prompt base para el perfil de cliente" },
          { type:"prompt", text:`"Actúa como investigador de mercado especializado en emprendimientos latinoamericanos. Mi proyecto se llama Impulso Digital y [describe tu producto/servicio en 2 líneas]. Mi público objetivo tiene entre 25 y 45 años, vive en [país/ciudad], y su problema principal es [problema]. Crea un perfil detallado de mi cliente ideal que incluya: datos demográficos, motivaciones profundas, miedos y frustraciones, qué busca en Google antes de comprar, qué palabras usa para describir su problema, y en qué redes sociales pasa más tiempo."` },
          { type:"callout", variant:"warning", icon:"⚠️", text:"ChatGPT puede inventar estadísticas ('el 73% de los usuarios latinoamericanos…'). Nunca uses esos números en publicaciones públicas sin verificarlos. Úsalos solo como hipótesis de trabajo." },
          { type:"exercise", text:"Ejecuta el prompt anterior con los datos reales de Impulso Digital. Guarda el resultado en un documento llamado 'Mi Cliente Ideal v1'. Lo usarás como insumo en todas las sesiones siguientes." }
        ]
      },
      { id:"m1-l3", title:"Sesión 3: Estrategia de Contenidos con IA", duration:"2 horas", icon:"✍️",
        tag:"Módulo 1", desc:"Crea un calendario de contenidos de 30 días en menos de 2 horas usando IA generativa.",
        sections:[
          { type:"heading", text:"Los 4 tipos de contenido que necesitas cada semana" },
          { type:"table", headers:["Tipo","Propósito","Frecuencia"],
            rows:[
              ["Educativo","Resuelve un problema real del cliente","2 por semana"],
              ["Conexión humana","Historia, proceso, detrás de cámaras","1 por semana"],
              ["Prueba social","Testimonios, resultados, casos reales","1 por semana"],
              ["Venta directa","Oferta clara, sin disculpas","1 por semana"]
            ]},
          { type:"heading", text:"Flujo de creación con IA (paso a paso)" },
          { type:"list", items:[
              "Paso 1 — Investigar temas: ChatGPT genera 20 ideas clasificadas por tipo",
              "Paso 2 — Escribir copy: prompt específico con tono de marca + estructura definida",
              "Paso 3 — Ajustar tono: la IA es el borrador, vos sois el editor",
              "Paso 4 — Diseñar: Canva AI con descripción del estilo de tu marca",
              "Paso 5 — Programar: Metricool al mejor horario automáticamente"
          ]},
          { type:"prompt", text:`"Dame 20 ideas de contenido para Instagram sobre [tu tema] que resuelvan problemas reales de [descripción de tu cliente ideal]. Clasifícalas por tipo: educativo, entretenimiento, caso de éxito, venta directa."` },
          { type:"exercise", text:"Genera el calendario de las próximas 2 semanas con el prompt de 20 ideas. Elige 10, asigna tipo y fecha. No necesitas escribir los posts todavía — solo el plan completo." }
        ]
      },
      { id:"m1-l4", title:"Sesión 4: SEO Básico Potenciado con IA", duration:"2 horas", icon:"🔎",
        tag:"Módulo 1", desc:"Que Google encuentre Impulso Digital de forma orgánica y sostenida, sin pagar un peso.",
        sections:[
          { type:"heading", text:"El 80% del SEO se resume en 3 acciones" },
          { type:"list", items:["Investigar palabras clave con intención de búsqueda real","Optimizar cada pieza de contenido (título, meta, URL)","Registrarse y configurar Google Search Console"] },
          { type:"heading", text:"Investigación de palabras clave con IA" },
          { type:"prompt", text:`"Soy dueño de [tipo de negocio] en [país]. Mi cliente ideal busca en Google frases relacionadas con [problema que resuelves]. Dame 15 palabras clave de cola larga con intención de compra o de aprendizaje, que un emprendimiento nuevo podría posicionar en los próximos 6 meses. Clasifícalas por intención: informativa, comercial, transaccional."` },
          { type:"heading", text:"Checklist de optimización SEO por página" },
          { type:"checklist", items:[
              "Título con keyword principal (máx. 60 caracteres)",
              "Metadescripción que invita al clic (máx. 155 caracteres)",
              "URL corta y descriptiva sin caracteres especiales",
              "Al menos un subtítulo H2 con variación de la keyword",
              "Imagen con texto ALT descriptivo"
          ]},
          { type:"callout", variant:"tip", icon:"💡", text:"El contenido sobreoptimizado (keyword repetida cada 2 párrafos) es penalizado por Google desde la actualización Helpful Content de 2023. Menciona la keyword 2-3 veces naturalmente y usa sinónimos el resto del tiempo." }
        ]
      },
      { id:"m1-l5", title:"Sesión 5: Meta Ads con Advantage+ IA", duration:"2 horas", icon:"📣",
        tag:"Módulo 1", desc:"Activa tu primera campaña inteligente con la IA de Meta y presupuesto controlado desde el día uno.",
        sections:[
          { type:"heading", text:"Estructura de campaña para principiantes" },
          { type:"flow", text:`CAMPAÑA
└── Objetivo: Tráfico o Conversiones
    Presupuesto: $5 USD/día mínimo

    CONJUNTO DE ANUNCIOS
    └── Audiencia: Advantage+ Audience (IA activa)
        Ubicaciones: Automáticas

        ANUNCIOS (siempre 3 variantes)
        ├── Variante A: Copy enfocado en el PROBLEMA
        ├── Variante B: Copy enfocado en el BENEFICIO
        └── Variante C: Copy con PRUEBA SOCIAL` },
          { type:"prompt", text:`"Crea 3 variantes de copy para un anuncio de Facebook. Producto: [describe tu oferta]. Público: [describe tu cliente ideal]. Objetivo: clic al sitio web. V1: enfocada en miedo o problema. V2: enfocada en beneficio o transformación. V3: enfocada en prueba social. Máximo 90 palabras por variante. Llamada a la acción clara en cada una."` },
          { type:"callout", variant:"warning", icon:"🚫", text:"No cambies la campaña antes de los 7 días. Meta tiene una fase de aprendizaje que requiere ~50 eventos de optimización. Si interrumpes antes, el algoritmo reinicia y quemas presupuesto." },
          { type:"checklist", items:[
              "Píxel de Meta instalado y verificado en mi web",
              "3 variantes de copy creadas con ChatGPT",
              "3 creatividades diseñadas en Canva AI",
              "Advantage+ Audience activado",
              "Presupuesto mínimo $5/día por 7 días"
          ]}
        ]
      },
      { id:"m1-l6", title:"Sesión 6: Email Marketing Automatizado", duration:"2 horas", icon:"📧",
        tag:"Módulo 1", desc:"Construye la secuencia de 3 emails que convierte suscriptores en clientes mientras duermes.",
        sections:[
          { type:"heading", text:"¿Por qué email sobre cualquier otro canal?" },
          { type:"text", text:"El email tiene el ROI más alto de todos los canales digitales: por cada $1 invertido, genera en promedio $36 en retorno. Y con IA, puedes construir flujos automáticos complejos en pocas horas." },
          { type:"heading", text:"El flujo mínimo viable (3 emails)" },
          { type:"table", headers:["Email","Cuándo se envía","Objetivo"],
            rows:[
              ["1 - Bienvenida","Inmediatamente al suscribirse","Entregar lo prometido + presentarte"],
              ["2 - Valor puro","2 días después","Demostrar autoridad con 1 tip accionable"],
              ["3 - Oferta","4 días después","Historia + solución + llamada a la acción"]
            ]},
          { type:"prompt", text:`"Escribe una secuencia de 3 emails de bienvenida para nuevos suscriptores de [Impulso Digital]. Tono: [cercano, profesional, motivador]. Email 1: bienvenida y entrega del recurso. Email 2: tip de valor sobre [tema relevante]. Email 3: presentación de la oferta principal sin sonar vendedor. Cada email máximo 200 palabras, asunto incluido."` },
          { type:"exercise", text:"Ejecuta el prompt y genera los 3 emails completos. Revísalos ajustando el tono a tu voz real. Configura el flujo en Mailchimp aunque no lo actives todavía — el ejercicio es la configuración completa." }
        ]
      },
      { id:"m1-l7", title:"Sesión 7: Google Analytics 4 + Looker Studio", duration:"2 horas", icon:"📊",
        tag:"Módulo 1", desc:"Lee los datos reales de tu negocio y toma decisiones basadas en evidencia, no en intuición.",
        sections:[
          { type:"heading", text:"Las 5 métricas que importan en GA4 (solo estas al inicio)" },
          { type:"table", headers:["Métrica","Qué te dice"],
            rows:[
              ["Usuarios activos","Cuánta gente real visita tu sitio"],
              ["Tasa de participación","Si la gente se queda o sale inmediatamente"],
              ["Páginas por sesión","Si navegan o solo ven una página y se van"],
              ["Conversiones","Si completan la acción que quieres (compra, registro)"],
              ["Fuente de tráfico","De dónde vienen: Google, Instagram, email"]
            ]},
          { type:"heading", text:"Usar IA para interpretar tus datos de GA4" },
          { type:"prompt", text:`"Estos son los datos de mi sitio web de los últimos 30 días: [pega los datos]. Soy dueño de [describe tu negocio]. Analiza estos resultados e identifica: qué está funcionando bien, qué tiene problemas urgentes, y dame 3 acciones concretas para mejorar el mes que viene."` },
          { type:"callout", variant:"tip", icon:"📈", text:"Conectar GA4 con Looker Studio es gratuito y toma 10 minutos. El resultado es un dashboard en tiempo real que podés compartir con colaboradores o clientes sin que accedan a tu cuenta de Google." }
        ]
      },
      { id:"m1-l8", title:"Sesión 8: Imágenes y Videos con IA", duration:"2 horas", icon:"🎨",
        tag:"Módulo 1", desc:"Produce contenido visual profesional sin diseñador ni camarógrafo.",
        sections:[
          { type:"heading", text:"Para imágenes estáticas: Canva AI" },
          { type:"list", items:[
              "Magic Design: describes lo que necesitas y Canva genera una propuesta completa",
              "Text to Image: generas ilustraciones personalizadas para tus posts",
              "Magic Write: genera copies directamente dentro del diseño",
              "Background Remover: elimina fondos de fotos en 1 clic"
          ]},
          { type:"heading", text:"Para videos cortos: CapCut" },
          { type:"list", items:[
              "Auto Captions: subtítulos automáticos en español de alta precisión",
              "AI Script: genera el guión del video antes de grabarlo",
              "Auto Cut: elimina silencios automáticamente",
              "Text to Video: convierte un guión en video animado"
          ]},
          { type:"heading", text:"Flujo semanal de producción visual (90 min/semana)" },
          { type:"flow", text:`LUNES (45 min)
→ Canva AI: genera 5 diseños para posts

MIÉRCOLES (30 min)
→ CapCut: graba y edita 1 Reel

VIERNES (15 min)
→ Metricool: programa todo el contenido` },
          { type:"exercise", text:"Crea hoy un diseño completo para un post usando Canva AI. No lo diseñes manualmente: describe lo que necesitas y deja que la IA lo genere. Ajusta solo lo que no encaje con tu marca (colores, tipografía, tono)." }
        ]
      },
      { id:"m1-l9", title:"Sesión 9: Flujo de Trabajo Semanal Integrado", duration:"2 horas", icon:"⚙️",
        tag:"Módulo 1", desc:"Conecta todas las herramientas en un sistema que ejecutas en 3 horas por semana.",
        sections:[
          { type:"heading", text:"El flujo semanal de Impulso Digital" },
          { type:"flow", text:`LUNES (45 min)
→ ChatGPT: genera 5 ideas de contenido
→ ChatGPT: escribe los 5 copies
→ Canva AI: diseña las 5 piezas

MARTES (30 min)
→ Metricool: programa los 5 posts
→ Revisar métricas de la semana anterior

MIÉRCOLES (30 min)
→ CapCut: grabar y editar 1 Reel
→ Programar el video en Metricool

JUEVES (30 min)
→ Meta Ads: revisar variantes activas
→ Pausar la más débil, crear alternativa

VIERNES (45 min)
→ GA4: revisar conversiones de la semana
→ ChatGPT: analizar datos + planear ajustes` },
          { type:"callout", variant:"tip", icon:"🗓️", text:"Herramienta de orquestación: Notion o Google Sheets. Una tabla simple con columnas: Fecha / Tipo / Copy / Estado / Métricas. Te permite ver el sistema completo de un vistazo y nunca perder el hilo." }
        ]
      },
      { id:"m1-l10", title:"Sesión 10: Evaluación y Plan 90 Días", duration:"2 horas", icon:"🎯",
        tag:"Módulo 1", desc:"Mide qué funcionó, corrige lo que no, y construye el plan del próximo trimestre.",
        sections:[
          { type:"heading", text:"Metas realistas para el primer trimestre" },
          { type:"table", headers:["Métrica","Mes 1","Mes 2","Mes 3"],
            rows:[
              ["Seguidores Instagram","0 → 300","300 → 600","600 → 1.000"],
              ["Engagement rate","—",">5%",">5%"],
              ["Suscriptores email","0 → 100","100 → 250","250 → 500"],
              ["Costo por lead","<$2 USD","<$1.5 USD","<$1 USD"],
              ["Tráfico web/mes","200 sesiones","500 sesiones","1.000 sesiones"]
            ]},
          { type:"heading", text:"Prompt de evaluación mensual" },
          { type:"prompt", text:`"Estos son los resultados de mi primer mes en marketing digital para Impulso Digital: [pega todos tus datos]. Analiza qué estrategias funcionaron mejor, qué debo eliminar o reducir, qué debo escalar, y dame un plan de 4 semanas para el mes siguiente con acciones específicas y métricas objetivo."` },
          { type:"callout", variant:"important", icon:"🏁", text:"El enfoque es lo que diferencia al emprendedor que crece del que hace mucho y no avanza. Escoge UNA sola métrica prioritaria para este mes. Una. No siete." }
        ]
      }
    ]
  },

  {
    id:"m2", icon:"📋", number:"02",
    title:"Guía Resumen de Una Página",
    subtitle:"Todo el sistema revisable en 5 minutos",
    accent:"#0D9488", lessons:[
      { id:"m2-l1", title:"Herramientas Esenciales del Ecosistema", duration:"10 min", icon:"🧰",
        tag:"Módulo 2", desc:"Las 7 herramientas que conforman tu stack completo de marketing digital con IA.",
        sections:[
          { type:"table", headers:["Herramienta","Función principal","Cuándo usarla"],
            rows:[
              ["ChatGPT","Copies, emails, guiones, investigación","Siempre: es el centro del sistema"],
              ["Canva Pro AI","Diseños, videos, presentaciones","Producción visual diaria"],
              ["CapCut","Edición de Reels con IA","Producción de video semanal"],
              ["Metricool","Programación + analítica","Publicación y revisión semanal"],
              ["Mailchimp","Email marketing automatizado","Configuración y monitoreo"],
              ["Google Analytics 4","Comportamiento en web","Revisión semanal de conversiones"],
              ["Meta Ads Manager","Publicidad pagada inteligente","Campañas activas y A/B testing"]
            ]},
          { type:"callout", variant:"important", icon:"⚡", text:"Domina una herramienta antes de agregar otra. Canva + ChatGPT + Metricool son suficientes para el primer mes completo." }
        ]
      },
      { id:"m2-l2", title:"Los 4 Pilares de Ejecución", duration:"15 min", icon:"🏛️",
        tag:"Módulo 2", desc:"Los cuatro pilares interdependientes que sostienen cualquier estrategia digital exitosa.",
        sections:[
          { type:"heading", text:"Pilar 1 — Contenido de valor" },
          { type:"list", items:["La IA genera el borrador. Tú pones el criterio y el tono de marca.","Fórmula: ChatGPT escribe → tú editas → Canva diseña → Metricool publica","Frecuencia mínima viable: 5 posts por semana","Mezcla: 40% educativo · 20% conexión humana · 20% prueba social · 20% venta"] },
          { type:"heading", text:"Pilar 2 — SEO on-page" },
          { type:"list", items:["Cada página necesita: título con keyword + metadescripción + URL limpia","Usa ChatGPT para generar títulos y metadescripciones optimizadas","Google Search Console (gratis) para ver qué búsquedas te encuentran","Resultado esperado: tráfico orgánico sostenido a partir del mes 3-4"] },
          { type:"heading", text:"Pilar 3 — Meta Ads con IA" },
          { type:"list", items:["Activa Advantage+ Audience: la IA encuentra tu público","Lanza siempre 3 variantes de creatividad: problema · beneficio · prueba social","Presupuesto mínimo para aprender: $5/día por 7 días","No toques la campaña antes de 72 horas: el algoritmo necesita tiempo"] },
          { type:"heading", text:"Pilar 4 — Email marketing automatizado" },
          { type:"list", items:["Flujo mínimo viable: Bienvenida → Valor → Oferta (3 emails, 5 días)","Tasa de apertura objetivo: >25% · Tasa de clic objetivo: >3%","Segmentación básica: separa quienes abren de quienes no","Genera los 3 emails con ChatGPT en menos de 20 minutos"] }
        ]
      },
      { id:"m2-l3", title:"Flujo de Trabajo Semanal", duration:"10 min", icon:"🔄",
        tag:"Módulo 2", desc:"El sistema de 3 horas semanales que mantiene vivo y creciendo Impulso Digital.",
        sections:[
          { type:"flow", text:`LUNES · 45 min
→ ChatGPT: 5 ideas + 5 copies
→ Canva AI: 5 piezas visuales

MARTES · 30 min
→ Metricool: programar posts
→ Revisar métricas anteriores

MIÉRCOLES · 30 min
→ CapCut: grabar y editar 1 Reel
→ Programar video en Metricool

JUEVES · 30 min
→ Meta Ads: revisar variantes
→ Pausar débiles · crear alternativa

VIERNES · 45 min
→ GA4: revisar conversiones
→ ChatGPT: análisis + plan semana siguiente

        ↓              ↓              ↓
   CREAR CON IA   DISTRIBUIR      MEDIR` }
        ]
      },
      { id:"m2-l4", title:"Las 4 Métricas que Importan", duration:"10 min", icon:"📈",
        tag:"Módulo 2", desc:"Las únicas métricas que necesitas monitorear para tomar decisiones correctas.",
        sections:[
          { type:"table", headers:["Métrica","Dónde medirla","Señal de alarma"],
            rows:[
              ["Tráfico orgánico","GA4 → Adquisición","Caída >20% en 2 semanas"],
              ["Tasa de apertura email","Mailchimp","Por debajo del 20%"],
              ["Costo por resultado","Meta Ads Manager","Sube >50% en 3 días"],
              ["ROAS","Meta Ads Manager","Por debajo de 2x"]
            ]},
          { type:"callout", variant:"warning", icon:"🚫", text:"Lo que NO mides al inicio: seguidores totales, likes, impresiones, alcance. Son métricas de vanidad. Mides conversiones y costo. Las métricas de vanidad no pagan el alquiler." }
        ]
      },
      { id:"m2-l5", title:"Errores Comunes y Cómo Evitarlos", duration:"10 min", icon:"❌",
        tag:"Módulo 2", desc:"Los 5 errores que frenan a la mayoría de emprendedores y cómo solucionarlos.",
        sections:[
          { type:"list", items:[
              "❌ No entrenar la IA con tu tono de marca → incluye siempre: 'Usa este tono: [descripción]. Estas son 3 frases que yo usaría: [ejemplos]'",
              "❌ Ignorar la segmentación → pregúntate siempre: ¿esto está escrito para UNA persona específica o para todo el mundo?",
              "❌ No hacer A/B testing → lanza siempre 2 versiones de cada anuncio y email. La IA necesita datos para optimizar",
              "❌ Confundir likes con ventas → configura al menos 1 conversión en GA4 (registro, compra, clic a WhatsApp)",
              "❌ Creerle todo a la IA sin revisar → la IA puede inventar datos y estadísticas. Revisa manualmente antes de publicar"
          ]},
          { type:"heading", text:"Prompt de emergencia (cuando no sabes qué publicar)" },
          { type:"prompt", text:`"Soy dueño de [Impulso Digital / describe tu negocio]. Mi cliente ideal es [descripción]. Hoy no sé qué publicar. Dame 5 ideas de contenido para Instagram que resuelvan un problema real de mi audiencia, generen conversación en comentarios, y no suenen a publicidad. Para cada idea: dame el gancho de la primera línea, el desarrollo en 3 puntos y una llamada a la acción."` }
        ]
      }
    ]
  },

  {
    id:"m3", icon:"🧪", number:"03",
    title:"Ponte a Prueba Hasta Fallar",
    subtitle:"10 preguntas de dificultad progresiva",
    accent:"#7C3AED", lessons:[
      { id:"m3-l1", title:"Preguntas Nivel Principiante (1-2)", duration:"20 min", icon:"🌱",
        tag:"Módulo 3", desc:"Evalúa tu comprensión de los fundamentos: prompts efectivos y elementos de un buen post.",
        sections:[
          { type:"quiz", num:"Pregunta 1 · Principiante", question:"¿Qué diferencia hay entre un prompt genérico y un prompt efectivo para marketing?",
            answer:[
              { type:"text", text:"Un prompt efectivo incluye: contexto del negocio (quién eres, qué haces, para quién), descripción del cliente ideal (edad, problema, frustración específica), tono definido con referencia concreta, estructura solicitada (gancho + desarrollo + cierre) y límite de palabras." },
              { type:"callout", variant:"warning", icon:"⚠️", text:"Matiz clave: la IA no tiene memoria entre conversaciones. Si no incluyes el contexto en CADA prompt, genera contenido genérico que podría ser de cualquier marca del planeta." }
            ]
          },
          { type:"quiz", num:"Pregunta 2 · Principiante", question:"¿Cuáles son los 3 elementos que determinan si un post de Instagram va a funcionar, antes de publicarlo?",
            answer:[
              { type:"list", items:[
                  "El gancho (primera línea): el 90% decide en 1 segundo si sigue leyendo o hace scroll. Debe generar curiosidad, identificar dolor o hacer una promesa específica.",
                  "La llamada a la acción (CTA): ¿qué quieres que haga quien lee? Si no lo dices explícitamente, no lo harán.",
                  "La relevancia para tu cliente ideal: ¿está escrito para UNA persona específica, o para todo el mundo?"
              ]},
              { type:"callout", variant:"tip", icon:"💡", text:"Los hashtags no son un elemento determinante desde 2022. Instagram prioriza la retención sobre los hashtags. Un buen gancho vale más que 30 hashtags." }
            ]
          }
        ]
      },
      { id:"m3-l2", title:"Preguntas Nivel Intermedio (3-5)", duration:"30 min", icon:"🌿",
        tag:"Módulo 3", desc:"Profundiza en Meta Ads, email marketing y SEO con IA.",
        sections:[
          { type:"quiz", num:"Pregunta 3 · Intermedio", question:"¿Cómo configurarías una campaña de Meta Ads con Advantage+ para Impulso Digital con $150 USD de presupuesto mensual?",
            answer:[
              { type:"flow", text:`CAMPAÑA: Objetivo Tráfico o Conversiones
└── Presupuesto: $5/día ($150/mes)
    CONJUNTO DE ANUNCIOS
    └── Audiencia: Advantage+ Audience ACTIVADO
        Ubicaciones: Automáticas
        ANUNCIOS (3 variantes)
        ├── Variante A: Copy problema
        ├── Variante B: Copy beneficio
        └── Variante C: Copy prueba social` },
              { type:"callout", variant:"warning", icon:"⚠️", text:"No cambiar la campaña en los primeros 7 días. Meta necesita ~50 eventos de optimización para aprender. Interrumpir antes reinicia el proceso y quemas presupuesto." }
            ]
          },
          { type:"quiz", num:"Pregunta 4 · Intermedio", question:"¿Qué es la tasa de apertura en email, por qué puede ser engañosa, y cómo sabrías si tus emails realmente funcionan?",
            answer:[
              { type:"text", text:"Desde 2021, Apple Mail Privacy Protection precarga imágenes de rastreo aunque nadie haya abierto el email, inflando artificialmente las tasas de apertura. Las métricas que no mienten son:" },
              { type:"list", items:["Tasa de clics (CTR): ¿cuántos hicieron clic en un enlace dentro del email?","Tasa de conversión: ¿cuántos completaron la acción después del clic?","Respuestas directas: la señal de engagement más fuerte","Cancelaciones: si suben, algo falla en el contenido o frecuencia"] }
            ]
          },
          { type:"quiz", num:"Pregunta 5 · Intermedio", question:"¿Cuáles son los 3 pasos para crear contenido SEO con IA sin cometer el error de la sobreoptimización?",
            answer:[
              { type:"list", items:[
                  "Paso 1 — Investigar intención de búsqueda (no solo keywords): distinguir entre informativa, comercial y transaccional.",
                  "Paso 2 — Estructurar el artículo con IA: título H1, metadescripción, 4 subtítulos H2, FAQ.",
                  "Paso 3 — Escribir para personas, no para robots: la IA tiende a sobreoptimizar. Reescribe en tu propia voz."
              ]},
              { type:"callout", variant:"warning", icon:"⚠️", text:"Sobreoptimización: poner la keyword en el título, los primeros 100 caracteres, 3 subtítulos, y 8 veces en el cuerpo. Google lo detecta como spam. Menciona la keyword 2-3 veces naturalmente." }
            ]
          }
        ]
      },
      { id:"m3-l3", title:"Preguntas Nivel Avanzado (6-8)", duration:"40 min", icon:"🌳",
        tag:"Módulo 3", desc:"Diagnóstico de GA4, reactivación de email y distribución de presupuesto.",
        sections:[
          { type:"quiz", num:"Pregunta 6 · Avanzado", question:"En GA4 detectas una caída del 35% en tráfico orgánico en 14 días. ¿Cuál es tu proceso de diagnóstico con IA?",
            answer:[
              { type:"list", items:[
                  "Paso 1: Confirmar que no es error de medición (Tag Assistant, fechas correctas, cambios en el sitio)",
                  "Paso 2: Identificar qué páginas perdieron tráfico en GA4 → Participación → Páginas",
                  "Paso 3: Google Search Console: ¿cayeron impresiones + clics? (algoritmo) o solo clics? (CTR bajo)",
                  "Paso 4: Verificar si coincide con una actualización de Google",
                  "Paso 5: ChatGPT con los datos: análisis de causas + plan de recuperación de 30 días"
              ]}
            ]
          },
          { type:"quiz", num:"Pregunta 7 · Avanzado", question:"¿Cómo diseñarías una secuencia de email para recuperar suscriptores inactivos por 60 días?",
            answer:[
              { type:"table", headers:["Email","Asunto","Objetivo"],
                rows:[
                  ["Email 1 (día 1)","'¿Todo bien por allá?'","Reenganche emocional + recurso de valor"],
                  ["Email 2 (día 4)","'Lo mejor que publicamos mientras no estabas'","Mostrar contenido de valor perdido"],
                  ["Email 3 (día 8)","'¿Seguimos o te damos de baja?'","Decisión final: quedarse o darse de baja"]
                ]},
              { type:"callout", variant:"tip", icon:"💡", text:"Quien no abrió ninguno de los 3 emails: eliminar de la lista. Una lista de 300 que abre es más valiosa que 3.000 que ignoran. Y mejora tu sender reputation." }
            ]
          },
          { type:"quiz", num:"Pregunta 8 · Avanzado", question:"Tienes $300 USD para el próximo mes. ¿Cómo los distribuyes entre los 4 pilares?",
            answer:[
              { type:"table", headers:["Canal","Inversión","Justificación"],
                rows:[
                  ["Meta Ads","$150 USD","Resultados inmediatos + datos de audiencia"],
                  ["Herramientas (Canva + Metricool)","$50 USD","Infraestructura de producción"],
                  ["Contenido (tiempo/freelancer)","$70 USD","Sin contenido de valor, los ads no convierten"],
                  ["SEO / Email","$30 USD","Plataformas gratuitas, inversión mínima en análisis"]
                ]}
            ]
          }
        ]
      },
      { id:"m3-l4", title:"Preguntas Nivel Experto (9-10)", duration:"30 min", icon:"🏆",
        tag:"Módulo 3", desc:"Alucinaciones de IA y la estrategia completa de 90 días.",
        sections:[
          { type:"quiz", num:"Pregunta 9 · Experto", question:"¿Cómo detectarías y corregirías una 'alucinación' de ChatGPT en un copy de marketing?",
            answer:[
              { type:"heading", text:"Sistema de verificación en 3 niveles" },
              { type:"list", items:[
                  "Nivel 1 — Datos numéricos: verificar en Statista, HubSpot State of Marketing, IAB Latin America. Sin fuente en 5 min → eliminar el dato.",
                  "Nivel 2 — Citas y atribuciones: buscar la frase exacta en Google. Si no aparece en fuentes confiables, la IA la inventó.",
                  "Nivel 3 — Afirmaciones sobre tu negocio: si la IA describe servicios o clientes que no existen, ese copy crea expectativas falsas."
              ]},
              { type:"callout", variant:"important", icon:"🧠", text:"La IA no sabe que está mintiendo. No hay intención maliciosa. El error no es de la herramienta: es tuyo si publicas sin verificar." }
            ]
          },
          { type:"quiz", num:"Pregunta 10 · Experto", question:"Diseña una estrategia de 90 días para llevar Impulso Digital de 0 a 1.000 seguidores con engagement >5% y costo por lead <$1 USD.",
            answer:[
              { type:"table", headers:["Período","Fase","Acciones clave"],
                rows:[
                  ["Mes 1 (sem 1-2)","Cimientos","GA4 + píxel + emails bienvenida configurados"],
                  ["Mes 1 (sem 3-4)","Prueba","5 posts/semana + primer ciclo de ads ($35)"],
                  ["Mes 2","Escalar","Duplicar presupuesto en creatividad ganadora + SEO"],
                  ["Mes 3","Conversión","Lead magnet + campaña específica + dashboard Looker"]
                ]},
              { type:"callout", variant:"tip", icon:"🎯", text:"La métrica de control de los 90 días no son los seguidores: es el costo por lead calificado. Si alguien descarga tu recurso, entra a tu lista y abre tus mensajes, ese es un lead real." }
            ]
          }
        ]
      }
    ]
  },

  {
    id:"m4", icon:"🪜", number:"04",
    title:"La Escalera de Aprendizaje",
    subtitle:"5 niveles de cero a estratega con IA",
    accent:"#10B981", lessons:[
      { id:"m4-l1", title:"Nivel 1 — Explorador", duration:"3 semanas", icon:"🌱",
        tag:"Módulo 4", desc:"Reconoce el terreno y arma tu base de operaciones con las herramientas fundamentales.",
        sections:[
          { type:"heading", text:"¿Qué sé hacer en este nivel?" },
          { type:"list", items:[
              "Abro ChatGPT y escribo un prompt con contexto completo obteniendo resultado útil en el primer intento",
              "Creo un diseño desde cero en Canva AI usando Magic Design o Text to Image",
              "Conecto mis redes en Metricool y programo un post para fecha y hora específica",
              "Explico los 4 pilares del marketing digital a otra persona sin leer notas",
              "Tengo mi perfil de cliente ideal documentado (400-600 palabras)",
              "Perfil de Google Business completo y optimizado"
          ]},
          { type:"heading", text:"🏁 Hito de salida del Nivel 1" },
          { type:"callout", variant:"tip", icon:"🏁", text:"Publicar 3 posts en Instagram completamente creados con IA (copy en ChatGPT + diseño en Canva AI) y programados en Metricool para los mejores horarios. No importa el resultado — importa haber completado el ciclo completo." },
          { type:"heading", text:"🌉 Puente hacia el Nivel 2" },
          { type:"checklist", items:[
              "Tengo el perfil de cliente ideal documentado y guardado",
              "Publiqué al menos 3 posts usando el flujo completo de IA",
              "Puedo explicar los 4 pilares a otra persona sin leer notas"
          ]}
        ]
      },
      { id:"m4-l2", title:"Nivel 2 — Creador", duration:"3-4 semanas", icon:"✨",
        tag:"Módulo 4", desc:"Produce contenido consistente que genera audiencia real con sistemas de IA.",
        sections:[
          { type:"heading", text:"¿Qué sé hacer en este nivel?" },
          { type:"list", items:[
              "Tengo un calendario de contenidos de 30 días construido con ChatGPT",
              "Publico con consistencia mínima de 5 posts semanales durante 4 semanas",
              "Produzco artículos de 800-1.200 palabras con estructura SEO usando IA",
              "Leo e interpreto métricas básicas semanalmente en Metricool",
              "Grabo y edito al menos 1 Reel por semana usando CapCut"
          ]},
          { type:"callout", variant:"warning", icon:"⚠️", text:"El error más común del Nivel 2: perfeccionismo. Esperar a tener el logo perfecto, el copy perfecto, la iluminación perfecta. El contenido publicado con defectos supera infinitamente al contenido perfecto que nunca sale." },
          { type:"heading", text:"🏁 Hito de salida del Nivel 2" },
          { type:"callout", variant:"tip", icon:"🏁", text:"Publicar 8 contenidos generados con IA (posts + al menos 1 video) en 2 semanas consecutivas, y alcanzar 500 seguidores con engagement rate promedio superior al 4%." }
        ]
      },
      { id:"m4-l3", title:"Nivel 3 — Activador", duration:"4-6 semanas", icon:"⚡",
        tag:"Módulo 4", desc:"Pon tu contenido a trabajar con publicidad inteligente que optimiza sola.",
        sections:[
          { type:"heading", text:"¿Qué sé hacer en este nivel?" },
          { type:"list", items:[
              "Configuro una campaña completa en Meta Ads con Advantage+ y 3 variantes",
              "Ejecuto ciclos de A/B testing: lanzar → medir 7 días → pausar débil → escalar ganadora",
              "Calculo el ROAS básico y sé interpretarlo",
              "Tengo el píxel de Meta instalado midiendo al menos 1 evento de conversión"
          ]},
          { type:"heading", text:"El proceso de A/B testing" },
          { type:"list", items:[
              "1. Crear 3 variantes de copy con ChatGPT (problema · beneficio · prueba social)",
              "2. Crear 3 variantes visuales en Canva AI",
              "3. Lanzar con el mismo presupuesto por variante",
              "4. Esperar mínimo 7 días antes de tomar decisiones",
              "5. Pausar las 2 variantes más débiles",
              "6. Escalar el presupuesto de la ganadora",
              "7. Crear nueva variante para competir contra la ganadora (ciclo continuo)"
          ]},
          { type:"heading", text:"🏁 Hito de salida del Nivel 3" },
          { type:"callout", variant:"tip", icon:"🏁", text:"Completar al menos 1 ciclo de A/B testing (lanzar → medir → pausar → escalar) con píxel instalado y ROAS documentado. El resultado en dinero no importa para este hito — importa el proceso." }
        ]
      },
      { id:"m4-l4", title:"Nivel 4 — Automatizador", duration:"6-8 semanas", icon:"🤖",
        tag:"Módulo 4", desc:"Construye sistemas de email, SEO técnico y dashboards que trabajan sin que estés presente.",
        sections:[
          { type:"heading", text:"Flujo de email automatizado (comportamiento)" },
          { type:"flow", text:`Suscripción
    ↓ (inmediato)
Email 1: Bienvenida + recurso prometido
    ↓ (2 días después)
Email 2: Tip de valor profundo
    ↓ (2 días después)
Email 3: Historia + oferta principal
    ↓ (3 días después)
Segmentación automática:
├── Abrió los 3 → flujo "prospecto caliente"
└── No abrió ninguno → flujo de reactivación` },
          { type:"heading", text:"SEO técnico básico con IA" },
          { type:"checklist", items:[
              "PageSpeed Insights: si carga >3 segundos en móvil, pierdes el 40% de visitantes",
              "Search Console: rastrear errores 404 (visitantes que llegan y se van)",
              "Sitemap XML: le dice a Google qué páginas indexar",
              "URLs limpias: '/marketing-con-ia' posiciona mejor que '/p=147'",
              "Mobile-first: Google indexa primero la versión móvil desde 2023"
          ]},
          { type:"heading", text:"🏁 Hito de salida del Nivel 4" },
          { type:"callout", variant:"tip", icon:"🏁", text:"Tener 3 flujos de email automatizados activos con tasa de conversión >3% medida en 30 días, y un dashboard en Looker Studio funcionando con datos reales de GA4." }
        ]
      },
      { id:"m4-l5", title:"Nivel 5 — Estratega", duration:"6-8 semanas", icon:"🎯",
        tag:"Módulo 4", desc:"Usa IA predictiva para anticiparte al mercado, integra CRM y gestiona la reputación en tiempo real.",
        sections:[
          { type:"heading", text:"¿Qué sé hacer en este nivel?" },
          { type:"list", items:[
              "Uso datos históricos de 90 días para análisis predictivo de demanda con ChatGPT",
              "Analizo el sentimiento de mi audiencia con IA (comentarios, DMs, reviews)",
              "Tengo HubSpot CRM conectado con Mailchimp y mi web",
              "La IA de HubSpot predice qué leads tienen mayor probabilidad de convertir",
              "Tengo Google Alerts configurado para monitoreo de reputación en tiempo real"
          ]},
          { type:"prompt", text:`"Estos son los datos de tráfico, conversiones y comportamiento de mis últimos 90 días: [datos]. Identifica patrones estacionales, días de la semana con mayor conversión, y tipos de contenido que correlacionan con picos de ventas. Dame una previsión de demanda para los próximos 30 días y las acciones de marketing que debería anticipar."` },
          { type:"heading", text:"🏁 Hito de salida del Nivel 5" },
          { type:"callout", variant:"tip", icon:"🏁", text:"Tener una estrategia que se autooptimiza semanalmente con inputs de IA, un CRM conectado con los flujos de email, y la capacidad de anticipar tendencias con al menos 2 semanas de anticipación basándose en datos históricos propios." }
        ]
      }
    ]
  },

  {
    id:"m5", icon:"📚", number:"05",
    title:"Los Mejores Recursos de Aprendizaje",
    subtitle:"El directorio definitivo para Impulso Digital",
    accent:"#F97316", lessons:[
      { id:"m5-l1", title:"Recurso 1 — Curso Práctico (Platzi + Domestika)", duration:"30 min", icon:"🎓",
        tag:"Módulo 5", desc:"Los dos únicos cursos en español que actualizan su contenido con frecuencia suficiente para seguir siendo relevantes.",
        sections:[
          { type:"heading", text:"OPCIÓN A — Platzi" },
          { type:"table", headers:["Curso","Para qué nivel","Tiempo"],
            rows:[
              ["Fundamentos de Marketing Digital","Nivel 1-2","8 horas"],
              ["ChatGPT para Marketing de Contenidos","Nivel 1-3","6 horas"],
              ["Estrategia de Contenidos con IA","Nivel 2-3","7 horas"],
              ["Google Analytics 4","Nivel 2-4","10 horas"],
              ["Meta Ads: Campañas con IA","Nivel 3-4","8 horas"],
              ["Email Marketing Automatizado","Nivel 3-4","6 horas"],
              ["SEO Avanzado con IA","Nivel 4-5","9 horas"]
            ]},
          { type:"heading", text:"OPCIÓN B — Domestika" },
          { type:"list", items:[
              "IA para Marketing y Negocios Digitales — $15-25 USD pago único — Nivel 1-3",
              "Canva para Redes Sociales con IA — $12-20 USD — Nivel 1-2",
              "Estrategia de Contenidos Digitales — $15-25 USD — Nivel 2-3",
              "Email Marketing Efectivo — $15-25 USD — Nivel 3-4"
          ]},
          { type:"callout", variant:"tip", icon:"💡", text:"Regla del 50/50: por cada hora de curso, dedica una hora de práctica aplicada a Impulso Digital. El aprendizaje que no se aplica en 48 horas se olvida en 2 semanas." }
        ]
      },
      { id:"m5-l2", title:"Recurso 2 — Marketing 6.0 de Kotler", duration:"20 min", icon:"📖",
        tag:"Módulo 5", desc:"El único libro que captura con precisión el paradigma actual: convergencia de marketing, IA y experiencia humana.",
        sections:[
          { type:"heading", text:"¿Por qué este libro y no los 50 de marketing que existen?" },
          { type:"text", text:"La mayoría de libros de marketing digital envejecen en 18 meses. Marketing 6.0 es diferente porque no te enseña a usar herramientas: te enseña a pensar estratégicamente en un entorno donde la IA, el metaverso y la experiencia omnicanal coexisten." },
          { type:"heading", text:"Plan de lectura para Impulso Digital" },
          { type:"table", headers:["Semana","Sección","Aplicación práctica"],
            rows:[
              ["Semana 1","Introducción + Parte 1 (contexto)","Reescribir la propuesta de valor de Impulso Digital"],
              ["Semana 2","Parte 2 (omnicanalidad)","Mapear los puntos de contacto actuales de tu marca"],
              ["Semana 3","Parte 3 (experiencia del cliente)","Diseñar el recorrido completo del cliente ideal"],
              ["Semana 4","Parte 4 (casos aplicados)","Identificar el caso más parecido a Impulso Digital"]
            ]},
          { type:"callout", variant:"info", icon:"📚", text:"Complemento recomendado: 'Hábitos Atómicos' de James Clear. No es de marketing, pero resuelve el problema más grande del emprendedor digital: la consistencia de ejecución." }
        ]
      },
      { id:"m5-l3", title:"Recurso 3 — Vilma Núñez + Convierte Más", duration:"15 min", icon:"👩‍💼",
        tag:"Módulo 5", desc:"La referente hispana que enseña desde la práctica real con presupuestos ajustados.",
        sections:[
          { type:"heading", text:"¿Por qué Vilma Núñez para Impulso Digital?" },
          { type:"list", items:[
              "Enseña lo que practica: construyó su negocio desde cero en Latinoamérica con las mismas restricciones de Impulso Digital",
              "Actualiza su contenido de IA constantemente: fue de las primeras en integrar IA de forma práctica y honesta en español",
              "Su comunidad resuelve problemas reales: no es un grupo de spam, tiene filtros de calidad activos"
          ]},
          { type:"heading", text:"Otros referentes que complementan" },
          { type:"table", headers:["Referente","Especialidad","Canal"],
            rows:[
              ["Romuald Fons","SEO avanzado con IA","YouTube + Blog"],
              ["Ángel Candelario","Meta Ads para principiantes","YouTube"],
              ["Coco Solution","Email marketing en español","YouTube + Newsletter"],
              ["midudev","Prompts de marketing y IA","YouTube + GitHub"]
            ]},
          { type:"callout", variant:"tip", icon:"💡", text:"Método recomendado: 1 video de Vilma por semana, aplicado inmediatamente a Impulso Digital. No acumules videos sin aplicar — el conocimiento sin práctica es trivia, no habilidad." }
        ]
      },
      { id:"m5-l4", title:"Recurso 4 — Google Skillshop + Meta Blueprint", duration:"25 min", icon:"🎯",
        tag:"Módulo 5", desc:"Las guías oficiales siempre actualizadas, escritas por las mismas personas que diseñaron las herramientas.",
        sections:[
          { type:"heading", text:"Google Skillshop — Certificaciones clave" },
          { type:"table", headers:["Certificación","Nivel recomendado","Duración"],
            rows:[
              ["Google Analytics 4","Nivel 2 en adelante","4-6 horas"],
              ["Google Ads Search","Nivel 4 en adelante","3-4 horas"],
              ["Google Business Profile","Nivel 1","1-2 horas"],
              ["Search Console","Nivel 2-3","2-3 horas"]
            ]},
          { type:"heading", text:"Meta Blueprint — Módulos prioritarios" },
          { type:"table", headers:["Módulo","Nivel","Por qué es crítico"],
            rows:[
              ["Introducción a Meta Ads","Nivel 1-2","Arquitectura antes de gastar dinero"],
              ["Advantage+ Audience","Nivel 3","IA para audiencias con presupuesto pequeño"],
              ["Píxel de Meta y Medición","Nivel 3","Sin píxel los ads son un gasto, no inversión"],
              ["Creatividades que convierten","Nivel 2-3","Diseño + copywriting para ads efectivos"]
            ]},
          { type:"callout", variant:"important", icon:"🏆", text:"Certificación más valiosa para comenzar: 'Meta Certified Digital Marketing Associate'. Gratuita, válida 1 año, reconocida por clientes y el mercado." }
        ]
      },
      { id:"m5-l5", title:"Recurso 5 — Repositorio de Prompts de Marketing", duration:"20 min", icon:"⚙️",
        tag:"Módulo 5", desc:"Los atajos que construyeron quienes ya hicieron las pruebas y errores por vos.",
        sections:[
          { type:"heading", text:"Los prompts más valiosos por categoría" },
          { type:"prompt", text:`CONTENIDO — Carrusel de Instagram:
"Escribe un carrusel de 5 diapositivas para Instagram sobre [tema]. Audiencia: [descripción]. Tono: [definir]. Cada diapositiva: título impactante + 2 líneas de desarrollo. Última: llamada a la acción."` },
          { type:"prompt", text:`COPYWRITING — Anuncio variante problema:
"Escribe el copy de un anuncio de Facebook para [producto]. Primera línea: identifica el dolor exacto. Agitación en 2 frases. Solución en 1 frase. CTA directa. Máximo 80 palabras. Titular del anuncio (máx 27 chars)."` },
          { type:"prompt", text:`EMAIL — 10 asuntos para A/B testing:
"Genera 10 opciones de asunto para un email sobre [tema]. Variantes con: pregunta directa, número específico, urgencia real, curiosidad, beneficio claro. Máximo 50 caracteres cada uno. Marca con * las 3 más efectivas y explica brevemente por qué."` },
          { type:"heading", text:"Dónde encontrar más prompts" },
          { type:"list", items:[
              "Repositorios Notion gratuitos: buscar 'prompts de marketing digital en español'",
              "GitHub de midudev: prompts de IA para negocios actualizados",
              "PromptBase.com: marketplace con prompts especializados ($2-10 USD cada uno)"
          ]}
        ]
      }
    ]
  },

  {
    id:"m6", icon:"🧠", number:"06",
    title:"La Técnica de Feynman",
    subtitle:"Aprende explicando. Domina demostrando.",
    accent:"#7C3AED", lessons:[
      { id:"m6-l1", title:"Ronda 1 — La Explicación Simple", duration:"20 min", icon:"💬",
        tag:"Módulo 6", desc:"Así funciona el marketing digital con IA para Impulso Digital — explicado para que lo entienda cualquiera.",
        sections:[
          { type:"heading", text:"El sistema completo en 5 pasos simples" },
          { type:"flow", text:`PASO 1 — Conocés a tu cliente (ChatGPT)
Le describís quién es tu cliente y la IA te
devuelve un perfil detallado de esa persona.

PASO 2 — Creás contenido que resuelve sus problemas
(ChatGPT + Canva + CapCut + Metricool)
Lo que antes tomaba medio día, ahora: 45 minutos.

PASO 3 — Pagás para amplificar lo que funciona
(Meta Ads + Advantage+)
La IA de Facebook busca personas similares
a quienes ya interactuaron con tu contenido.

PASO 4 — Capturás el contacto de quien mostró interés
(Mailchimp + automatización)
3 emails automáticos que trabajan mientras dormís.

PASO 5 — Medís qué funcionó y ajustás
(GA4 + ChatGPT para análisis)
No mirás likes. Mirás conversiones y costo.

        ↓
     CICLO QUE SE RETROALIMENTA:
más datos → mejor IA → mejores resultados` },
          { type:"callout", variant:"important", icon:"✋", text:"EJERCICIO: Antes de leer los vacíos, explícale el sistema completo a alguien (en voz alta, por escrito, o mentalmente). Tienes 3 minutos. Sin notas." }
        ]
      },
      { id:"m6-l2", title:"Los 5 Vacíos que la Mayoría Olvida", duration:"25 min", icon:"🔍",
        tag:"Módulo 6", desc:"Los errores conceptuales más comunes al explicar el sistema y cómo cerrarlos.",
        sections:[
          { type:"heading", text:"Vacío 1 — 'La IA puede inventar datos y no lo mencioné'" },
          { type:"text", text:"ChatGPT genera texto que suena plausible, no texto que es necesariamente verdadero. Si publicas estadísticas sin verificar, construyes tu estrategia sobre datos inventados y dañas tu credibilidad." },
          { type:"heading", text:"Vacío 2 — 'No definí un embudo claro de conversión'" },
          { type:"flow", text:`TOPE DEL EMBUDO (muchas personas)
→ Contenido orgánico + Meta Ads

MEDIO (menos personas, más interés)
→ Lead magnet + Email marketing

FONDO (pocas personas, alta intención)
→ Oferta clara + Seguimiento` },
          { type:"heading", text:"Vacío 3 — 'Confundí me gusta con ventas'" },
          { type:"table", headers:["Objetivo","Métrica real","Métrica de vanidad"],
            rows:[
              ["Generar leads","Costo por lead","Alcance del post"],
              ["Vender","ROAS / Costo por venta","Likes del anuncio"],
              ["Email marketing","Tasa de conversión","Tasa de apertura"]
            ]},
          { type:"heading", text:"Vacío 4 — 'No revisé manualmente los copies'" },
          { type:"list", items:[
              "Error tipo 1: Tono robótico ('en el dinámico mundo del marketing digital')",
              "Error tipo 2: Promesas exageradas ('la solución definitiva', 'resultados garantizados')",
              "Error tipo 3: Pérdida de voz de marca (suena formal cuando deberías ser cercano)",
              "Error tipo 4: Datos inventados presentados con confianza absoluta"
          ]},
          { type:"heading", text:"Vacío 5 — 'No expliqué por qué el orden importa'" },
          { type:"callout", variant:"warning", icon:"⚠️", text:"Sin contenido de valor probado orgánicamente (Paso 2), no sabes qué amplificar con ads (Paso 3). Pagar para amplificar contenido que no conecta es desperdiciar el presupuesto activamente." }
        ]
      },
      { id:"m6-l3", title:"Ronda 2 — La Re-enseñanza Completa", duration:"25 min", icon:"🔄",
        tag:"Módulo 6", desc:"La explicación correcta y completa con todos los vacíos cerrados.",
        sections:[
          { type:"heading", text:"Ahora con los vacíos integrados" },
          { type:"checklist", items:[
              "¿Mencionaste que la IA puede inventar datos y necesita supervisión humana?",
              "¿Explicaste que los likes no son ventas y qué métrica usar en cambio?",
              "¿Mostraste el orden lógico de los pasos y por qué no se pueden invertir?",
              "¿Diste un ejemplo concreto para cada paso aplicado a un negocio real?",
              "¿Explicaste el sistema sin usar jerga técnica inaccesible?",
              "¿Mencionaste que el copy generado por IA siempre necesita revisión antes de publicar?"
          ]},
          { type:"callout", variant:"tip", icon:"✅", text:"Si marcaste las 6: pasaste la Técnica de Feynman. Si marcaste menos de 6, vuelve a la Ronda 1 y estudia específicamente los vacíos que fallaste." }
        ]
      },
      { id:"m6-l4", title:"Ronda 3 — Casos de Aplicación Real", duration:"30 min", icon:"💼",
        tag:"Módulo 6", desc:"Demuestra comprensión real aplicando el sistema a 3 situaciones nuevas.",
        sections:[
          { type:"quiz", num:"Caso 1", question:"Carlos tiene 2.800 seguidores en Instagram, engagement 6%, publica 7 veces/semana con Canva y ChatGPT. En 3 meses vendió 4 prendas de su marca de ropa. ¿Cuál es el diagnóstico?",
            answer:[
              { type:"list", items:[
                  "✅ Paso 1 (Cliente): tiene perfil implícito — el 6% de engagement lo prueba",
                  "✅ Paso 2 (Contenido): crea consistentemente con buenas herramientas",
                  "❌ Paso 3 (Ads): no tiene ads activos, solo confía en el orgánico",
                  "❌ Paso 4 (Email): no tiene sistema de captura ni secuencia de nutrición",
                  "❌ Paso 5 (Métricas): mide engagement (vanidad) en lugar de conversiones"
              ]},
              { type:"text", text:"Solución: crear un lead magnet, activar Meta Ads para capturar emails a $5/día, configurar secuencia de 3 emails en Mailchimp. El problema no era la cantidad de contenido: era que no tenía adónde llevar a las personas interesadas." }
            ]
          },
          { type:"quiz", num:"Caso 2", question:"Ana invirtió $200 USD en Meta Ads en 3 días, con 1 solo anuncio, segmentación manual. No funcionó. Conclusión: 'Meta Ads no sirve para mi negocio'. ¿Cuántos errores cometió?",
            answer:[
              { type:"list", items:[
                  "Error 1: Segmentación manual en lugar de Advantage+ (limitó el algoritmo artificialmente)",
                  "Error 2: Un solo anuncio sin variantes (sin A/B testing no hay aprendizaje posible)",
                  "Error 3: Solo 3 días (Meta necesita mínimo 7 días de fase de aprendizaje)",
                  "Error 4: Copy de 200 palabras (nadie lee más de 90 en un ad de feed)",
                  "Error 5: Sin píxel instalado (Meta no podía optimizar hacia conversiones reales)"
              ]}
            ]
          },
          { type:"quiz", num:"Caso 3", question:"Julián tiene 800 suscriptores de email, tasa de apertura del 42%, CTR de 0.8%, y nunca ha vendido nada por email. ¿Cuál es el diagnóstico real?",
            answer:[
              { type:"list", items:[
                  "El 42% de apertura es una métrica inflada por Mail Privacy Protection de Apple desde 2021",
                  "El 0.8% de CTR revela la verdad: de 800 suscriptores, solo 6-7 hacen clic en algo",
                  "Causa 1: no hay llamada a la acción clara en los emails (la IA genera contenido informativo sin CTA)",
                  "Causa 2: audiencia no segmentada (todos reciben lo mismo independiente de su intención)",
                  "Causa 3: no hay embudo detrás del email (el clic lleva al blog sin ninguna oferta)"
              ]}
            ]
          }
        ]
      }
    ]
  }
];

// ─────────────────────────────────────────────
// HELPERS
// ─────────────────────────────────────────────
function ContentBlock({ block, checks, onCheck }) {
  if (block.type === "heading") return <h3 className="cb-h2 fade-in">{block.text}</h3>;
  if (block.type === "subheading") return <h4 className="cb-h3">{block.text}</h4>;
  if (block.type === "text") return <p className="cb-p">{block.text}</p>;
  if (block.type === "list") return (
    <ul className="cb-list">
      {block.items.map((item, i) => <li key={i}>{item}</li>)}
    </ul>
  );
  if (block.type === "table") return (
    <div style={{overflowX:"auto",marginBottom:14}}>
      <table className="cb-table">
        <thead><tr>{block.headers.map((h,i) => <th key={i}>{h}</th>)}</tr></thead>
        <tbody>{block.rows.map((row,i) => <tr key={i}>{row.map((cell,j) => <td key={j}>{cell}</td>)}</tr>)}</tbody>
      </table>
    </div>
  );
  if (block.type === "callout") return (
    <div className={`cb-callout ${block.variant}`}>
      <span className="cb-callout-icon">{block.icon}</span>
      <span className="cb-callout-text">{block.text}</span>
    </div>
  );
  if (block.type === "code") return <pre className="cb-code">{block.text}</pre>;
  if (block.type === "flow") return <pre className="cb-flow">{block.text}</pre>;
  if (block.type === "exercise") return (
    <div className="cb-exercise">
      <div className="cb-exercise-label">✏️ Mini-ejercicio</div>
      <div className="cb-exercise-text">{block.text}</div>
    </div>
  );
  if (block.type === "prompt") return (
    <div className="cb-prompt">
      <div className="cb-prompt-text">{block.text}</div>
    </div>
  );
  if (block.type === "checklist") return (
    <div className="cb-checklist">
      {block.items.map((item, i) => {
        const key = `check-${i}-${item.slice(0,10)}`;
        const done = checks && checks.has(key);
        return (
          <div key={i} className={`cb-check-item ${done?"checked":""}`} onClick={() => onCheck && onCheck(key)}>
            <div className="cb-check-box">{done ? "✓" : ""}</div>
            <span>{item}</span>
          </div>
        );
      })}
    </div>
  );
  if (block.type === "divider") return <div className="cb-divider" />;
  return null;
}

function QuizBlock({ block, quizOpen, onToggle }) {
  const isOpen = quizOpen.has(block.num);
  return (
    <div className="quiz-card fade-in">
      <div className="quiz-num">{block.num}</div>
      <div className="quiz-q">{block.question}</div>
      <button className="quiz-reveal-btn" onClick={() => onToggle(block.num)}>
        {isOpen ? "▲ Ocultar respuesta" : "▼ Ver respuesta completa"}
      </button>
      {isOpen && (
        <div className="quiz-answer">
          {block.answer.map((ab, i) => <ContentBlock key={i} block={ab} />)}
        </div>
      )}
    </div>
  );
}

function LessonContent({ lesson, checks, onCheck, quizOpen, onToggleQuiz }) {
  return (
    <div className="content-body">
      {lesson.sections.map((section, i) => {
        if (section.type === "quiz") {
          return <QuizBlock key={i} block={section} quizOpen={quizOpen} onToggle={onToggleQuiz} />;
        }
        return (
          <div key={i} className="cb-section" style={{animationDelay:`${i*0.05}s`}}>
            <ContentBlock block={section} checks={checks} onCheck={onCheck} />
          </div>
        );
      })}
    </div>
  );
}

// ─────────────────────────────────────────────
// MAIN COMPONENT
// ─────────────────────────────────────────────
export default function ImpulsoDigitalCourse() {
  const [view, setView] = useState("home"); // home | module | lesson
  const [activeModule, setActiveModule] = useState(null);
  const [activeLesson, setActiveLesson] = useState(null);
  const [completed, setCompleted] = useState(new Set());
  const [checks, setChecks] = useState(new Set());
  const [quizOpen, setQuizOpen] = useState(new Set());
  const [sidebarOpen, setSidebarOpen] = useState(true);
  const [animKey, setAnimKey] = useState(0);
  const mainRef = useRef(null);

  const totalLessons = MODULES_DATA.reduce((s, m) => s + m.lessons.length, 0);
  const progress = Math.round((completed.size / totalLessons) * 100);

  const navigate = (newView, mod = null, les = null) => {
    setAnimKey(k => k + 1);
    setView(newView);
    setActiveModule(mod);
    setActiveLesson(les);
    if (mainRef.current) mainRef.current.scrollTo(0, 0);
  };

  const goHome = () => navigate("home");
  const goModule = (mod) => navigate("module", mod);
  const goLesson = (mod, les) => navigate("lesson", mod, les);

  const toggleComplete = (lessonId) => {
    setCompleted(prev => {
      const n = new Set(prev);
      if (n.has(lessonId)) n.delete(lessonId); else n.add(lessonId);
      return n;
    });
  };

  const toggleCheck = (key) => {
    setChecks(prev => {
      const n = new Set(prev);
      if (n.has(key)) n.delete(key); else n.add(key);
      return n;
    });
  };

  const toggleQuiz = (key) => {
    setQuizOpen(prev => {
      const n = new Set(prev);
      if (n.has(key)) n.delete(key); else n.add(key);
      return n;
    });
  };

  const getModuleProgress = (mod) => {
    const done = mod.lessons.filter(l => completed.has(l.id)).length;
    return Math.round((done / mod.lessons.length) * 100);
  };

  const currentMod = activeModule ? MODULES_DATA.find(m => m.id === activeModule) : null;
  const currentLes = (currentMod && activeLesson) ? currentMod.lessons.find(l => l.id === activeLesson) : null;
  const lesIdx = currentMod && currentLes ? currentMod.lessons.indexOf(currentLes) : -1;
  const prevLes = lesIdx > 0 ? currentMod.lessons[lesIdx - 1] : null;
  const nextLes = lesIdx >= 0 && lesIdx < currentMod.lessons.length - 1 ? currentMod.lessons[lesIdx + 1] : null;

  return (
    <>
      <style>{STYLES}</style>
      <div className="app">
        {/* ── Sidebar ── */}
        <aside className={`sidebar ${sidebarOpen ? "open" : "closed"}`}>
          <div className="sidebar-logo" onClick={goHome} style={{cursor:"pointer"}}>
            <div className="logo-badge">🚀</div>
            <div>
              <div className="logo-text">Impulso Digital</div>
              <div className="logo-sub">Marketing con IA · Curso completo</div>
            </div>
          </div>
          <div className="sidebar-progress">
            <div className="prog-label">
              <span>Progreso general</span>
              <span style={{color:"var(--gold)",fontWeight:700}}>{progress}%</span>
            </div>
            <div className="prog-bar">
              <div className="prog-fill" style={{width:`${progress}%`}} />
            </div>
          </div>
          <nav className="sidebar-nav">
            <div className="nav-section-label">Módulos del curso</div>
            {MODULES_DATA.map(mod => {
              const modDone = mod.lessons.every(l => completed.has(l.id));
              return (
                <button
                  key={mod.id}
                  className={`module-btn ${activeModule === mod.id ? "active" : ""} ${modDone ? "done" : ""}`}
                  onClick={() => goModule(mod.id)}
                >
                  <div className="module-icon">{mod.icon}</div>
                  <div className="module-info">
                    <div className="module-num">Módulo {mod.number}</div>
                    <div className="module-name">{mod.title}</div>
                  </div>
                  <div className="module-check">{modDone ? "✓" : ""}</div>
                </button>
              );
            })}
          </nav>
        </aside>

        {/* ── Main ── */}
        <main className="main" ref={mainRef}>
          <div className="topbar">
            <div style={{display:"flex",alignItems:"center",gap:12}}>
              <button className="menu-btn" onClick={() => setSidebarOpen(v => !v)}>☰</button>
              <div className="breadcrumb">
                <span style={{cursor:"pointer",color:"var(--gold)"}} onClick={goHome}>Inicio</span>
                {currentMod && <>
                  <span>›</span>
                  <span style={{cursor:"pointer"}} onClick={() => goModule(currentMod.id)}>{currentMod.title}</span>
                </>}
                {currentLes && <><span>›</span><span style={{color:"var(--txt)"}}>{currentLes.title}</span></>}
              </div>
            </div>
            <div className="topbar-right">
              <div className="badge-count">{completed.size}/{totalLessons} lecciones</div>
            </div>
          </div>

          <div className="content" key={animKey}>
            {/* ── HOME ── */}
            {view === "home" && (
              <div>
                <div className="home-hero fade-in">
                  <div className="hero-eyebrow">
                    <div className="hero-dot" />
                    Curso completo · 6 módulos · 40 lecciones
                  </div>
                  <h1 className="hero-title">
                    Marketing Digital con IA para<br />
                    <span>Impulso Digital</span>
                  </h1>
                  <p className="hero-desc">
                    Aprende a crear contenido, activar publicidad inteligente y automatizar tu marketing
                    con herramientas de inteligencia artificial. Sin equipo, con presupuesto ajustado,
                    desde Latinoamérica.
                  </p>
                  <div className="hero-stats">
                    {[
                      {val:"20h",lbl:"De aprendizaje"},
                      {val:"6",lbl:"Módulos"},
                      {val:"40",lbl:"Lecciones"},
                      {val:"7",lbl:"Herramientas IA"},
                      {val:"5",lbl:"Niveles"}
                    ].map((s,i) => (
                      <div key={i} className="stat-card fade-in" style={{animationDelay:`${i*0.07}s`}}>
                        <div className="stat-val">{s.val}</div>
                        <div className="stat-lbl">{s.lbl}</div>
                      </div>
                    ))}
                  </div>
                </div>

                <h2 style={{fontFamily:"'Sora',sans-serif",fontSize:16,fontWeight:700,color:"var(--txt2)",marginBottom:16,textTransform:"uppercase",letterSpacing:".06em"}}>
                  Módulos del curso
                </h2>
                <div className="modules-grid">
                  {MODULES_DATA.map((mod, i) => {
                    const mp = getModuleProgress(mod);
                    return (
                      <div
                        key={mod.id}
                        className="mod-card fade-in"
                        style={{animationDelay:`${i*0.07}s`}}
                        onClick={() => goModule(mod.id)}
                      >
                        <div className="mod-card-top">
                          <div className="mod-card-icon" style={{background:`${mod.accent}18`}}>{mod.icon}</div>
                          <div className="mod-card-num">MÓDULO {mod.number}</div>
                        </div>
                        <div className="mod-card-title">{mod.title}</div>
                        <div className="mod-card-sub">{mod.subtitle}</div>
                        <div className="mod-card-footer">
                          <div className="mod-card-meta">
                            <span>📚</span>
                            <span>{mod.lessons.length} lecciones</span>
                          </div>
                          <div className="mod-card-arrow">→</div>
                        </div>
                        <div className="mod-progress-mini">
                          <div className="mod-progress-mini-fill" style={{width:`${mp}%`,background:mod.accent}} />
                        </div>
                      </div>
                    );
                  })}
                </div>
              </div>
            )}

            {/* ── MODULE VIEW ── */}
            {view === "module" && currentMod && (
              <div>
                <button className="lesson-back-btn fade-in" onClick={goHome}>← Volver al inicio</button>
                <div className="module-header fade-in">
                  <div className="module-header-top">
                    <div className="module-big-icon" style={{background:`${currentMod.accent}18`,border:`1px solid ${currentMod.accent}33`}}>
                      {currentMod.icon}
                    </div>
                    <div>
                      <div className="module-eyebrow" style={{color:currentMod.accent}}>Módulo {currentMod.number}</div>
                      <h1 className="module-title">{currentMod.title}</h1>
                      <p className="module-subtitle">{currentMod.subtitle}</p>
                    </div>
                  </div>
                </div>
                <div className="lesson-list">
                  {currentMod.lessons.map((les, i) => {
                    const isDone = completed.has(les.id);
                    return (
                      <div
                        key={les.id}
                        className={`lesson-item fade-in ${activeLesson === les.id ? "active-lesson" : ""} ${isDone ? "completed-lesson" : ""}`}
                        style={{animationDelay:`${i*0.05}s`}}
                        onClick={() => goLesson(currentMod.id, les.id)}
                      >
                        <div className="lesson-num" style={isDone?{background:"rgba(16,185,129,.2)",color:"var(--green)"}:{}}>
                          {isDone ? "✓" : String(i+1).padStart(2,"0")}
                        </div>
                        <div className="lesson-info">
                          <div className="lesson-title">{les.title}</div>
                          <div className="lesson-meta">
                            <span>{les.icon}</span>
                            <span>{les.duration}</span>
                            {isDone && <span style={{color:"var(--green)"}}>Completada ✓</span>}
                          </div>
                        </div>
                        <div className="lesson-arrow">→</div>
                      </div>
                    );
                  })}
                </div>
              </div>
            )}

            {/* ── LESSON VIEW ── */}
            {view === "lesson" && currentMod && currentLes && (
              <div>
                <div className="lesson-header fade-in">
                  <button className="lesson-back-btn" onClick={() => goModule(currentMod.id)}>
                    ← {currentMod.title}
                  </button>
                  <div className="lesson-tag">{currentLes.tag}</div>
                  <h1 className="lesson-h1">{currentLes.title}</h1>
                  <p className="lesson-desc">{currentLes.desc}</p>
                  <div style={{display:"flex",alignItems:"center",gap:12,flexWrap:"wrap"}}>
                    <div className="lesson-duration">⏱ {currentLes.duration}</div>
                    <button
                      className={`complete-btn ${completed.has(currentLes.id) ? "done" : ""}`}
                      onClick={() => !completed.has(currentLes.id) && toggleComplete(currentLes.id)}
                    >
                      {completed.has(currentLes.id) ? "✓ Lección completada" : "Marcar como completada"}
                    </button>
                  </div>
                </div>

                <div className="cb-divider" />
                <LessonContent
                  lesson={currentLes}
                  checks={checks}
                  onCheck={toggleCheck}
                  quizOpen={quizOpen}
                  onToggleQuiz={toggleQuiz}
                />

                <div className="lesson-nav">
                  {prevLes ? (
                    <button className="nav-btn" onClick={() => goLesson(currentMod.id, prevLes.id)}>
                      ← {prevLes.title}
                    </button>
                  ) : (
                    <button className="nav-btn" onClick={() => goModule(currentMod.id)}>
                      ← Ver módulo
                    </button>
                  )}
                  {nextLes ? (
                    <button className="nav-btn primary nav-btn-right" onClick={() => goLesson(currentMod.id, nextLes.id)}>
                      {nextLes.title} →
                    </button>
                  ) : (
                    <button className="nav-btn primary nav-btn-right" onClick={goHome}>
                      🏠 Ir al inicio
                    </button>
                  )}
                </div>
              </div>
            )}
          </div>
        </main>
      </div>
    </>
  );
}
