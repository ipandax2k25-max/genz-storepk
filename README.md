
<html lang="en">
<head>
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
      integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY=" crossorigin="">
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
<meta name="theme-color" content="#0A0A0A" />
<title>GEN Z — Shop Your Vibe</title>
<meta name="description" content="GEN Z — Pakistan's boldest online store." />
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<script src="https://unpkg.com/lucide@latest"></script>
<style>
/* ============================================================
   1. RESET & TOKENS
============================================================ */
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
:root{
  --black:#0a0a0a;--dark:#141414;--dark-2:#1c1c1c;--gray:#262626;
  --border:#2a2a2a;--red:#e11d48;--red-glow:#ff2a4b;
  --text:#f5f5f5;--text-muted:#a1a1aa;
  --green:#22c55e;--yellow:#facc15;
  --safe-bottom:env(safe-area-inset-bottom,0px);
  --mobile-nav-h:68px;
  --home-header-h:118px; /* measured; adjusted by JS if needed */
}
html{scroll-behavior:smooth}
body{
  font-family:'Inter',system-ui,sans-serif;
  background:var(--black);
  color:var(--text);
  line-height:1.5;
  overflow-x:hidden;
  padding-bottom:calc(var(--mobile-nav-h) + var(--safe-bottom) + 12px);
}
@media(min-width:768px){body{padding-bottom:0}}
img{max-width:100%;display:block;object-fit:cover}
button{cursor:pointer;border:none;background:none;font-family:inherit;color:inherit}
input,select,textarea{font-family:inherit;font-size:inherit}
a{text-decoration:none;color:inherit}
ul{list-style:none}
:focus-visible{outline:2px solid var(--red);outline-offset:2px}
.sr-only{position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);white-space:nowrap;border:0}
.container{max-width:1400px;margin:0 auto;padding:0 16px}
.hide-mobile{display:none}
@media(min-width:768px){.hide-mobile{display:initial}}
.text-muted{color:var(--text-muted)}
.text-sm{font-size:13px}
.text-xs{font-size:11px}
.font-bold{font-weight:700}
@media (prefers-reduced-motion:reduce){*,*::before,*::after{animation-duration:.001ms!important;transition-duration:.001ms!important}}
::-webkit-scrollbar{width:6px;height:6px}
::-webkit-scrollbar-track{background:var(--black)}
::-webkit-scrollbar-thumb{background:var(--red);border-radius:10px}

/* ============================================================
   2. TOP BAR (non-dashboard pages only use mobile nav)
   The DASHBOARD header is rendered INSIDE #app-content by JS.
============================================================ */
.top-bar{background:#000;font-size:11px;padding:6px 0;border-bottom:1px solid var(--border);color:var(--text-muted);display:none}
@media(min-width:768px){.top-bar{display:block}}
.top-bar-inner{display:flex;justify-content:space-between;flex-wrap:wrap;gap:8px}
.top-bar span{display:flex;align-items:center;gap:5px}
.top-bar svg{color:var(--red);width:14px;height:14px}

/* Home-only fixed header — rendered dynamically */
#app-content{position:relative}
.home-header{
  position:sticky;top:0;z-index:100;
  background:rgba(20,20,20,.98);
  border-bottom:1px solid var(--border);
  backdrop-filter:none;-webkit-backdrop-filter:none;
  margin:0 calc(-1 * 16px) 20px; /* bleed to container edges on mobile */
}
@media(min-width:768px){.home-header{margin:0 0 24px}}
.home-header .header-inner{display:flex;align-items:center;gap:12px;padding:10px 16px;flex-wrap:wrap}
.logo{display:flex;flex-direction:column;align-items:flex-start;line-height:1}
.logo-svg{height:30px;width:auto;display:block}
.logo p{font-size:9px;color:var(--text-muted);letter-spacing:1.5px;margin-top:2px;text-transform:uppercase}
.search-bar{flex:1;min-width:180px;display:flex;align-items:center;background:var(--dark-2);border:1px solid var(--border);border-radius:50px;overflow:hidden;padding:4px 4px 4px 16px;order:3;width:100%}
@media(min-width:768px){.search-bar{order:2;width:auto}}
.search-bar input{flex:1;background:transparent;border:none;outline:none;color:var(--text);font-size:14px;min-width:0}
.search-bar button{background:var(--red);color:#fff;width:34px;height:34px;border-radius:50%;display:flex;align-items:center;justify-content:center}
.search-bar button:hover{background:var(--red-glow);box-shadow:0 0 15px var(--red)}
.search-bar button svg{width:16px;height:16px}
.header-actions{display:flex;align-items:center;gap:14px;order:2;margin-left:auto}
.header-btn{display:flex;flex-direction:column;align-items:center;gap:2px;font-size:10px;color:var(--text-muted);position:relative}
.header-btn:hover{color:var(--red)}
.header-btn svg{width:20px;height:20px}
.badge{position:absolute;top:-4px;right:-4px;background:var(--red);color:#fff;font-size:9px;font-weight:700;min-width:16px;height:16px;padding:0 4px;border-radius:10px;display:flex;align-items:center;justify-content:center;border:2px solid var(--dark)}

/* Primary nav under dashboard header only */
.home-nav{background:rgba(20,20,20,.98);border-bottom:1px solid var(--border);overflow-x:auto;white-space:nowrap;scrollbar-width:none;margin:0 calc(-1 * 16px) 20px}
@media(min-width:768px){.home-nav{margin:0 0 24px}}
.home-nav::-webkit-scrollbar{display:none}
.home-nav .container{display:flex;gap:8px;padding:8px 16px}
.tab-btn{padding:8px 14px;border-radius:8px;font-size:13px;font-weight:600;color:var(--text-muted);background:var(--dark-2);transition:.2s;display:inline-flex}
.tab-btn.active{background:var(--red);color:#fff;box-shadow:0 0 15px rgba(225,29,72,.4)}

/* Mobile drawer */
.mobile-nav{position:fixed;top:0;left:0;width:min(85vw,340px);height:100vh;background:var(--dark);z-index:200;padding:20px;transform:translateX(-100%);transition:.25s;display:flex;flex-direction:column;gap:4px;overflow-y:auto}
.mobile-nav.open{transform:translateX(0)}
.mobile-nav-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;padding-bottom:14px;border-bottom:1px solid var(--border)}
.mobile-nav a{padding:12px 10px;border-radius:8px;font-size:15px;font-weight:500}
.mobile-nav a:hover{background:var(--dark-2);color:var(--red)}
.mobile-nav-backdrop{position:fixed;inset:0;background:rgba(0,0,0,.6);z-index:150;display:none}
.mobile-nav-backdrop.show{display:block}

/* Fixed mobile bottom nav */
nav.mobile-bottom-bar{
  position:fixed !important;bottom:0 !important;left:0 !important;right:0 !important;top:auto !important;
  width:100% !important;z-index:9999 !important;
  display:flex;justify-content:space-around;align-items:center;
  background:rgba(20,20,20,.98);border-top:1px solid var(--red);
  box-shadow:0 -4px 20px rgba(0,0,0,.6);
  padding:8px 8px;padding-bottom:calc(8px + var(--safe-bottom));
  transform:none !important;filter:none !important;
  backdrop-filter:none;-webkit-backdrop-filter:none;
}
nav.mobile-bottom-bar a{display:flex;flex-direction:column;align-items:center;justify-content:center;gap:3px;font-size:10px;color:var(--text-muted);padding:4px 8px;border-radius:8px;transition:.2s;min-width:52px;min-height:48px;flex:1;max-width:80px;text-decoration:none}
nav.mobile-bottom-bar a.active{color:var(--red)}
nav.mobile-bottom-bar a:hover,nav.mobile-bottom-bar a:active{background:var(--dark-2)}
nav.mobile-bottom-bar svg{width:22px;height:22px}
@media(min-width:768px){nav.mobile-bottom-bar{display:none !important}}

/* ============================================================
   3. BUTTONS, FORMS, TOASTS
============================================================ */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;padding:12px 20px;border-radius:10px;font-weight:700;font-size:14px;transition:.2s;border:1px solid transparent}
.btn:disabled{opacity:.5;cursor:not-allowed}
.btn-primary{background:var(--red);color:#fff;box-shadow:0 0 18px rgba(225,29,72,.35)}
.btn-primary:hover:not(:disabled){background:var(--red-glow);transform:translateY(-1px)}
.btn-secondary{background:#fff;color:#000}
.btn-secondary:hover:not(:disabled){background:#e5e5e5}
.btn-ghost{background:var(--dark-2);border-color:var(--border);color:var(--text)}
.btn-ghost:hover{border-color:var(--red);color:var(--red)}
.btn-danger{background:transparent;color:#f87171;border-color:#7f1d1d}
.btn-danger:hover{background:#7f1d1d;color:#fff}
.btn-block{width:100%}
.btn-sm{padding:8px 14px;font-size:12px}
.btn-lg{padding:14px 24px;font-size:16px}
.field{display:flex;flex-direction:column;gap:6px;margin-bottom:14px}
.field label{font-size:12px;color:var(--text-muted);font-weight:600}
.field input,.field select,.field textarea{background:var(--dark-2);border:1px solid var(--border);border-radius:10px;padding:11px 12px;color:var(--text);outline:none;transition:.2s;width:100%}
.field input:focus,.field select:focus,.field textarea:focus{border-color:var(--red);box-shadow:0 0 0 3px rgba(225,29,72,.15)}
.field .error{color:#f87171;font-size:11px;min-height:14px}
.field.invalid input,.field.invalid select,.field.invalid textarea{border-color:#f87171}
.field-row{display:grid;gap:12px;grid-template-columns:1fr}
@media(min-width:600px){.field-row.two{grid-template-columns:1fr 1fr}}
.toast-container{position:fixed;bottom:calc(var(--mobile-nav-h) + var(--safe-bottom) + 16px);left:50%;transform:translateX(-50%);z-index:10000;display:flex;flex-direction:column;gap:8px;align-items:center;pointer-events:none;width:calc(100% - 32px);max-width:400px}
@media(min-width:768px){.toast-container{bottom:24px}}
.toast{background:var(--dark-2);color:var(--text);padding:12px 18px;border-radius:10px;border-left:4px solid var(--red);font-weight:600;font-size:13px;box-shadow:0 8px 30px rgba(0,0,0,.5);pointer-events:auto;animation:toastIn .25s ease}
.toast.success{border-left-color:var(--green)}
.toast.error{border-left-color:#f87171}
.toast.warn{border-left-color:var(--yellow)}
@keyframes toastIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}
.skeleton{background:linear-gradient(90deg,var(--dark-2) 25%,var(--gray) 50%,var(--dark-2) 75%);background-size:200% 100%;animation:shimmer 1.5s infinite;border-radius:8px}
@keyframes shimmer{0%{background-position:200% 0}100%{background-position:-200% 0}}
.skeleton-card{height:280px;width:100%;border-radius:14px}
.empty-state{display:flex;flex-direction:column;align-items:center;justify-content:center;padding:60px 20px;text-align:center;color:var(--text-muted)}
.empty-state svg{width:48px;height:48px;margin-bottom:16px;color:var(--gray)}
.empty-state h3{color:var(--text);font-size:18px;margin-bottom:8px}
.empty-state p{font-size:14px;margin-bottom:16px;max-width:400px}

/* ============================================================
   4. PRODUCT CARDS
============================================================ */
.product-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px}
@media(min-width:768px){.product-grid{grid-template-columns:repeat(3,1fr);gap:16px}}
@media(min-width:1024px){.product-grid{grid-template-columns:repeat(4,1fr)}}
@media(min-width:1200px){.product-grid{grid-template-columns:repeat(5,1fr)}}
.product-card{background:var(--dark);border:1px solid transparent;border-radius:14px;padding:10px;display:flex;flex-direction:column;position:relative;transition:.3s;overflow:hidden}
.product-card:hover{border-color:rgba(225,29,72,.6);box-shadow:0 0 20px rgba(225,29,72,.15);transform:translateY(-3px)}
.product-card .discount-badge{position:absolute;top:14px;left:14px;z-index:2;background:var(--red);color:#fff;font-size:10px;font-weight:700;padding:2px 6px;border-radius:6px}
.product-card .card-heart{position:absolute;top:12px;right:12px;z-index:2;color:var(--text-muted);background:rgba(0,0,0,.35);border-radius:50%;width:30px;height:30px;display:flex;align-items:center;justify-content:center}
.product-card .card-heart:hover,.product-card .card-heart.active{color:var(--red)}
.product-card .card-heart.active svg{fill:var(--red)}
.product-card .card-img{aspect-ratio:1;background:#0f0f0f;border-radius:10px;overflow:hidden;margin-bottom:10px}
.product-card .card-img img{width:100%;height:100%;transition:.4s}
.product-card:hover .card-img img{transform:scale(1.06)}
.card-title{font-size:13px;font-weight:600;line-height:1.3;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.card-rating{display:flex;align-items:center;gap:4px;font-size:11px;color:var(--text-muted);margin:6px 0}
.card-rating svg{color:var(--yellow);width:12px;height:12px;fill:var(--yellow)}
.card-footer{display:flex;align-items:flex-end;justify-content:space-between;margin-top:auto;gap:6px}
.card-price{color:var(--red);font-weight:700;font-size:15px;line-height:1}
.card-old-price{color:var(--text-muted);font-size:11px;text-decoration:line-through;margin-top:4px}
.card-special{color:#fbbf24;font-size:10px;font-weight:600;margin-top:2px}
.card-add{background:rgba(225,29,72,.1);color:var(--red);padding:8px;border-radius:8px;transition:.2s;flex-shrink:0}
.card-add:hover{background:var(--red);color:#fff}

/* ============================================================
   5. HOME / HERO / SECTIONS
============================================================ */
.hero-slider{position:relative;border-radius:16px;overflow:hidden;margin-bottom:30px;background:var(--dark);border:1px solid var(--border);min-height:220px;aspect-ratio:16/7;max-height:420px}
@media(max-width:600px){.hero-slider{aspect-ratio:16/10;min-height:180px}}
.hero-slider-track{position:relative;width:100%;height:100%}.hero-swipe-hint{position:absolute;right:12px;bottom:12px;z-index:5;background:rgba(0,0,0,.55);color:#fff;border:1px solid rgba(255,255,255,.2);border-radius:20px;padding:5px 9px;font-size:10px;pointer-events:none}
.hero-slide{position:absolute;inset:0;opacity:0;transition:opacity .5s;pointer-events:none}
.hero-slide.active{opacity:1;pointer-events:auto}
.hero-slide img,.hero-slide video{width:100%;height:100%;object-fit:cover;display:block}.hero-slider{touch-action:pan-y;user-select:none}.hero-slide video{background:#000}
.hero-slide-overlay{position:absolute;inset:0;background:linear-gradient(90deg,rgba(0,0,0,.85) 0%,rgba(0,0,0,.35) 55%,transparent 100%);display:flex;align-items:center;padding:0 5%;color:#fff}
.hero-slide-content{max-width:520px}
.hero-slide-content h2{font-size:32px;font-weight:900;line-height:1.05;margin-bottom:8px;text-shadow:0 2px 8px rgba(0,0,0,.5)}
.hero-slide-content p{font-size:14px;color:#e5e5e5;margin-bottom:16px;max-width:420px;text-shadow:0 1px 4px rgba(0,0,0,.6)}
@media(min-width:768px){.hero-slide-content h2{font-size:42px}}
.hero-nav{position:absolute;top:50%;transform:translateY(-50%);width:40px;height:40px;border-radius:50%;background:rgba(0,0,0,.6);color:#fff;display:flex;align-items:center;justify-content:center;z-index:2;transition:.2s}
.hero-nav:hover{background:var(--red)}
.hero-nav.prev{left:12px}
.hero-nav.next{right:12px}
.hero-nav svg{width:20px;height:20px}
.hero-dots{position:absolute;bottom:14px;left:50%;transform:translateX(-50%);display:flex;gap:8px;z-index:2}
.hero-dot{width:8px;height:8px;border-radius:50%;background:rgba(255,255,255,.4);padding:0;transition:.2s}
.hero-dot.active{background:var(--red);width:24px;border-radius:4px}
.hero-banner{position:relative;border-radius:16px;overflow:hidden;margin-bottom:30px;background:#000;border:1px solid var(--border);min-height:220px;display:flex;align-items:center}
.hero-banner .hero-banner-img{width:100%;height:100%;min-height:220px;object-fit:cover;display:block}
@media(min-width:768px){.hero-banner,.hero-banner .hero-banner-img{min-height:320px}}
.section-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:16px;margin-top:30px;flex-wrap:wrap;gap:8px}
.section-header h3{font-size:20px;font-weight:800}
.section-header a{color:var(--red);font-size:13px;font-weight:600}
.categories-scroll{display:flex;gap:16px;overflow-x:auto;padding-bottom:10px;scrollbar-width:none}
.categories-scroll::-webkit-scrollbar{display:none}
.category-item{display:flex;flex-direction:column;align-items:center;gap:8px;min-width:76px}
.category-img{width:64px;height:64px;border-radius:50%;background:var(--dark-2);border:2px solid var(--border);display:flex;align-items:center;justify-content:center;overflow:hidden;transition:.2s}
.category-item:hover .category-img{border-color:var(--red);box-shadow:0 0 10px rgba(225,29,72,.5)}
.category-img img{width:100%;height:100%;object-fit:cover}
.category-item span{font-size:11px;color:var(--text-muted);text-align:center}


/* Google Drive link shown below the home navigation and above the hero banner */
.store-drive-link{
  margin:10px 0 18px;padding:12px 14px;
  border:1px solid rgba(225,29,72,.42);border-radius:12px;
  background:linear-gradient(135deg,rgba(225,29,72,.12),rgba(20,20,20,.96));
}
.store-drive-description{font-size:13px;color:var(--text);white-space:pre-wrap;overflow-wrap:anywhere;margin-bottom:8px}
.store-drive-anchor{
  display:inline-flex;align-items:center;gap:8px;max-width:100%;
  color:#fff;background:var(--red);padding:9px 13px;border-radius:9px;
  font-size:12px;font-weight:750;overflow-wrap:anywhere;
}
.store-drive-anchor:hover{background:var(--red-glow)}
.store-drive-anchor svg{width:15px;height:15px;flex:0 0 auto}

/* Offers strip */
.offers-strip{background:linear-gradient(135deg,rgba(225,29,72,.18),rgba(0,0,0,.4));border:1px solid rgba(225,29,72,.4);border-radius:16px;padding:14px 16px;margin:24px 0 8px;display:flex;align-items:center;justify-content:space-between;gap:10px;flex-wrap:wrap}
.offers-strip h3{font-size:18px;font-weight:800}
.offers-strip h3 span{color:var(--red)}
.offers-strip p{font-size:12px;color:var(--text-muted);margin-top:2px}

/* ============================================================
   6. SHOP / FILTERS
============================================================ */
.shop-layout{display:grid;grid-template-columns:1fr;gap:20px;padding:20px 0}
@media(min-width:900px){.shop-layout{grid-template-columns:260px 1fr}}
.filters{background:var(--dark);border:1px solid var(--border);border-radius:14px;padding:16px;height:fit-content;position:sticky;top:20px}
.filters h3{font-size:14px;margin-bottom:14px;display:flex;justify-content:space-between;align-items:center}
.filters h3 button{font-size:11px;color:var(--red)}
.filter-group{margin-bottom:16px;padding-bottom:16px;border-bottom:1px solid var(--border)}
.filter-group:last-child{border-bottom:none;margin-bottom:0;padding-bottom:0}
.filter-group h4{font-size:12px;color:var(--text-muted);text-transform:uppercase;letter-spacing:.5px;margin-bottom:8px}
.filter-group label{display:flex;align-items:center;gap:8px;font-size:13px;padding:5px 0;cursor:pointer}
.filter-group input[type=checkbox]{accent-color:var(--red);width:16px;height:16px}
.price-inputs{display:flex;gap:8px;margin-top:6px}
.price-inputs input{flex:1;background:var(--dark-2);border:1px solid var(--border);border-radius:8px;padding:8px;color:var(--text);font-size:12px;min-width:0}
.sort-bar{display:flex;justify-content:space-between;align-items:center;gap:8px;margin-bottom:14px;flex-wrap:wrap}
.sort-bar select{background:var(--dark-2);border:1px solid var(--border);border-radius:8px;padding:8px 12px;color:var(--text);font-size:13px}
.chips{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:12px}
.chip{background:rgba(225,29,72,.12);color:var(--red);font-size:11px;padding:4px 10px;border-radius:20px;display:inline-flex;align-items:center;gap:6px}
.chip button{color:var(--red);font-weight:bold;font-size:14px;line-height:1}
.mobile-filter-toggle{display:flex;justify-content:space-between;margin-bottom:12px}
@media(min-width:900px){.mobile-filter-toggle{display:none}}
.filters.mobile-closed{display:none}
@media(min-width:900px){.filters.mobile-closed{display:block}}

/* ============================================================
   7. PRODUCT DETAILS
============================================================ */
#page-product{padding:20px 0 60px}
.breadcrumb{font-size:11px;color:var(--text-muted);display:flex;align-items:center;gap:6px;margin-bottom:16px;flex-wrap:wrap}
.breadcrumb a:hover{color:var(--red)}
.breadcrumb span:last-child{color:var(--text)}
.product-layout{display:grid;grid-template-columns:1fr;gap:24px}
@media(min-width:992px){.product-layout{grid-template-columns:1fr 1fr}}
@media(min-width:1200px){.product-layout{grid-template-columns:5fr 4fr 3fr}}
.gallery-main{background:var(--dark);border-radius:16px;aspect-ratio:1;position:relative;display:flex;align-items:center;justify-content:center;overflow:hidden;padding:20px;border:1px solid var(--border);cursor:zoom-in}
.gallery-main img{max-width:90%;max-height:90%;border-radius:10px;transition:transform .3s}
.gallery-main:hover img{transform:scale(1.08)}
.gallery-thumbs{display:flex;gap:10px;margin-top:12px;justify-content:center;flex-wrap:wrap}
.thumb{width:60px;height:60px;border-radius:8px;overflow:hidden;border:2px solid transparent;background:var(--dark);cursor:pointer;padding:0}
.thumb img{width:100%;height:100%}
.thumb.active{border-color:var(--red)}
.product-info h1{font-size:22px;font-weight:700;margin-bottom:8px;line-height:1.2}
.rating-row{display:flex;align-items:center;gap:12px;font-size:12px;color:var(--text-muted);flex-wrap:wrap;margin-bottom:16px}
.rating-row svg{width:14px;height:14px;fill:var(--yellow);color:var(--yellow)}
.genz-choice{display:inline-block;background:var(--red);color:#fff;font-size:10px;font-weight:700;padding:3px 10px;border-radius:20px;margin-bottom:12px}
.features-list{display:flex;flex-direction:column;gap:6px;margin-bottom:16px}
.features-list li{display:flex;align-items:center;gap:8px;font-size:12px;color:#d4d4d8}
.features-list svg{width:14px;height:14px;color:var(--red);flex-shrink:0}
.price-row{display:flex;align-items:flex-end;gap:10px;margin-bottom:12px;flex-wrap:wrap}
.price-main{font-size:30px;font-weight:800;color:var(--red);line-height:1}
.price-old{font-size:14px;color:var(--text-muted);text-decoration:line-through;margin-bottom:4px}
.price-discount{background:rgba(225,29,72,.15);color:var(--red);padding:3px 8px;border-radius:6px;font-size:11px;font-weight:600;margin-bottom:4px}
.price-special{background:rgba(251,191,36,.15);color:#fbbf24;padding:3px 8px;border-radius:6px;font-size:11px;font-weight:600;margin-bottom:4px}
.color-picker{margin-bottom:16px}
.color-picker p{font-size:12px;color:var(--text-muted);margin-bottom:6px}
.color-picker p span{color:var(--text);font-weight:600}
.colors{display:flex;gap:8px;flex-wrap:wrap}
.color-dot{width:32px;height:32px;border-radius:50%;border:2px solid var(--border);transition:.2s;cursor:pointer}
.color-dot.active{border-color:var(--red);transform:scale(1.15);box-shadow:0 0 10px rgba(225,29,72,.6)}
.qty-row{display:flex;align-items:center;gap:12px;flex-wrap:wrap;margin-bottom:16px}
.qty-row label{font-size:12px;color:var(--text-muted)}
.qty-ctrl{display:flex;align-items:center;border:1px solid var(--border);border-radius:8px;overflow:hidden}
.qty-ctrl button{padding:6px 12px;color:var(--text);background:var(--dark-2);font-weight:700;font-size:16px}
.qty-ctrl button:hover:not(:disabled){background:var(--red)}
.qty-ctrl button:disabled{opacity:.35;cursor:not-allowed}
.qty-ctrl span{padding:6px 14px;font-weight:600;font-size:14px;min-width:36px;text-align:center}
.stock-tag{color:var(--green);font-size:12px;display:flex;align-items:center;gap:4px}
.stock-tag.out{color:#f87171}
.stock-tag svg{width:14px;height:14px}
.checkout-card{background:var(--dark);border:1px solid var(--border);border-radius:16px;padding:16px;display:flex;flex-direction:column;gap:14px;height:fit-content}
.checkout-card hr{border:none;border-top:1px solid var(--border)}
.ship-row{display:flex;justify-content:space-between;align-items:center;font-size:12px;color:var(--text-muted);gap:8px}
.delivery-info{display:flex;gap:10px;align-items:flex-start}
.delivery-info>svg{width:16px;height:16px;color:var(--text-muted);flex-shrink:0;margin-top:2px}
.delivery-info .title{font-size:13px;font-weight:600;color:var(--text)}
.delivery-info .sub{font-size:11px;color:var(--text-muted)}
.product-tabs-section{margin-top:30px;background:var(--dark);border-radius:16px;padding:16px}
.tabs-header{display:flex;gap:20px;border-bottom:1px solid var(--border);margin-bottom:20px;overflow-x:auto}
.tab-item{padding:10px 0;font-size:14px;font-weight:500;color:var(--text-muted);border-bottom:2px solid transparent;transition:.2s;white-space:nowrap;cursor:pointer;background:none}
.tab-item.active{color:var(--red);border-bottom-color:var(--red)}
.tab-pane{display:none}
.tab-pane.active{display:block}
.highlights-grid{display:grid;grid-template-columns:1fr;gap:20px}
@media(min-width:768px){.highlights-grid{grid-template-columns:1fr 1fr 1fr}}
.highlights-banner{background:linear-gradient(135deg,#000 0%,#1a0505 100%);border-radius:12px;padding:20px;position:relative;overflow:hidden;display:flex;flex-direction:column;justify-content:center;min-height:160px}
.highlights-banner::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,transparent 30%,rgba(225,29,72,.5) 100%)}
.highlights-banner>*{position:relative;z-index:1}
.highlights-banner h3{font-size:20px;font-weight:900;margin-bottom:4px}
.highlights-banner h3 span{color:var(--red);font-style:italic;font-size:28px;display:block}
.highlights-banner p{font-size:12px;color:var(--text-muted)}
.highlights-list div{display:flex;align-items:center;gap:8px;font-size:12px;color:#d4d4d8;margin-bottom:8px}
.highlights-list svg{width:14px;height:14px;color:var(--red)}
.review-summary h3{font-size:20px;font-weight:800;margin-bottom:4px}
.review-summary .big-rating{display:flex;align-items:center;gap:10px;margin-bottom:6px}
.review-summary .big-rating .score{font-size:36px;font-weight:900;color:var(--red)}
.review-summary .stars svg{width:16px;height:16px;color:var(--yellow);fill:var(--yellow)}
.review-summary p{font-size:11px;color:var(--text-muted);margin-bottom:12px}
.review-card{background:var(--dark-2);border:1px solid var(--border);border-radius:12px;padding:12px;margin-bottom:10px}
.review-card .head{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:8px;gap:8px}
.review-card .user{display:flex;align-items:center;gap:10px}
.review-card .avatar{width:32px;height:32px;border-radius:50%;background:var(--red);display:flex;align-items:center;justify-content:center;font-weight:700;font-size:12px;flex-shrink:0}
.review-card .name{font-size:12px;font-weight:600}
.review-card .verified{color:var(--green);font-size:10px;display:flex;align-items:center;gap:3px}
.review-card .verified svg{width:10px;height:10px}
.review-card .r-stars svg{width:12px;height:12px;color:var(--yellow);fill:var(--yellow)}
.review-card p{font-size:12px;color:#d4d4d8;margin-bottom:6px}
.review-card .r-date{font-size:10px;color:var(--text-muted)}

/* ============================================================
   8. CART / CHECKOUT / ORDERS / ACCOUNT
============================================================ */
.page-card{background:var(--dark);border:1px solid var(--border);border-radius:16px;padding:20px;margin:20px 0}
.page-title{font-size:24px;font-weight:800;margin:16px 0}
.cart-layout{display:grid;grid-template-columns:1fr;gap:20px}
@media(min-width:900px){.cart-layout{grid-template-columns:1fr 380px}}
.cart-item{display:grid;grid-template-columns:80px 1fr auto;gap:12px;padding:14px 0;border-bottom:1px solid var(--border);align-items:center}
.cart-item:last-child{border-bottom:none}
.cart-item img{width:80px;height:80px;border-radius:10px;background:var(--dark-2)}
.cart-item .info h4{font-size:14px;font-weight:600;margin-bottom:4px;line-height:1.3}
.cart-item .info .variant{font-size:11px;color:var(--text-muted);margin-bottom:6px}
.cart-item .info .price{color:var(--red);font-weight:700;font-size:14px}
.cart-item .actions{display:flex;flex-direction:column;align-items:flex-end;gap:8px}
.qty-ctrl.sm button{padding:3px 9px;font-size:13px}
.qty-ctrl.sm span{padding:3px 10px;font-size:12px}
.summary-card{background:var(--dark);border:1px solid var(--border);border-radius:16px;padding:20px;height:fit-content;position:sticky;top:20px}
.summary-card h3{font-size:16px;margin-bottom:14px}
.summary-row{display:flex;justify-content:space-between;font-size:13px;padding:6px 0;color:var(--text-muted)}
.summary-row.total{font-size:16px;font-weight:800;color:var(--text);border-top:1px solid var(--border);margin-top:8px;padding-top:12px}
.summary-row.total .val{color:var(--red)}
.summary-row.discount{color:#fbbf24}
.success-card{text-align:center;padding:40px 20px;background:var(--dark);border:1px solid var(--border);border-radius:16px;margin:30px 0}
.success-card .check{width:80px;height:80px;border-radius:50%;background:rgba(34,197,94,.15);color:var(--green);display:flex;align-items:center;justify-content:center;margin:0 auto 20px}
.success-card .check svg{width:44px;height:44px}
.success-card h1{font-size:26px;margin-bottom:8px}
.order-card{background:var(--dark);border:1px solid var(--border);border-radius:14px;padding:16px;margin-bottom:14px}
.order-card .head{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:12px;gap:8px;flex-wrap:wrap}
.order-card .head h4{font-size:14px;font-weight:700}
.order-card .head .date{font-size:11px;color:var(--text-muted)}
.status-pill{padding:3px 10px;border-radius:20px;font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:.5px}
.status-pill.placed,.status-pill.confirmed,.status-pill.processing{background:rgba(250,204,21,.15);color:var(--yellow)}
.status-pill.shipped,.status-pill.out-for-delivery{background:rgba(59,130,246,.15);color:#60a5fa}
.status-pill.delivered{background:rgba(34,197,94,.15);color:var(--green)}
.status-pill.cancelled,.status-pill.refunded{background:rgba(248,113,113,.15);color:#f87171}
.timeline{display:flex;flex-direction:column;gap:0;margin:16px 0}
.timeline-step{display:flex;gap:12px;position:relative;padding-bottom:20px}
.timeline-step:last-child{padding-bottom:0}
.timeline-step::before{content:'';position:absolute;left:11px;top:24px;bottom:0;width:2px;background:var(--border)}
.timeline-step:last-child::before{display:none}
.timeline-step.done::before{background:var(--green)}
.timeline-step .dot{width:24px;height:24px;border-radius:50%;background:var(--dark-2);border:2px solid var(--border);display:flex;align-items:center;justify-content:center;flex-shrink:0;z-index:1}
.timeline-step.done .dot{background:var(--green);border-color:var(--green);color:#fff}
.timeline-step.done .dot svg{width:12px;height:12px}
.timeline-step .label{font-size:13px;font-weight:600}
.timeline-step .time{font-size:11px;color:var(--text-muted)}
.auth-card{max-width:440px;margin:40px auto;background:var(--dark);border:1px solid var(--border);border-radius:16px;padding:28px}
.auth-card h1{font-size:22px;margin-bottom:8px;text-align:center}
.auth-card p.sub{text-align:center;color:var(--text-muted);font-size:13px;margin-bottom:20px}
.error-banner{background:rgba(248,113,113,.1);border:1px solid rgba(248,113,113,.3);color:#f87171;padding:10px 14px;border-radius:10px;font-size:12px;margin-bottom:16px;display:flex;gap:8px;align-items:flex-start}
.error-banner svg{flex-shrink:0;width:16px;height:16px;margin-top:1px}
.addr-list{display:grid;grid-template-columns:1fr;gap:12px;margin-top:12px}
@media(min-width:600px){.addr-list{grid-template-columns:1fr 1fr}}
.addr-card{background:var(--dark-2);border:1px solid var(--border);border-radius:12px;padding:14px;position:relative}
.addr-card.default{border-color:var(--red)}
.addr-card .badge-default{position:absolute;top:10px;right:10px;background:var(--red);color:#fff;font-size:9px;font-weight:700;padding:2px 8px;border-radius:20px}
.addr-card p{font-size:13px;margin-bottom:3px}
.addr-card .muted{color:var(--text-muted);font-size:11px}
.addr-card .actions{display:flex;gap:8px;margin-top:10px}
.notif-item{display:flex;gap:12px;padding:14px;background:var(--dark-2);border-radius:12px;margin-bottom:10px;border-left:3px solid var(--red)}
.notif-item.read{opacity:.6;border-left-color:var(--gray)}
.notif-item .icon{width:36px;height:36px;border-radius:50%;background:rgba(225,29,72,.15);color:var(--red);display:flex;align-items:center;justify-content:center;flex-shrink:0}
.notif-item .icon svg{width:18px;height:18px}
.notif-item h4{font-size:13px;margin-bottom:2px}
.notif-item p{font-size:12px;color:var(--text-muted)}
.notif-item .time{font-size:10px;color:var(--text-muted);margin-top:4px}
.policy-content h2{font-size:20px;margin:24px 0 10px}
.policy-content h3{font-size:15px;margin:16px 0 8px;color:var(--red)}
.policy-content p{font-size:13px;color:var(--text-muted);margin-bottom:10px;line-height:1.7}
.site-footer{background:var(--dark);border-top:1px solid var(--border);margin-top:60px;padding:32px 0 16px}
.footer-grid{display:grid;grid-template-columns:1fr;gap:24px}
@media(min-width:768px){.footer-grid{grid-template-columns:repeat(4,1fr)}}
.footer-grid h3{font-size:12px;text-transform:uppercase;letter-spacing:1px;color:var(--text-muted);margin-bottom:10px}
.footer-grid a{display:block;font-size:13px;padding:4px 0;color:var(--text)}
.footer-grid a:hover{color:var(--red)}
.footer-bottom{border-top:1px solid var(--border);margin-top:24px;padding-top:16px;display:flex;flex-wrap:wrap;gap:8px;justify-content:space-between;font-size:11px;color:var(--text-muted)}
.offline-banner{background:#7f1d1d;color:#fff;padding:8px 16px;text-align:center;font-size:12px;display:none}
body.offline .offline-banner{display:block}

/* ===== MAP ===== */
.map-wrap{position:relative;width:100%;height:280px;border-radius:12px;overflow:hidden;border:1px solid var(--border);margin-top:8px;background:var(--dark-2)}
.map-wrap #map{width:100%;height:100%}
.map-hint{position:absolute;top:8px;left:8px;right:8px;background:rgba(0,0,0,.7);color:#fff;padding:8px 12px;border-radius:8px;font-size:11px;z-index:2;pointer-events:none;text-align:center}
.map-fallback{display:flex;align-items:center;justify-content:center;height:100%;color:var(--text-muted);font-size:12px;padding:20px;text-align:center}
.map-error{color:#f87171}

/* ===== VIDEO MODAL ===== */
.video-modal{position:fixed;inset:0;background:rgba(0,0,0,.9);z-index:9999;display:none;align-items:center;justify-content:center;padding:20px}
.video-modal.show{display:flex}
.video-modal video{max-width:100%;max-height:90vh;border-radius:12px;box-shadow:0 10px 40px rgba(0,0,0,.5)}
.video-close{position:absolute;top:20px;right:20px;color:#fff;background:rgba(255,255,255,.2);border-radius:50%;width:44px;height:44px;display:flex;align-items:center;justify-content:center;cursor:pointer}
.video-close:hover{background:rgba(255,255,255,.4)}

/* ===== FULLSCREEN IMAGE VIEWER ===== */
.image-viewer{position:fixed;inset:0;background:rgba(0,0,0,.95);z-index:9999;display:none;align-items:center;justify-content:center;padding:20px}
.image-viewer.show{display:flex}
.image-viewer img{max-width:95vw;max-height:92vh;border-radius:10px;box-shadow:0 10px 40px rgba(0,0,0,.6)}
.image-viewer .close{position:absolute;top:20px;right:20px;color:#fff;background:rgba(255,255,255,.2);border-radius:50%;width:44px;height:44px;display:flex;align-items:center;justify-content:center;cursor:pointer}

/* ============================================================
   BACKGROUND
============================================================ */
body{background-color:#0a0a0a;background-image:url('red-background.png');background-size:cover;background-position:center;background-attachment:scroll;background-repeat:no-repeat}
body::before{content:'';position:fixed;inset:0;background:rgba(0,0,0,.55);pointer-events:none;z-index:0}
main#app-content,footer.site-footer,.toast-container{position:relative;z-index:1}
.product-card,.page-card,.summary-card,.auth-card,.order-card,.filters,.checkout-card,.site-footer,.home-header,.home-nav{background-color:rgba(20,20,20,.97)}
/* Keep compositing inexpensive on Android/WebView: no per-card backdrop blur. */
.product-card,.page-card,.summary-card,.auth-card,.order-card,.filters,.checkout-card,.site-footer,.home-header,.home-nav{
  -webkit-backdrop-filter:none;
  backdrop-filter:none;
}
.home-header,.home-nav{background-color:rgba(20,20,20,.97)}
.site-footer{background-color:rgba(20,20,20,.95)}

@media (max-width:767px){
  .product-card,.page-card,.summary-card,.auth-card,.order-card,.filters,.checkout-card,
  .site-footer,.home-header,.home-nav,nav.mobile-bottom-bar{
    backdrop-filter:none !important;
    -webkit-backdrop-filter:none !important;
  }
  main#app-content{padding-bottom:calc(var(--mobile-nav-h) + var(--safe-bottom) + 24px)}
  .site-footer{padding-bottom:calc(var(--mobile-nav-h) + var(--safe-bottom) + 16px)}
}
</style>
</head>
<body>

<div class="offline-banner">⚠ You are offline. Some features may not work.</div>

<!-- Top bar (desktop only, shown on ALL pages as informational) -->
<div class="top-bar"><div class="container top-bar-inner">
  <span><i data-lucide="zap"></i> Free Delivery Over Rs. 5,000</span>
  <span><i data-lucide="refresh-ccw"></i> 7-Day Easy Returns</span>
  <span><i data-lucide="wallet"></i> Cash on Delivery</span>
  <span><i data-lucide="headphones"></i> 24/7 Support</span>
</div></div>

<!-- The dashboard header is rendered by JS inside #app-content, ONLY on Home. -->
<main id="app-content" class="container" aria-live="polite"></main>

<footer class="site-footer">
  <div class="container footer-grid">
    <div>
      <div class="logo">
        <svg class="logo-svg" viewBox="0 0 220 60" xmlns="http://www.w3.org/2000/svg" aria-label="GEN Z logo">
          <defs>
            <linearGradient id="lg" x1="0" y1="0" x2="1" y2="0">
              <stop offset="0" stop-color="#e11d48"/>
              <stop offset="1" stop-color="#ff2a4b"/>
            </linearGradient>
          </defs>
          <text x="0" y="42" font-family="Inter,system-ui,sans-serif" font-weight="900" font-style="italic" font-size="40" fill="url(#lg)" letter-spacing="-2">GEN Z</text>
          <rect x="0" y="48" width="220" height="3" fill="url(#lg)"/>
        </svg>
        <p>Shop Your Vibe</p>
      </div>
      <p class="text-muted text-sm" style="margin-top:8px">Bold, fast, and made for you. Cash on delivery across Pakistan.</p>
    </div>
    <div><h3>Shop</h3><a href="#/shop">All Products</a><a href="#/category/all">Categories</a><a href="#/shop?sort=discount">Sale</a></div>
    <div><h3>Help</h3><a href="#/support">Contact Us</a><a href="#/support">FAQs</a><a href="#/chat">Chat with Us</a><a href="#/support">Shipping</a><a href="#/support">Returns</a></div>
    <div><h3>Legal</h3><a href="#/support">Privacy</a><a href="#/support">Terms</a></div>
  </div>
  <div class="container footer-bottom">
    <span>© <span id="year"></span> GEN Z. All rights reserved.</span>
    <span class="text-muted">Powered by Firebase · © <span id="year2"></span></span>
  </div>
</footer>

<nav class="mobile-bottom-bar" aria-label="Mobile">
  <a href="#/" data-nav="home"><i data-lucide="home"></i>Home</a>
  <a href="#/shop" data-nav="shop"><i data-lucide="layout-grid"></i>Shop</a>
  <a href="#/search"><i data-lucide="search"></i>Search</a>
  <a href="#/cart" data-nav="cart"><i data-lucide="shopping-cart"></i>Cart</a>
  <a href="#/account" data-nav="account"><i data-lucide="user"></i>Account</a>
</nav>

<div id="toastContainer" class="toast-container" aria-live="polite"></div>

<!-- Video Modal -->
<div class="video-modal" id="videoModal" onclick="if(event.target.id==='videoModal')App.closeVideo()">
  <div class="video-close" onclick="App.closeVideo()"><i data-lucide="x"></i></div>
  <video id="videoPlayer" controls></video>
</div>

<!-- Fullscreen Image Viewer -->
<div class="image-viewer" id="imageViewer" onclick="if(event.target.id==='imageViewer')App.closeImageViewer()">
  <div class="close" onclick="App.closeImageViewer()"><i data-lucide="x"></i></div>
  <img id="imageViewerImg" alt="Full-size product image">
</div>

<script>
/* ---------- MAPTILER + LEAFLET LOADER ---------- */
window.MAPTILER_KEY = "qdvkHVwEbMok4wj1LAPF"; // your MapTiler key
window.__leafletLoading = false;
window.loadLeaflet = function() {
  return new Promise((resolve, reject) => {
    if (window.L) { resolve(); return; }
    if (window.__leafletLoading) {
      const check = setInterval(() => {
        if (window.L) { clearInterval(check); resolve(); }
      }, 100);
      return;
    }
    window.__leafletLoading = true;
    const s = document.createElement('script');
    s.src = "https://unpkg.com/leaflet@1.9.4/dist/leaflet.js";
    s.integrity = "sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo=";
    s.crossOrigin = "";
    s.async = true;
    s.onload = () => { window.__leafletLoading = false; resolve(); };
    s.onerror = () => { window.__leafletLoading = false; reject(new Error('Leaflet failed to load')); };
    document.head.appendChild(s);
  });
};
</script>
<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import {
  getDatabase, ref, get, set, update, push, remove, onValue, query, orderByChild, equalTo, runTransaction
} from "https://www.gstatic.com/firebasejs/10.12.0/firebase-database.js";
import { getAuth, onAuthStateChanged, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, sendPasswordResetEmail, updateProfile } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-auth.js";
import { getStorage, ref as storageRef, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-storage.js";

// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: "AIzaSyDGBZZk_SxIWjqRC4fcrLIkS1Yy9W4xkIo",
  authDomain: "generate-gen-z.firebaseapp.com",
  projectId: "generate-gen-z",
  storageBucket: "generate-gen-z.firebasestorage.app",
  messagingSenderId: "870044313041",
  appId: "1:870044313041:web:3ca635f9ed9d7054d62cf0",
  measurementId: "G-1W31NSFX4P"
};
const app = initializeApp(firebaseConfig);
const db = getDatabase(app);
const auth = getAuth(app);
const firebaseStorage = getStorage(app);



const ENV = { STORE: { currency:"PKR", deliveryFee:250, freeDeliveryThreshold:999999, codEnabled:true } };

// Guest identity is browser-local convenience only; it is not authentication.
function getGuestId(){
  let id="";
  try{id=localStorage.getItem("genz:guestId")||"";}catch{}
  if(!id){
    id="guest_"+(window.crypto?.randomUUID?crypto.randomUUID().replace(/-/g,""):(Date.now().toString(36)+Math.random().toString(36).slice(2,12)));
    try{localStorage.setItem("genz:guestId",id);}catch{}
  }
  return id;
}
const guestId=getGuestId();
const State = {
  user:{uid:guestId,email:"",isGuest:true}, userProfile:null, authReady:false,
  products:[], categories:[], banners:[], discounts:[], cart:[], wishlist:[],
  orders:[], addresses:[], notifications:[], myReviews:[], recentlyViewed:[],
  appDownloads:[], appDownloadsReady:false,
  settings:{}, ready:false, authReady:false, productsReady:false, backgroundUrl:null, placingOrder:false
};

const Storage = {
  get(k,f){ try{ const v=localStorage.getItem('genz:'+k); return v?JSON.parse(v):f; }catch{ return f; } },
  set(k,v){ try{ localStorage.setItem('genz:'+k,JSON.stringify(v)); }catch{} },
  remove(k){ try{ localStorage.removeItem('genz:'+k); }catch{} }
};
State.cart = Storage.get('cart', []);
State.wishlist = Storage.get('wishlist', []);
State.recentlyViewed = Storage.get('recentlyViewed', []);
let persistLocalTimer = null;
function flushPersistLocal(){
  if(persistLocalTimer){ clearTimeout(persistLocalTimer); persistLocalTimer=null; }
  Storage.set('cart',State.cart);
  Storage.set('wishlist',State.wishlist);
  Storage.set('recentlyViewed',State.recentlyViewed);
}
function persistLocal(){
  if(persistLocalTimer) clearTimeout(persistLocalTimer);
  persistLocalTimer=setTimeout(flushPersistLocal,180);
}
window.addEventListener('pagehide',flushPersistLocal);

function fmt(n){ return 'Rs. '+Number(n||0).toLocaleString('en-PK'); }
function escapeHtml(s){ if(s==null) return ''; return String(s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])); }
function getProduct(id){ return State.products.find(p=>String(p.id)===String(id)); }
function toast(msg,type){
  const c=document.getElementById('toastContainer');
  if(!c){ console.warn(String(msg||'')); return; }
  const el=document.createElement('div'); el.className='toast '+(type||''); el.textContent=String(msg??'');
  c.appendChild(el);
  setTimeout(()=>{el.style.opacity='0';el.style.transform='translateY(8px)';},2000);
  setTimeout(()=>el.remove(),2400);
}
function formValue(form,name){return form?.elements?.namedItem(name)?.value??'';}
function cleanForFirebase(value){
  if(value===undefined)return null;
  if(value===null||typeof value!=='object')return value;
  if(Array.isArray(value))return value.map(v=>v===undefined?null:cleanForFirebase(v));
  const out={};
  Object.keys(value).forEach(k=>{if(value[k]!==undefined)out[k]=cleanForFirebase(value[k]);});
  return out;
}
function mergeCartItems(primary,secondary){
  const result=[];
  const add=item=>{if(!item||item.productId==null)return;const qty=Math.max(1,Number(item.qty)||1);const color=item.color??null;const found=result.find(x=>String(x.productId)===String(item.productId)&&(x.color??null)===(color??null));if(found)found.qty+=qty;else result.push({productId:item.productId,qty,color});};
  (Array.isArray(primary)?primary:[]).forEach(add);(Array.isArray(secondary)?secondary:[]).forEach(add);return result;
}
function authErrorMessage(err){
  const code=String(err?.code||'');
  const messages={
    'auth/email-already-in-use':'This email already has an account. Please sign in.',
    'auth/invalid-email':'Please enter a valid email address.',
    'auth/weak-password':'Choose a stronger password with at least 6 characters.',
    'auth/user-not-found':'No account was found for this email.',
    'auth/wrong-password':'Incorrect email or password.',
    'auth/invalid-credential':'Incorrect email or password.',
    'auth/too-many-requests':'Too many attempts. Please wait and try again.',
    'auth/network-request-failed':'Network error. Check your internet connection.',
    'auth/operation-not-allowed':'Email/Password sign-in is not enabled in Firebase Console.',
    'auth/invalid-api-key':'Firebase API key is invalid. Check firebaseConfig.',
    'auth/app-not-authorized':'This domain is not authorized in Firebase Authentication settings.',
    'auth/unauthorized-domain':'Add this website domain in Firebase Authentication > Settings > Authorized domains.'
  };
  return messages[code]||err?.message||'Authentication failed. Please try again.';
}
let iconRefreshFrame=0;
function refreshIcons(){
  if(iconRefreshFrame) cancelAnimationFrame(iconRefreshFrame);
  iconRefreshFrame=requestAnimationFrame(()=>{
    iconRefreshFrame=0;
    if(window.lucide&&window.lucide.createIcons) window.lucide.createIcons();
  });
}
function updateBadges(){
  const q=State.cart.reduce((a,b)=>a+b.qty,0);
  const cb=document.getElementById('cartBadge'); if(cb) cb.textContent=q;
  const wb=document.getElementById('wishlistBadge'); if(wb) wb.textContent=State.wishlist.length;
}

/* ---------- PRICING / ADMIN-LINKED DISCOUNTS ---------- */
function activeOfferForProduct(productId){
  const t=Date.now();
  return (State.discounts||[]).find(o=>String(o.productId)===String(productId)&&!o.paused&&(!Number(o.startAt)||t>=Number(o.startAt))&&(!Number(o.endAt)||t<Number(o.endAt))&&Number(o.finalPrice)>0)||null;
}
function effectivePrice(p){
  if(!p)return 0;
  const offer=activeOfferForProduct(p.id);
  if(offer)return Number(offer.finalPrice);
  if(p.specialPrice&&Number(p.specialPrice)>0&&Number(p.specialPrice)<Number(p.price))return Number(p.specialPrice);
  return Number(p.price||0);
}
function discountPercent(p){
  const offer=p?activeOfferForProduct(p.id):null;
  if(offer)return Number(offer.percent)||Math.round(((Number(offer.originalPrice)-Number(offer.finalPrice))/Math.max(1,Number(offer.originalPrice)))*100);
  const ep=effectivePrice(p), base=Number(p?.oldPrice)>Number(p?.price)?Number(p.oldPrice):Number(p?.price);
  if(base>0&&ep<base)return Math.round(((base-ep)/base)*100);
  return Number(p?.discount)||0;
}
function hasActiveDiscount(p){return discountPercent(p)>0;}

/* ---------- CART ---------- */
function addToCart(pid, qty, color){
  const p = getProduct(pid);
  if(!p){ toast('Product unavailable','error'); return false; }
  if(p.stock<=0){ toast('Out of stock','error'); return false; }
  qty = Math.max(1, Math.min(qty||1, p.stock));
  const colorKey = color || (p.colors&&p.colors[0]) || null;
  const ex = State.cart.find(it=>String(it.productId)===String(p.id)&&it.color===colorKey);
  if(ex){ ex.qty = Math.min(ex.qty+qty, p.stock); }
  else { State.cart.push({productId:p.id, qty, color:colorKey}); }
  persistLocal(); updateBadges();
  return true;
}
function removeFromCart(pid, color){
  State.cart = State.cart.filter(it=>!(String(it.productId)===String(pid)&&it.color===color));
  persistLocal(); updateBadges();
}
function updateCartQty(pid, color, delta){
  const it = State.cart.find(x=>String(x.productId)===String(pid)&&x.color===color);
  if(!it) return;
  const p = getProduct(pid);
  it.qty = Math.max(1, Math.min(it.qty+delta, p?p.stock:1));
  persistLocal(); updateBadges();
}
function cartSubtotal(){ // discounted subtotal
  return State.cart.reduce((s,it)=>{
    const p = getProduct(it.productId);
    return s + (p ? effectivePrice(p)*it.qty : 0);
  },0);
}
function cartOriginalSubtotal(){
  return State.cart.reduce((s,it)=>{
    const p = getProduct(it.productId);
    return s + (p ? Number(p.price||0)*it.qty : 0);
  },0);
}
function cartDiscount(){ return Math.max(0, cartOriginalSubtotal() - cartSubtotal()); }
function cartDelivery(){
  const sub = cartSubtotal();
  if(sub===0) return 0;
  const fee=Number(State.settings?.deliveryFee);
  const threshold=Number(State.settings?.freeDeliveryThreshold);
  return Number.isFinite(threshold)&&threshold>0&&sub>=threshold?0:(Number.isFinite(fee)?fee:ENV.STORE.deliveryFee);
}
function cartTotal(){ return cartSubtotal() + cartDelivery(); }

/* ---------- WISHLIST ---------- */
async function toggleWishlist(pid){
  const i = State.wishlist.indexOf(pid);
  if(i>=0){ State.wishlist.splice(i,1); toast('Removed from wishlist','warn'); }
  else { State.wishlist.push(pid); toast('Added to wishlist','success'); }
  persistLocal(); updateBadges();
  if(State.user&&!State.user.isGuest){ try{ await set(ref(db,'users/'+State.user.uid+'/wishlist'), State.wishlist); }catch{} }
  return i<0;
}
function isWishlisted(id){ return State.wishlist.includes(id); }

/* ---------- DATA LOADERS ---------- */
function mapProduct(k, p){
  return {
    // Keep the real Realtime Database child key separately from the public/UI id.
    // Stock transactions must always target the actual /products/<database-key> path.
    _dbKey: String(k),
    id: p.id || k,
    title: p.title || 'Untitled',
    price: Number(p.price)||0,
    oldPrice: Number(p.oldPrice)||0,
    specialPrice: Number(p.specialPrice)||0,
    rating: Number(p.rating)||0,
    reviews: String(p.reviews||'0'),
    discount: Number(p.discount)||0,
    image: p.image||'',
    images: p.images||[p.image].filter(Boolean),
    video: p.video || '',
    category: p.category||'all',
    categoryName: p.categoryName||p.category||'All',
    brand: p.brand||'GEN Z',
    stock: Number(p.stock)||0,
    colors: Array.isArray(p.colors)?p.colors:(p.colors?Object.values(p.colors):[]),
    features: Array.isArray(p.features)?p.features:(p.features?Object.values(p.features):[]),
    description: p.description||'',
    shortDescription:p.shortDescription||'',
    sizes:Array.isArray(p.sizes)?p.sizes:(p.sizes?Object.values(p.sizes):[]),
    tags:Array.isArray(p.tags)?p.tags:(p.tags?Object.values(p.tags):[]),
    sku:p.sku||'', status:p.status||'active',
    lowStockThreshold:Number(p.lowStockThreshold)||5,
    packageWeight:p.packageWeight||null, warranty:p.warranty||'',
    packageIncludes:p.packageIncludes||'', createdAt:p.createdAt||0
  };
}
async function loadProducts(){
  try{
    const snap = await get(ref(db,'products'));
    State.products = snap.exists() ? Object.keys(snap.val()).map(k=>mapProduct(k, snap.val()[k])).filter(p=>!['inactive','hidden','draft'].includes(String(p.status||'active').toLowerCase())) : [];
  }catch(e){ console.warn('loadProducts',e); State.products=[]; }
}
async function loadCategories(){
  try{
    const snap = await get(ref(db,'categories'));
    State.categories = snap.exists() ? Object.keys(snap.val()).map(k=>({slug:k,name:snap.val()[k].name||k,img:snap.val()[k].img||''})) : [];
  }catch{ State.categories=[]; }
}
function bannerIsActive(b){
  const t=Date.now();
  return b.active!==false&&(!Number(b.startAt)||t>=Number(b.startAt))&&(!Number(b.endAt)||t<Number(b.endAt));
}
async function loadBanners(){
  try{
    const snap=await get(ref(db,'banners'));
    State.banners=snap.exists()?Object.keys(snap.val()).map(k=>({id:k,...snap.val()[k]})).filter(bannerIsActive).sort((a,b)=>(a.order||0)-(b.order||0)):[];
  }catch{State.banners=[];}
}
async function loadDiscounts(){
  try{const snap=await get(ref(db,'discounts'));State.discounts=snap.exists()?Object.keys(snap.val()).map(k=>({id:k,...snap.val()[k]})):[];}
  catch{State.discounts=[];}
}
async function loadSettings(){
  try{
    const snap = await get(ref(db,'settings/store'));
    State.settings = snap.exists() ? snap.val() : {};
    ENV.STORE.deliveryFee=Number(State.settings.deliveryFee??250);
    ENV.STORE.freeDeliveryThreshold=Number(State.settings.freeDeliveryThreshold??999999);
    ENV.STORE.codEnabled=State.settings.codEnabled!==false;
  }catch{ State.settings={}; }
}
async function loadBackground(){
  try{
    const snap=await get(ref(db,'settings/background'));
    applyBackground(snap.exists()&&snap.val().url?snap.val().url:null);
  }catch(err){
    console.warn('loadBackground',err);
    applyBackground(null);
  }
}
async function loadUserData(uid){
  // Load each user-data area independently. A missing RTDB index or a
  // permission issue for one area must not prevent the other areas loading.
  try{
    const profSnap=await get(ref(db,'users/'+uid));
    const saved=profSnap.exists()?(profSnap.val()||{}):{};
    State.userProfile={name:saved.name||'',phone:saved.phone||'',email:saved.email||uid};
    State.addresses=saved.addresses&&typeof saved.addresses==='object'
      ?Object.keys(saved.addresses).map(k=>({id:k,...saved.addresses[k]})):[];
    if(Array.isArray(saved.wishlist))State.wishlist=[...new Set([...(State.wishlist||[]),...saved.wishlist])];
    if(Array.isArray(saved.cart))State.cart=mergeCartItems(saved.cart,State.cart);
    if(Array.isArray(saved.recentlyViewed))State.recentlyViewed=[...new Set([...(saved.recentlyViewed||[]),...(State.recentlyViewed||[])])].slice(0,10);
  }catch(err){console.warn('loadUserData profile:',err);}

  try{
    // Firebase Realtime Database Rules must define .indexOn: ["userId"] at /orders.
    const ordersSnap=await get(query(ref(db,'orders'),orderByChild('userId'),equalTo(uid)));
    State.orders=ordersSnap.exists()
      ?Object.keys(ordersSnap.val()).map(k=>({id:k,...ordersSnap.val()[k]}))
        .sort((x,y)=>(Number(y.date)||0)-(Number(x.date)||0)):[];
  }catch(err){
    console.error('loadUserData orders (check /orders .indexOn and read rules):',err);
    State.orders=[];
  }

  try{
    const notifSnap=await get(ref(db,'notifications/'+uid));
    State.notifications=notifSnap.exists()
      ?Object.keys(notifSnap.val()).map(k=>({id:k,...notifSnap.val()[k]}))
        .sort((x,y)=>(Number(y.date)||0)-(Number(x.date)||0)):[];
  }catch(err){console.warn('loadUserData notifications:',err);State.notifications=[];}

  State.myReviews=[];
  try{
    const pids=[...new Set(State.orders.flatMap(o=>(Array.isArray(o.items)?o.items:[])
      .map(it=>String(it.productId||'')).filter(Boolean)))];
    const snaps=await Promise.all(pids.map(pid=>get(ref(db,'reviews/'+pid))));
    snaps.forEach((snap,i)=>{
      if(!snap.exists())return;
      const pid=pids[i];
      Object.keys(snap.val()).forEach(rid=>{
        const review=snap.val()[rid];
        if(String(review.uid||'')===String(uid))State.myReviews.push({id:rid,productId:pid,...review});
      });
    });
    State.myReviews.sort((x,y)=>(Number(y.date)||0)-(Number(x.date)||0));
  }catch(err){console.warn('loadUserData reviews:',err);}
  persistLocal();
}
async function loadReviews(pid){
  try{
    const snap = await get(ref(db,'reviews/'+pid));
    if(snap.exists()) return Object.keys(snap.val()).map(k=>({id:k,...snap.val()[k]})).sort((a,b)=>(b.date||0)-(a.date||0));
  }catch{}
  return [];
}
// Reviews the user is eligible to write (delivered order containing product)
function getUserEligibleReviewItems(){
  const eligible = [];
  State.orders.forEach(o => {
    if (o.status !== 'delivered') return;
    (o.items||[]).forEach(it => {
      const pid = it.productId;
      // already reviewed this order+product?
      const already = State.myReviews.some(r => r.orderId === o.id && String(r.productId) === String(pid));
      if (!already) eligible.push({ orderId: o.id, productId: pid, order: o });
    });
  });
  return eligible;
}

/* ---------- BACKGROUND ---------- */
function applyBackground(url){
  if(url){
    State.backgroundUrl = url;
    document.body.style.backgroundImage = `url('${url}')`;
  } else {
    State.backgroundUrl = null;
    document.body.style.backgroundImage = `url('red-background.png')`;
  }
}

/* ---------- ROUTER ---------- */
const Routes = {};
function parseHash(){
  let h = location.hash.replace(/^#/,'')||'/';
  const [path,qs] = h.split('?');
  const params = {};
  if(qs) qs.split('&').forEach(pair=>{ const [k,v]=pair.split('='); if(k) params[k]=decodeURIComponent(v||''); });
  return {path,params};
}
function navigate(h){ location.hash = h; }

function renderHomeHeader(activeNav){
  return `<header class="home-header">
    <div class="header-inner">
      <a href="#/" class="logo" aria-label="GEN Z home">
        <svg class="logo-svg" viewBox="0 0 220 60" xmlns="http://www.w3.org/2000/svg" aria-label="GEN Z">
          <defs><linearGradient id="lg2" x1="0" y1="0" x2="1" y2="0">
            <stop offset="0" stop-color="#e11d48"/><stop offset="1" stop-color="#ff2a4b"/>
          </linearGradient></defs>
          <text x="0" y="42" font-family="Inter,system-ui,sans-serif" font-weight="900" font-style="italic" font-size="40" fill="url(#lg2)" letter-spacing="-2">GEN Z</text>
          <rect x="0" y="48" width="220" height="3" fill="url(#lg2)"/>
        </svg>
        <p>Shop Your Vibe</p>
      </a>
      <form class="search-bar" onsubmit="event.preventDefault();App.submitSearch('headerSearchInput')" role="search">
        <label for="headerSearchInput" class="sr-only">Search products</label>
        <input type="search" id="headerSearchInput" placeholder="Search products, brands…" autocomplete="off" />
        <button type="submit" aria-label="Search"><i data-lucide="search"></i></button>
      </form>
      <div class="header-actions">
        <a class="header-btn" href="#/account" aria-label="Account"><i data-lucide="user"></i><span class="hide-mobile">Account</span></a>
        <a class="header-btn" href="#/wishlist" aria-label="Wishlist"><i data-lucide="heart"></i><span class="badge" id="wishlistBadge">0</span><span class="hide-mobile">Wishlist</span></a>
        <a class="header-btn" href="#/cart" aria-label="Cart"><i data-lucide="shopping-cart"></i><span class="badge" id="cartBadge">0</span><span class="hide-mobile">Cart</span></a>
        <button class="header-btn" onclick="App.toggleMobileNav()" aria-label="Menu"><i data-lucide="menu"></i></button>
      </div>
    </div>
    <nav class="home-nav" aria-label="Primary"><div class="container">
      <a class="tab-btn ${activeNav==='home'?'active':''}" href="#/" data-nav="home">Home</a>
      <a class="tab-btn ${activeNav==='shop'?'active':''}" href="#/shop" data-nav="shop">Shop</a>
      <a class="tab-btn ${activeNav==='cat-all'?'active':''}" href="#/category/all" data-nav="cat-all">All</a>
      <a class="tab-btn" href="#/shop?sort=discount">Sale 🔥</a>
      <a class="tab-btn ${activeNav==='support'?'active':''}" href="#/support" data-nav="support">Support</a>
    </div></nav>
  </header>
  <div id="mobileNavBackdrop" class="mobile-nav-backdrop" onclick="App.toggleMobileNav()"></div>
  <aside id="mobileNav" class="mobile-nav" aria-hidden="true">
    <div class="mobile-nav-head"><span class="logo"><svg class="logo-svg" viewBox="0 0 220 60" style="height:24px"><text x="0" y="42" font-family="Inter,system-ui,sans-serif" font-weight="900" font-style="italic" font-size="40" fill="#e11d48" letter-spacing="-2">GEN Z</text></svg></span>
      <button onclick="App.toggleMobileNav()" aria-label="Close menu"><i data-lucide="x"></i></button></div>
    <a href="#/" data-close-nav>Home</a>
    <a href="#/shop" data-close-nav>Shop</a>
    <a href="#/wishlist" data-close-nav>Wishlist</a>
    <a href="#/cart" data-close-nav>Cart</a>
    <a href="#/orders" data-close-nav>My Orders</a>
    <a href="#/account" data-close-nav>My Account</a>
    <a href="#/notifications" data-close-nav>Notifications</a>
    <a href="#/support" data-close-nav>Support</a>
  </aside>`;
}

let routeRenderToken=0;
let mountDebounceTimer=null;
function scheduleMount(delay=180){
  if(mountDebounceTimer) clearTimeout(mountDebounceTimer);
  mountDebounceTimer=setTimeout(()=>{
    mountDebounceTimer=null;
    mount({preserveScroll:true});
  },delay);
}
function mount(options={}){
  const preserveScroll=options.preserveScroll===true;
  const previousScrollY=window.scrollY||window.pageYOffset||0;
  const renderToken=++routeRenderToken;
  if(!State.ready){
    document.getElementById('app-content').innerHTML = `<div style="padding:20px 0"><div class="product-grid">
      <div class="skeleton skeleton-card"></div><div class="skeleton skeleton-card"></div>
      <div class="skeleton skeleton-card"></div><div class="skeleton skeleton-card"></div>
    </div></div>`; return;
  }
  const {path,params} = parseHash();
  const seg = path.split('/').filter(Boolean);
  const route = seg[0]||'home';
  const arg = seg[1]?decodeURIComponent(seg[1]):null;

  document.querySelectorAll('[data-nav]').forEach(a=>{
    a.classList.toggle('active', a.dataset.nav === route);
  });

  const content = document.getElementById('app-content');
  content.innerHTML = '';
  if(!preserveScroll) window.scrollTo({top:0,behavior:'instant'});

  // Dashboard header ONLY for home route
  if (route === 'home') {
    content.innerHTML = renderHomeHeader('home');
    const homeMount = document.createElement('div');
    homeMount.id = 'homeMount';
    content.appendChild(homeMount);
    try { Routes.home(homeMount); } catch(err){ console.error(err); }
    refreshIcons();
    updateBadges();
    return;
  }

  try{
    switch(route){
      case 'shop': Routes.shop(content,params); break;
      case 'category': Routes.category(content,arg,params); break;
      case 'product':
        Routes.product(content,arg,renderToken).then(()=>{if(renderToken===routeRenderToken){refreshIcons();updateBadges();}}).catch(err=>{console.error('Product page render failed:',err);if(renderToken===routeRenderToken)content.innerHTML=`<div class="empty-state"><h3>Could not load product</h3><p>${escapeHtml(err.message||'Please try again.')}</p></div>`;});
        break;
      case 'search': Routes.search(content,params); break;
      case 'cart': Routes.cart(content); break;
      case 'wishlist': Routes.wishlist(content); break;
      case 'checkout': Routes.checkout(content); break;
      case 'success': Routes.success(content,arg); break;
      case 'account': Routes.account(content); break;
      case 'login': Routes.login(content); break;
      case 'register': Routes.register(content); break;
      case 'orders': Routes.orders(content); break;
      case 'order': Routes.orderDetail(content,arg); break;
      case 'notifications': Routes.notifications(content); break;
      case 'myreviews': Routes.myReviews(content); break;
      case 'support': Routes.support(content); break;
      case 'chat': Routes.chat(content); break;
      default: Routes.notfound(content);
    }
  }catch(err){
    console.error(err);
    content.innerHTML = `<div class="empty-state"><i data-lucide="alert-triangle"></i><h3>Something went wrong</h3><p>${escapeHtml(err.message||'Unknown error')}</p><a href="#/" class="btn btn-primary">Go Home</a></div>`;
  }
  refreshIcons();
  updateBadges();
  if(preserveScroll) window.scrollTo(0,previousScrollY);
}

/* ---------- PRODUCT CARD ---------- */
function productCard(p){
  const wl = isWishlisted(p.id);
  const href = '#/product/'+p.id;
  const ep = effectivePrice(p);
  const dp = discountPercent(p);
  const hasSpecial = ep < Number(p.price||0);
  const offer=activeOfferForProduct(p.id);
  const oldPrice=offer?Number(offer.originalPrice||p.price):(Number(p.oldPrice)>Number(p.price)?Number(p.oldPrice):(hasSpecial?Number(p.price):0));
  return `<article class="product-card">
    ${dp?`<div class="discount-badge">-${dp}%</div>`:''}
    <button class="card-heart ${wl?'active':''}" aria-label="Wishlist" onclick="event.preventDefault();App.handleWishlist('${p.id}',this)">
      <i data-lucide="heart" style="width:16px;height:16px"></i>
    </button>
    <a href="${href}" class="card-img"><img src="${escapeHtml(p.image||'')}" alt="${escapeHtml(p.title)}" loading="lazy" decoding="async" onerror="this.style.opacity=0.3"></a>
    <a href="${href}" class="card-title">${escapeHtml(p.title)}</a>
    <div class="card-rating"><i data-lucide="star"></i> <span>${p.rating} (${p.reviews})</span></div>
    <div class="card-footer">
      <div>
        <div class="card-price">${fmt(ep)}</div>
        ${hasSpecial?`<div class="card-special">Special price</div>`:''}
        ${oldPrice > ep ? `<div class="card-old-price">${fmt(oldPrice)}</div>` : ''}
      </div>
      <button class="card-add" aria-label="Add to cart" onclick="event.preventDefault();App.handleAddToCart('${p.id}',1,null)">
        <i data-lucide="shopping-cart" style="width:16px;height:16px"></i>
      </button>
    </div>
    <div class="product-card-actions" style="display:flex;gap:7px;padding:0 12px 12px">
      <button class="btn btn-sm btn-ghost" style="flex:1" onclick="event.preventDefault();App.shareProduct('${p.id}')">↗ Share</button>
      <button class="btn btn-sm btn-ghost" style="flex:1" onclick="event.preventDefault();App.downloadProductImage('${p.id}')">⬇ Image</button>
    </div>
  </article>`;
}

/* ---------- HERO ---------- */
function renderHeroBanner(){
  const banners = State.banners.filter(bannerIsActive);
  if(banners.length > 0){
    return `<section class="hero-slider" id="heroSlider">
      <div class="hero-slider-track">
        ${banners.map((b,i)=>`
          <div class="hero-slide ${i===0?'active':''}" data-slide="${i}">
            ${(b.mediaType==='video'||b.video) ? `<video src="${escapeHtml(b.video||'')}" ${i===0?'autoplay':''} muted playsinline controls preload="${i===0?'auto':'metadata'}" aria-label="${escapeHtml(b.title||'Promotion')}"></video>` : `<img src="${escapeHtml(b.image||'')}" alt="${escapeHtml(b.title||'Promotion')}" loading="${i===0?'eager':'lazy'}">`}
            <div class="hero-slide-overlay"><div class="hero-slide-content">
              ${b.title?`<h2>${escapeHtml(b.title)}</h2>`:''}
              ${b.subtitle?`<p>${escapeHtml(b.subtitle)}</p>`:''}
              ${b.ctaText?`<a href="${escapeHtml(b.ctaLink||'#/shop')}" class="btn btn-secondary" style="width:fit-content">${escapeHtml(b.ctaText)}</a>`:''}
            </div></div>
          </div>`).join('')}
      </div>
      ${banners.length>1?`
        <button class="hero-nav prev" onclick="App.heroNav(-1)" aria-label="Previous"><i data-lucide="chevron-left"></i></button>
        <button class="hero-nav next" onclick="App.heroNav(1)" aria-label="Next"><i data-lucide="chevron-right"></i></button>
        <div class="hero-dots">${banners.map((_,i)=>`<button class="hero-dot ${i===0?'active':''}" data-dot="${i}" onclick="App.heroGoTo(${i})" aria-label="Go to slide ${i+1}"></button>`).join('')}</div><span class="hero-swipe-hint">Swipe or use arrows</span>
      `:''}
    </section>`;
  }
  return `<section class="hero-banner">
    <img class="hero-banner-img" src="boy-banner.png" alt="GEN Z Smart Life Smart Choice" loading="eager"
         onerror="this.style.display='none'; this.parentElement.innerHTML='<div style=&quot;padding:40px;text-align:center;color:#fff&quot;><h2>Smart Life, Smart Choice</h2><p>Shop Your Vibe</p></div>'">
  </section>`;
}
let heroSlideIndex=0,heroSlideTimer=null,heroTouchStartX=null;
function stopHeroSlider(){if(heroSlideTimer){clearTimeout(heroSlideTimer);heroSlideTimer=null;}}
function scheduleHeroAdvance(){
  stopHeroSlider();const root=document.getElementById('heroSlider');if(!root)return;
  const active=root.querySelector('.hero-slide.active');if(!active)return;
  const video=active.querySelector('video');
  if(video){video.onended=()=>heroAdvance(1);const play=video.play();if(play&&play.catch)play.catch(()=>{});return;}
  if(State.banners.filter(bannerIsActive).length>1)heroSlideTimer=setTimeout(()=>heroAdvance(1),5000);
}
function startHeroSlider(){
  stopHeroSlider();const root=document.getElementById('heroSlider');const banners=State.banners.filter(bannerIsActive);
  if(!root||banners.length<2)return;
  heroSlideIndex=Math.max(0,Math.min(heroSlideIndex,banners.length-1));
  root.addEventListener('touchstart',e=>{heroTouchStartX=e.changedTouches?.[0]?.clientX??null;},{passive:true});
  root.addEventListener('touchend',e=>{if(heroTouchStartX===null)return;const dx=(e.changedTouches?.[0]?.clientX??heroTouchStartX)-heroTouchStartX;heroTouchStartX=null;if(Math.abs(dx)>45)heroNav(dx<0?1:-1);},{passive:true});
  root.addEventListener('keydown',e=>{if(e.key==='ArrowLeft')heroNav(-1);if(e.key==='ArrowRight')heroNav(1);});
  updateHeroSlide();
}
function heroAdvance(dir){const banners=State.banners.filter(bannerIsActive);if(banners.length<2)return;heroSlideIndex=(heroSlideIndex+dir+banners.length)%banners.length;updateHeroSlide();}
function updateHeroSlide(){
  stopHeroSlider();const root=document.getElementById('heroSlider');if(!root)return;
  const slides=[...root.querySelectorAll('.hero-slide')],dots=[...root.querySelectorAll('.hero-dot')];if(!slides.length)return;
  heroSlideIndex=Math.max(0,Math.min(heroSlideIndex,slides.length-1));
  slides.forEach((slide,i)=>{slide.classList.toggle('active',i===heroSlideIndex);const v=slide.querySelector('video');if(v){if(i===heroSlideIndex){try{v.currentTime=0;}catch{}v.onended=()=>heroAdvance(1);}else{v.pause();v.onended=null;try{v.currentTime=0;}catch{}}}});
  dots.forEach((d,i)=>d.classList.toggle('active',i===heroSlideIndex));scheduleHeroAdvance();
}


/* ---------- GOOGLE DRIVE STORE LINK ---------- */
function renderAppDownloads(){
  const item = (State.appDownloads || []).find(a => {
    const link = String(a?.googleDriveLink || '').trim();
    return a && /^https:\/\/(drive\.google\.com|docs\.google\.com)\//i.test(link);
  });
  if (!item) return '';
  const description = String(item.description || '').trim();
  const link = String(item.googleDriveLink || '').trim();
  return `<section class="store-drive-link" aria-label="GEN Z Store link">
    ${description ? `<p class="store-drive-description">${escapeHtml(description)}</p>` : ''}
    <a class="store-drive-anchor" href="${escapeHtml(link)}" target="_blank" rel="noopener noreferrer">
      <i data-lucide="link"></i><span>Open Google Drive Link</span><i data-lucide="external-link"></i>
    </a>
  </section>`;
}

/* ---------- HOME ---------- */
Routes.home = function(el){
  const featured = State.products.slice(0,10);
  const newArrivals = [...State.products].sort((a,b)=>(b.createdAt||0)-(a.createdAt||0)).slice(0,5);
  const discounted = State.products.filter(p=>hasActiveDiscount(p)).sort((a,b)=>discountPercent(b)-discountPercent(a)).slice(0,10);
  const recently = State.recentlyViewed.map(getProduct).filter(Boolean).slice(0,5);

  el.innerHTML = `
    ${renderAppDownloads()}
    ${renderHeroBanner()}
    ${State.categories.length?`
      <div class="section-header"><h3>Categories</h3><a href="#/shop">View All →</a></div>
      <div class="categories-scroll">
        ${State.categories.map(c=>`
          <a href="#/category/${c.slug}" class="category-item">
            <div class="category-img">${c.img?`<img src="${escapeHtml(c.img)}" alt="${escapeHtml(c.name)}" loading="lazy" decoding="async" onerror="this.style.opacity=0.3">`:`<i data-lucide="grid"></i>`}</div>
            <span>${escapeHtml(c.name)}</span>
          </a>`).join('')}
      </div>`:''}
    ${featured.length?`
      <div class="section-header"><h3>Trending Products 🔥</h3><a href="#/shop">View All →</a></div>
      <div class="product-grid">${featured.map(productCard).join('')}</div>`:`
      <div class="empty-state" style="margin-top:40px"><i data-lucide="package"></i>
        <h3>No products yet</h3><p>The store is empty. Add products from the Admin Panel to see them here.</p>
      </div>`}
    ${discounted.length?`
      <div class="offers-strip">
        <div><h3>OFFERS & <span>DISCOUNTS</span> 🔥</h3><p>Biggest savings on your favourite drops.</p></div>
        <a href="#/shop?sort=discount" class="btn btn-primary btn-sm">View All Offers →</a>
      </div>
      <div class="product-grid">${discounted.map(productCard).join('')}</div>`:''}
    ${newArrivals.length?`<div class="section-header"><h3>New Arrivals</h3><a href="#/shop?sort=newest">View All →</a></div><div class="product-grid">${newArrivals.map(productCard).join('')}</div>`:''}
    ${recently.length?`<div class="section-header"><h3>Recently Viewed</h3></div><div class="product-grid">${recently.map(productCard).join('')}</div>`:''}
    <div class="page-card" style="text-align:center;margin-top:40px">
      <h3 style="font-size:18px;margin-bottom:8px">Stay in the loop</h3>
      <p class="text-muted text-sm" style="margin-bottom:14px">Get drops, deals and updates.</p>
      <form onsubmit="event.preventDefault();App.toast('Subscribed!','success');this.reset()" style="display:flex;gap:8px;max-width:400px;margin:0 auto;flex-wrap:wrap">
        <input type="email" placeholder="you@example.com" required style="flex:1;min-width:0;background:var(--dark-2);border:1px solid var(--border);border-radius:10px;padding:11px 12px;color:var(--text);outline:none">
        <button type="submit" class="btn btn-primary">Subscribe</button>
      </form>
    </div>`;
  startHeroSlider();
};

/* ---------- SHOP ---------- */
Routes.shop = function(el, params){
  const cat = params.cat||'';
  const sort = params.sort||'popular';
  const minP = params.min?Number(params.min):null;
  const maxP = params.max?Number(params.max):null;
  const inStock = params.stock==='1';
  const brands = params.brand?params.brand.split(','):[];

  let items = [...State.products];
  if(cat) items = items.filter(p=>p.category===cat);
  if(minP!=null) items = items.filter(p=>effectivePrice(p)>=minP);
  if(maxP!=null) items = items.filter(p=>effectivePrice(p)<=maxP);
  if(inStock) items = items.filter(p=>p.stock>0);
  if(brands.length) items = items.filter(p=>brands.includes(p.brand));

  switch(sort){
    case 'price-asc': items.sort((a,b)=>effectivePrice(a)-effectivePrice(b)); break;
    case 'price-desc': items.sort((a,b)=>effectivePrice(b)-effectivePrice(a)); break;
    case 'newest': items.sort((a,b)=>(b.createdAt||0)-(a.createdAt||0)); break;
    case 'rating': items.sort((a,b)=>b.rating-a.rating); break;
    case 'discount': items.sort((a,b)=>discountPercent(b)-discountPercent(a)); break;
    default: items.sort((a,b)=>(b.rating||0)-(a.rating||0));
  }

  const allBrands = [...new Set(State.products.map(p=>p.brand))].filter(Boolean).sort();
  const chips = [];
  if(cat) chips.push({key:'cat',label:'Category: '+cat});
  if(minP!=null) chips.push({key:'min',label:'Min: '+fmt(minP)});
  if(maxP!=null) chips.push({key:'max',label:'Max: '+fmt(maxP)});
  if(inStock) chips.push({key:'stock',label:'In Stock'});
  brands.forEach(b=>chips.push({key:'brand-'+b,label:'Brand: '+b}));

  el.innerHTML = `
    <div class="shop-layout">
      <aside class="filters mobile-closed" id="filtersPanel">
        <h3>Filters <button onclick="App.clearFilters()">Clear all</button></h3>
        <div class="filter-group">
          <h4>Category</h4>
          ${State.categories.map(c=>`<label><input type="checkbox" data-fcat value="${c.slug}" ${cat===c.slug?'checked':''} onchange="App.applyShopFilter()"> ${escapeHtml(c.name)}</label>`).join('')||'<p class="text-xs text-muted">No categories</p>'}
        </div>
        <div class="filter-group">
          <h4>Brand</h4>
          ${allBrands.map(b=>`<label><input type="checkbox" data-fbrand value="${escapeHtml(b)}" ${brands.includes(b)?'checked':''} onchange="App.applyShopFilter()"> ${escapeHtml(b)}</label>`).join('')||'<p class="text-xs text-muted">No brands</p>'}
        </div>
        <div class="filter-group">
          <h4>Price</h4>
          <div class="price-inputs">
            <input type="number" placeholder="Min" id="fMin" value="${minP||''}">
            <input type="number" placeholder="Max" id="fMax" value="${maxP||''}">
          </div>
          <button class="btn btn-sm btn-ghost btn-block" style="margin-top:8px" onclick="App.applyShopFilter()">Apply</button>
        </div>
        <div class="filter-group">
          <h4>Availability</h4>
          <label><input type="checkbox" id="fStock" ${inStock?'checked':''} onchange="App.applyShopFilter()"> In stock only</label>
        </div>
      </aside>
      <div>
        <div class="mobile-filter-toggle">
          <button class="btn btn-ghost btn-sm" onclick="document.getElementById('filtersPanel').classList.toggle('mobile-closed')">
            <i data-lucide="sliders"></i> Filters
          </button>
          <span class="text-muted text-sm">${items.length} products</span>
        </div>
        <div class="sort-bar">
          <div class="text-sm text-muted">Showing ${items.length} of ${State.products.length}</div>
          <select onchange="App.changeSort(this.value)">
            <option value="popular" ${sort==='popular'?'selected':''}>Popular</option>
            <option value="newest" ${sort==='newest'?'selected':''}>Newest</option>
            <option value="price-asc" ${sort==='price-asc'?'selected':''}>Price: Low → High</option>
            <option value="price-desc" ${sort==='price-desc'?'selected':''}>Price: High → Low</option>
            <option value="rating" ${sort==='rating'?'selected':''}>Rating</option>
            <option value="discount" ${sort==='discount'?'selected':''}>Discount</option>
          </select>
        </div>
        ${chips.length?`<div class="chips">${chips.map(c=>`<span class="chip">${escapeHtml(c.label)} <button onclick="App.removeChip('${c.key}')">×</button></span>`).join('')}</div>`:''}
        ${items.length===0?`<div class="empty-state"><i data-lucide="search-x"></i><h3>No products match</h3><p>Try removing some filters or add products in Admin.</p><button class="btn btn-primary" onclick="App.clearFilters()">Clear filters</button></div>`:`<div class="product-grid">${items.map(productCard).join('')}</div>`}
      </div>
    </div>`;
};

/* ---------- CATEGORY ---------- */
Routes.category = function(el, slug, params){
  if(slug==='all'){
    const items = State.products;
    el.innerHTML = `
      <div class="breadcrumb"><a href="#/">Home</a> / <span>All Categories</span></div>
      ${State.categories.length?`
        <div class="section-header"><h3>Categories</h3></div>
        <div class="categories-scroll">
          ${State.categories.map(c=>`
            <a href="#/category/${c.slug}" class="category-item">
              <div class="category-img">${c.img?`<img src="${escapeHtml(c.img)}" alt="${escapeHtml(c.name)}" onerror="this.style.opacity=0.3">`:`<i data-lucide="grid"></i>`}</div>
              <span>${escapeHtml(c.name)}</span>
            </a>`).join('')}
        </div>`:''}
      <div class="section-header"><h3>All Products (${items.length})</h3></div>
      ${items.length===0?`<div class="empty-state"><i data-lucide="package-search"></i><h3>No products yet</h3><p>Add products from Admin Panel.</p></div>`:`<div class="product-grid">${items.map(productCard).join('')}</div>`}`;
    return;
  }
  const cat = State.categories.find(c=>c.slug===slug);
  const items = State.products.filter(p=>p.category===slug);
  el.innerHTML = `
    <div class="breadcrumb"><a href="#/">Home</a> / <a href="#/shop">Shop</a> / <span>${escapeHtml(cat?cat.name:slug)}</span></div>
    <div class="page-card">
      <h1 class="page-title">${escapeHtml(cat?cat.name:slug)}</h1>
      <p class="text-muted text-sm">Browse ${items.length} products.</p>
    </div>
    ${items.length===0?`<div class="empty-state"><i data-lucide="package-search"></i><h3>No products in this category</h3><p>Add products via Admin Panel.</p></div>`:`<div class="product-grid">${items.map(productCard).join('')}</div>`}`;
};

/* ---------- PRODUCT DETAIL ---------- */
Routes.product = async function(el, id, renderToken=routeRenderToken){
  const p = getProduct(id);
  if(!p) return Routes.notfound(el);

  State.recentlyViewed = [p.id, ...State.recentlyViewed.filter(x=>x!==p.id)].slice(0,10);
  persistLocal();

  const wl = isWishlisted(p.id);
  const similar = State.products.filter(x=>String(x.id)!==String(p.id)&&x.category===p.category).slice(0,4);
  const reviews = await loadReviews(p.id);
  if(renderToken!==routeRenderToken || !el.isConnected || !el.closest('#app-content') || !location.hash.startsWith('#/product/')) return;
  const imgs = (p.images&&p.images.length)?p.images:[p.image];
  const ep = effectivePrice(p);
  const hasSpecial = ep < Number(p.price||0);
  const dp = discountPercent(p);
  const offer=activeOfferForProduct(p.id);
  const oldPrice=offer?Number(offer.originalPrice||p.price):(Number(p.oldPrice)>Number(p.price)?Number(p.oldPrice):(hasSpecial?Number(p.price):0));

  el.innerHTML = `<div id="page-product">
    <div class="breadcrumb">
      <a href="#/">Home</a> <i data-lucide="chevron-right" style="width:12px;height:12px"></i>
      <a href="#/category/${p.category}">${escapeHtml(p.categoryName)}</a>
      <i data-lucide="chevron-right" style="width:12px;height:12px"></i>
      <span>${escapeHtml(p.title)}</span>
    </div>
    <div class="product-layout">
      <div>
        <div class="gallery-main" onclick="App.openImageViewer('${escapeHtml(p.image||imgs[0]||'')}')">
          <img src="${escapeHtml(p.image||imgs[0]||'')}" alt="${escapeHtml(p.title)}" id="mainImage" onerror="this.style.opacity=0.3">
          <button class="card-heart ${wl?'active':''}" style="top:16px;right:16px;z-index:3;position:absolute" aria-label="Wishlist" onclick="event.stopPropagation();App.handleWishlist('${p.id}',this)">
            <i data-lucide="heart" style="width:20px;height:20px"></i>
          </button>
        </div>
        <div class="gallery-thumbs">
          ${imgs.map((img,i)=>`<button class="thumb ${i===0?'active':''}" onclick="App.changeImage(this,'${escapeHtml(img)}')"><img src="${escapeHtml(img)}" alt="view ${i+1}" onerror="this.style.opacity=0.3"></button>`).join('')}
          ${p.video ? `<button class="thumb" onclick="App.openVideo('${escapeHtml(p.video)}')" style="display:flex;align-items:center;justify-content:center;background:#000"><i data-lucide="play-circle" style="width:24px;height:24px;color:var(--red)"></i></button>` : ''}
        </div>
      </div>
      <div class="product-info">
        <h1>${escapeHtml(p.title)}</h1>
        <div class="rating-row">
          <span style="display:flex;align-items:center;gap:4px;color:var(--yellow)"><i data-lucide="star"></i> ${p.rating} (${p.reviews} reviews)</span>
          <span>|</span><span>${escapeHtml(p.brand)}</span>
        </div>
        <div class="genz-choice">GEN Z Choice</div>
        <ul class="features-list">${(p.features||[]).map(f=>`<li><i data-lucide="check-circle-2"></i> ${escapeHtml(f)}</li>`).join('')}</ul>
        <div class="price-row">
          <span class="price-main">${fmt(ep)}</span>
          ${hasSpecial?`<span class="price-special">Special Price</span>`:''}
          ${oldPrice > ep ? `<span class="price-old">${fmt(oldPrice)}</span><span class="price-discount">-${dp}%</span>` : ''}
        </div>
        ${p.colors && p.colors.length ? `
          <div class="color-picker">
            <p>Color: <span id="selectedColorText">Default</span></p>
            <div class="colors">
              ${p.colors.map((c,i)=>`<button class="color-dot ${i===0?'active':''}" style="background-color:${c};${c==='#ffffff'?'border-color:#666':''}" onclick="App.selectColor(this,'${c}')" aria-label="Color ${i+1}"></button>`).join('')}
            </div>
          </div>`:''}
        <div class="qty-row">
          <label>Quantity:</label>
          <div class="qty-ctrl">
            <button onclick="App.changeQty(-1)" aria-label="Decrease">-</button>
            <span id="qtyDisplay">1</span>
            <button onclick="App.changeQty(1)" aria-label="Increase">+</button>
          </div>
          <span class="stock-tag ${p.stock===0?'out':''}"><i data-lucide="check-circle"></i> ${p.stock===0?'Out of stock':'In Stock ('+p.stock+')'}</span>
        </div>
        <div style="display:flex;gap:8px;flex-wrap:wrap;margin:10px 0 4px">
          <button class="btn btn-sm btn-ghost" onclick="App.shareProduct('${p.id}')">↗ Share product</button>
          <button class="btn btn-sm btn-ghost" onclick="App.downloadProductImage('${p.id}')">⬇ Download product image</button>
        </div>
      </div>
      <div class="checkout-card">
        <div class="ship-row"><span><i data-lucide="truck" style="width:16px;height:16px;margin-right:6px;display:inline;vertical-align:middle"></i> Delivery across Pakistan</span></div>
        <p style="font-size:11px;color:var(--text-muted)">Flat delivery fee: <strong>${fmt(ENV.STORE.deliveryFee)}</strong></p>
        <hr>
        <div class="delivery-info"><i data-lucide="refresh-ccw"></i><div><p class="title">7-Day Returns</p><p class="sub">Easy refund</p></div></div>
        <div class="delivery-info"><i data-lucide="shield-check"></i><div><p class="title">100% Authentic</p><p class="sub">Guaranteed</p></div></div>
        <button class="btn btn-primary btn-block" onclick="App.handleAddToCart('${p.id}', App.currentQty, App.currentColor)" ${p.stock===0?'disabled':''}><i data-lucide="shopping-cart"></i> Add to Cart</button>
        <button class="btn btn-secondary btn-block" onclick="App.buyNow('${p.id}')" ${p.stock===0?'disabled':''}><i data-lucide="zap"></i> Buy Now</button>
      </div>
    </div>
    <div class="product-tabs-section">
      <div class="tabs-header">
        <button class="tab-item active" onclick="App.switchTab(this,'tab-overview')">Overview</button>
        <button class="tab-item" onclick="App.switchTab(this,'tab-specs')">Specifications</button>
        <button class="tab-item" onclick="App.switchTab(this,'tab-reviews')">Reviews (${reviews.length})</button>
      </div>
      <div id="tab-overview" class="tab-pane active">
        <div class="highlights-grid">
          <div class="highlights-banner"><h3>Smart Life<br><span>GEN Z</span></h3><p>Shop Your Vibe</p></div>
          <div class="highlights-list">
            <h4 style="font-size:14px;margin-bottom:12px">Highlights</h4>
            ${(p.features||[]).map(f=>`<div><i data-lucide="check-circle-2"></i> ${escapeHtml(f)}</div>`).join('')}
          </div>
          <div class="review-summary">
            <h3>Customer Reviews</h3>
            <div class="big-rating"><span class="score">${p.rating||'—'}</span><div class="stars">${'<i data-lucide="star"></i>'.repeat(5)}</div></div>
            <p>Based on ${p.reviews} reviews</p>
          </div>
        </div>
        <div style="margin-top:24px" id="reviewList">
          ${reviews.length===0?`<p class="text-muted text-sm">No reviews yet. Verified buyers can review after delivery.</p>`:reviews.map(r=>`
            <div class="review-card">
              <div class="head">
                <div class="user"><div class="avatar">${escapeHtml((r.name||'U')[0].toUpperCase())}</div>
                  <div><p class="name">${escapeHtml(r.name||'User')}</p>
                  ${r.verified?'<p class="verified"><i data-lucide="check-circle"></i> Verified Purchase</p>':''}
                  </div>
                </div>
                <div class="r-stars">${'<i data-lucide="star"></i>'.repeat(Number(r.rating)||5)}</div>
              </div>
              <p>${escapeHtml(r.text||'')}</p>
              <p class="r-date">${r.date?new Date(r.date).toLocaleDateString():''}</p>
            </div>`).join('')}
        </div>
        <div style="margin-top:16px" id="reviewFormWrap">
          ${State.user ? '' : '<p class="text-muted text-sm">Sign in and purchase this product to leave a review.</p>'}
        </div>
      </div>
      <div id="tab-specs" class="tab-pane">
        <div class="features-list">
          <div><strong style="display:inline-block;min-width:140px">Brand</strong> ${escapeHtml(p.brand)}</div>
          <div><strong style="display:inline-block;min-width:140px">Category</strong> ${escapeHtml(p.categoryName)}</div>
          <div><strong style="display:inline-block;min-width:140px">Stock</strong> ${p.stock} units</div>
        </div>
        <p style="color:var(--text-muted);font-size:13px;margin-top:12px">${escapeHtml(p.description||'')}</p>
      </div>
      <div id="tab-reviews" class="tab-pane">
        <p style="color:var(--text-muted);font-size:14px">${reviews.length} review(s). See Overview tab for details.</p>
      </div>
    </div>
    ${similar.length?`<div class="section-header" style="margin-top:40px"><h3>Similar Products</h3><a href="#/category/${p.category}">View All →</a></div><div class="product-grid">${similar.map(productCard).join('')}</div>`:''}
  </div>`;

  App.currentQty = 1;
  App.currentColor = (p.colors&&p.colors[0])||null;
  App.currentProductId = p.id;
  // Check eligibility & inject review form if eligible
  if (State.user) {
    const eligible = getUserEligibleReviewItems().filter(e => String(e.productId) === String(p.id));
    const wrap = document.getElementById('reviewFormWrap');
    if (wrap && eligible.length) {
      wrap.innerHTML = `<h4 style="margin-bottom:10px">Write a review</h4>
        <form onsubmit="event.preventDefault();App.submitReview(event, '${p.id}', '${eligible[0].orderId}')">
          <div class="field"><label>Rating</label>
            <select name="rating" required>
              <option value="5">5 stars</option><option value="4">4 stars</option>
              <option value="3">3 stars</option><option value="2">2 stars</option>
              <option value="1">1 star</option>
            </select>
          </div>
          <div class="field"><label>Your review</label>
            <textarea name="review" rows="3" minlength="10" maxlength="500" required placeholder="Share your experience (min 10 chars)"></textarea>
          </div>
          <button type="submit" class="btn btn-primary">Submit Verified Review</button>
        </form>`;
    } else if (wrap) {
      wrap.innerHTML = '<p class="text-muted text-sm">Reviews are only available after your order is delivered.</p>';
    }
  }
  refreshIcons();
};

/* ---------- SEARCH ---------- */
Routes.search = function(el, params){
  const q = (params.q||'').trim().toLowerCase();
  let results = [];
  if(q){
    const terms = q.split(/\s+/).filter(Boolean);
    results = State.products.filter(p=>{
      const hay = [
        p.title, p.brand, p.categoryName, p.category, p.description
      ].filter(Boolean).join(' ').toLowerCase();
      return terms.every(t => hay.includes(t));
    });
  }
  el.innerHTML = `
    <h1 class="page-title">Search</h1>
    <form onsubmit="event.preventDefault();App.submitSearch('searchPageInput')" style="display:flex;gap:8px;margin-bottom:20px;flex-wrap:wrap">
      <input type="search" id="searchPageInput" value="${escapeHtml(params.q||'')}" placeholder="Search products…" style="flex:1;min-width:0;background:var(--dark-2);border:1px solid var(--border);border-radius:10px;padding:11px 12px;color:var(--text);outline:none">
      <button type="submit" class="btn btn-primary">Search</button>
    </form>
    ${!q?`<div class="empty-state"><i data-lucide="search"></i><h3>Search GEN Z</h3><p>Try keywords from titles or brands.</p></div>`:
      results.length===0?`<div class="empty-state"><i data-lucide="search-x"></i><h3>No results for "${escapeHtml(q)}"</h3><p>Try different keywords.</p><a href="#/shop" class="btn btn-primary">Browse all</a></div>`:
      `<p class="text-muted text-sm" style="margin-bottom:14px">${results.length} results for "${escapeHtml(q)}"</p><div class="product-grid">${results.map(productCard).join('')}</div>`}`;
};

/* ---------- CART ---------- */
Routes.cart = function(el){
  if(State.cart.length===0){
    el.innerHTML = `<h1 class="page-title">Shopping Cart</h1><div class="empty-state"><i data-lucide="shopping-cart"></i><h3>Your cart is empty</h3><p>Start shopping to fill it up.</p><a href="#/shop" class="btn btn-primary">Shop Now</a></div>`;
    return;
  }
  const orig = cartOriginalSubtotal(), disc = cartDiscount(), sub = cartSubtotal(), del = cartDelivery(), total = cartTotal();
  el.innerHTML = `<h1 class="page-title">Shopping Cart (${State.cart.length})</h1>
    <div class="cart-layout">
      <div class="page-card">
        ${State.cart.map(it=>{
          const p = getProduct(it.productId);
          if(!p) return '';
          const ep = effectivePrice(p);
          return `<div class="cart-item">
            <a href="#/product/${p.id}"><img src="${escapeHtml(p.image||'')}" alt="${escapeHtml(p.title)}" onerror="this.style.opacity=0.3"></a>
            <div class="info">
              <h4><a href="#/product/${p.id}">${escapeHtml(p.title)}</a></h4>
              ${it.color?`<div class="variant">Color: <span style="display:inline-block;width:12px;height:12px;border-radius:50%;background:${it.color};border:1px solid #444;vertical-align:middle"></span></div>`:''}
              <div class="price">${fmt(ep)} ${ep<Number(p.price||0)?`<span style="color:#fbbf24;font-size:10px">sale</span>`:''}</div>
            </div>
            <div class="actions">
              <div class="qty-ctrl sm">
                <button onclick="App.cartQty('${p.id}','${it.color||''}',-1)">-</button>
                <span>${it.qty}</span>
                <button onclick="App.cartQty('${p.id}','${it.color||''}',1)">+</button>
              </div>
              <button class="btn btn-sm btn-danger" onclick="App.removeCartItem('${p.id}','${it.color||''}')">Remove</button>
            </div>
          </div>`;
        }).join('')}
      </div>
      <div class="summary-card">
        <h3>Order Summary</h3>
        <div class="summary-row"><span>Subtotal (original)</span><span>${fmt(orig)}</span></div>
        ${disc>0?`<div class="summary-row discount"><span>Discount</span><span>-${fmt(disc)}</span></div>`:''}
        <div class="summary-row"><span>Discounted subtotal</span><span>${fmt(sub)}</span></div>
        <div class="summary-row"><span>Delivery</span><span>${del===0?'Free':fmt(del)}</span></div>
        <div class="summary-row total"><span>Total</span><span class="val">${fmt(total)}</span></div>
        <a href="#/checkout" class="btn btn-primary btn-block" style="margin-top:14px">Proceed to Checkout</a>
        <a href="#/shop" class="btn btn-ghost btn-block" style="margin-top:8px">Continue Shopping</a>
        <button class="btn btn-danger btn-block btn-sm" style="margin-top:8px" onclick="App.clearCart()">Clear Cart</button>
      </div>
    </div>`;
};

/* ---------- WISHLIST ---------- */
Routes.wishlist = function(el){
  const items = State.wishlist.map(getProduct).filter(Boolean);
  if(items.length===0){
    el.innerHTML = `<h1 class="page-title">Wishlist</h1><div class="empty-state"><i data-lucide="heart"></i><h3>Your wishlist is empty</h3><p>Save products you love.</p><a href="#/shop" class="btn btn-primary">Discover Products</a></div>`;
    return;
  }
  el.innerHTML = `<h1 class="page-title">Wishlist (${items.length})</h1><div class="product-grid">${items.map(productCard).join('')}</div>`;
};

/* ---------- CHECKOUT ---------- */
Routes.checkout = function(el){
if(!State.user||State.user.isGuest){Storage.set('returnTo','#/checkout');el.innerHTML=`<div class="empty-state"><i data-lucide="lock"></i><h3>Sign in before checkout</h3><p>Create a GEN Z account or sign in to place an order and track delivery.</p><a href="#/login" class="btn btn-primary">Sign In</a> <a href="#/register" class="btn btn-ghost">Create Account</a></div>`;return;}
if(State.cart.length===0){
    el.innerHTML = `<div class="empty-state"><i data-lucide="shopping-cart"></i><h3>Cart is empty</h3><a href="#/shop" class="btn btn-primary">Shop Now</a></div>`;
    return;
  }
  const orig = cartOriginalSubtotal(), disc = cartDiscount(), sub = cartSubtotal(), del = cartDelivery(), total = cartTotal();
  const defaultAddr = State.addresses.find(a=>a.isDefault) || State.addresses[0] || null;

  el.innerHTML = `<h1 class="page-title">Checkout</h1>
    <div class="cart-layout">
      <div>
        <div class="page-card">
          <h3 style="margin-bottom:14px">Shipping Address</h3>
          <form id="checkoutForm" onsubmit="event.preventDefault();App.placeOrder(event)">
            <div class="field-row two">
              <div class="field"><label>Full Name *</label><input name="name" value="${escapeHtml(State.userProfile?.name||'')}" required minlength="2"></div>
              <div class="field"><label>Phone *</label><input name="phone" value="${escapeHtml(State.userProfile?.phone||'')}" placeholder="03XX-XXXXXXX" pattern="^03\\d{2}-?\\d{7}$" required title="Format: 03XX-XXXXXXX"></div>
            </div>
            <div class="field-row two">
              <div class="field"><label>Province *</label>
                <select name="province" required>
                  <option value="">Select</option>
                  <option>Sindh</option><option>Punjab</option><option>KPK</option><option>Balochistan</option><option>Islamabad</option><option>Gilgit-Baltistan</option><option>AJK</option>
                </select>
              </div>
              <div class="field"><label>City *</label><input name="city" value="${defaultAddr?escapeHtml(defaultAddr.city||''):''}" required></div>
            </div>
            <div class="field"><label>Complete House / Street / Area Address *</label><textarea name="area" id="checkoutFullAddress" rows="3" required placeholder="Enter your delivery address">${defaultAddr?escapeHtml(defaultAddr.area||''):''}</textarea><p class="text-xs text-muted" style="margin-top:5px">Enter your address in your own words. No minimum word limit.</p></div>
            <div class="field-row two">
              <div class="field"><label>Postal Code</label><input name="postal" value="${defaultAddr?escapeHtml(defaultAddr.postal||''):''}"></div>
              <div class="field"><label>Landmark</label><input name="landmark" placeholder="Optional"></div>
            </div>

<div class="field">
  <label>Delivery Location (Optional)</label>
  <p class="text-xs text-muted" style="margin-bottom:6px">
    You can optionally use your current location or pin the map. This is not required to place an order.
  </p>

  <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:8px">
    <button type="button" class="btn btn-sm btn-primary" id="btnUseLocation" onclick="App.useCurrentLocation()">
      <i data-lucide="locate-fixed"></i> Use current location
    </button>
    <button type="button" class="btn btn-sm btn-ghost" onclick="App.clearPinnedLocation()">
      <i data-lucide="x"></i> Clear
    </button>
  </div>

  <div class="map-wrap" id="mapWrap">
    <div id="map"><div class="map-fallback">Loading map…</div></div>
    <div class="map-hint" id="mapHint">Optional: click on the map to add a delivery pin</div>
  </div>

  <input type="hidden" name="lat" id="deliveryLat">
  <input type="hidden" name="lng" id="deliveryLng">
  <input type="hidden" name="locSource" id="deliveryLocSource">
</div>
            <div class="field"><label>Order Notes</label><textarea name="notes" rows="2" placeholder="Optional"></textarea></div>
            <div class="field"><label>Payment Method *</label>
              <select name="payment" required>
                ${(State.settings.codEnabled ?? ENV.STORE.codEnabled) ? '<option value="cod">Cash on Delivery</option>' : ''}
                <option value="online">Online (manual confirmation)</option>
              </select>
            </div>
            <button type="submit" class="btn btn-primary btn-block btn-lg" style="padding:14px" id="placeOrderBtn">Place Order — ${fmt(total)}</button>
            <p class="text-xs text-muted" style="margin-top:10px;text-align:center">🔒 Your order will be saved to Firebase.</p>
          </form>
        </div>
      </div>
      <div class="summary-card">
        <h3>Order Summary</h3>
        <div class="summary-row"><span>Subtotal (original)</span><span>${fmt(orig)}</span></div>
        ${disc>0?`<div class="summary-row discount"><span>Discount</span><span>-${fmt(disc)}</span></div>`:''}
        <div class="summary-row"><span>Discounted subtotal</span><span>${fmt(sub)}</span></div>
        <div class="summary-row"><span>Delivery</span><span>${del===0?'Free':fmt(del)}</span></div>
        <div class="summary-row total"><span>Total</span><span class="val">${fmt(total)}</span></div>
      </div>
    </div>`;

  requestAnimationFrame(() => requestAnimationFrame(() => initCheckoutMap()));
};

/* ---------- MAP (MapTiler + Leaflet) with reverse geocoding ---------- */
let __checkoutMap = null;
let __checkoutMarker = null;

function __setPinnedLocation(lat, lng, source){
  const latEl = document.getElementById('deliveryLat');
  const lngEl = document.getElementById('deliveryLng');
  const srcEl = document.getElementById('deliveryLocSource');
  if(latEl) latEl.value = Number(lat).toFixed(6);
  if(lngEl) lngEl.value = Number(lng).toFixed(6);
  if(srcEl) srcEl.value = source || 'manual';

  if(__checkoutMap){
    if(__checkoutMarker){
      __checkoutMarker.setLatLng([lat, lng]);
    }else{
      __checkoutMarker = L.marker([lat, lng], { draggable: true }).addTo(__checkoutMap);
      __checkoutMarker.on('dragend', () => {
        const pos = __checkoutMarker.getLatLng();
        __setPinnedLocation(pos.lat, pos.lng, 'manual');
        // When user drags pin manually, refill address too (nice touch)
        reverseGeocodeAndFill(pos.lat, pos.lng, true);
      });
    }
  }

  const hint = document.getElementById('mapHint');
  if(hint){
    const label = source === 'gps' ? '📍 Current location' : '📍 Pinned';
    hint.textContent = `${label}: ${Number(lat).toFixed(4)}, ${Number(lng).toFixed(4)} — drag pin to adjust`;
  }
}

/* Reverse geocode using MapTiler, then fill the checkout address fields.
   Only fills fields that are EMPTY unless `overwrite` is true. */
async function reverseGeocodeAndFill(lat, lng, overwrite){
  try{
    const url = `https://api.maptiler.com/geocoding/${lng},${lat}.json?key=${encodeURIComponent(window.MAPTILER_KEY)}`;
    const res = await fetch(url);
    if(!res.ok) throw new Error('Geocoder HTTP '+res.status);
    const data = await res.json();
    const feat = (data.features && data.features[0]) || null;
    if(!feat) throw new Error('No address found');
    const ctx = feat.context || [];
    const find = (prefix) => {
      const hit = ctx.find(c => String(c.id||'').startsWith(prefix));
      return hit ? hit.text : '';
    };
    const postal = (feat.properties?.postal_code)
      || (ctx.find(c => c.id === 'postal_code')?.text)
      || '';
    const province = find('region') || find('subregion') || '';
    const city = find('place') || find('municipality') || find('locality') || '';
    const area = feat.text || feat.place_name || '';
    const landmark = (ctx.find(c => String(c.id||'').startsWith('neighbourhood'))?.text) || '';

    const form = document.getElementById('checkoutForm');
    if(!form) return;
    const setField = (name, value) => {
      const el = form.elements.namedItem(name);
      if(!el || !value) return;
      if(overwrite || !el.value) el.value = value;
    };

    // Province <select> is fixed list — try to match
    const provinceSelect = form.elements.namedItem('province');
    if(provinceSelect && province){
      const target = province.toLowerCase();
      const opts = Array.from(provinceSelect.options);
      const match = opts.find(o => o.value && target.includes(o.value.toLowerCase()))
                 || opts.find(o => o.value && o.value.toLowerCase().includes(target.split(' ')[0]));
      if(match) provinceSelect.value = match.value;
    }

    setField('city', city);
    setField('area', area);
    setField('postal', postal);
    setField('landmark', landmark);

    // Also save to a data-attr so we can show the full address text
    const fullEl = document.getElementById('resolvedAddress');
    if(fullEl) fullEl.textContent = feat.place_name || '';

    toast('Address filled from your location ✅','success');
  }catch(err){
    console.warn('Reverse geocode failed:', err);
    toast('Could not fetch address. Fill it in manually.','warn');
  }
}

function initCheckoutMap(){
  const mapEl = document.getElementById('map');
  if(!mapEl) return;

  if(!window.MAPTILER_KEY){
    mapEl.innerHTML = `<div class="map-fallback map-error">
      Map unavailable.<br>MapTiler API key missing.
    </div>`;
    const hint = document.getElementById('mapHint');
    if(hint) hint.style.display = 'none';
    return;
  }

  window.loadLeaflet().then(() => {
    const defaultCenter = [24.8607, 67.0011]; // Karachi fallback
    __checkoutMap = L.map('map', {
      center: defaultCenter,
      zoom: 12,
      zoomControl: true
    });

    L.tileLayer(
      `https://api.maptiler.com/maps/streets-v2/{z}/{x}/{y}.png?key=${encodeURIComponent(window.MAPTILER_KEY)}`,
      {
        tileSize: 512,
        zoomOffset: -1,
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> &copy; <a href="https://www.maptiler.com/copyright/">MapTiler</a>',
        crossOrigin: true,
        maxZoom: 19
      }
    ).addTo(__checkoutMap);

    __checkoutMap.on('click', (e) => {
      __setPinnedLocation(e.latlng.lat, e.latlng.lng, 'manual');
      reverseGeocodeAndFill(e.latlng.lat, e.latlng.lng, false); // fill empty fields only
    });

    const latEl = document.getElementById('deliveryLat');
    const lngEl = document.getElementById('deliveryLng');
    if (latEl && lngEl && latEl.value && lngEl.value) {
      const lat = Number(latEl.value), lng = Number(lngEl.value);
      if (Number.isFinite(lat) && Number.isFinite(lng)) {
        __checkoutMap.setView([lat, lng], 15);
        __setPinnedLocation(lat, lng, document.getElementById('deliveryLocSource')?.value || 'manual');
      }
    } else {
      autoLocateOnMapOpen();
    }

    setTimeout(() => __checkoutMap.invalidateSize(), 100);
  }).catch(err => {
    mapEl.innerHTML = `<div class="map-fallback map-error">Map failed to load: ${escapeHtml(err.message)}</div>`;
  });
}

function autoLocateOnMapOpen(){
  if(!navigator.geolocation) return;
  const hint = document.getElementById('mapHint');
  if(hint) hint.textContent = '📡 Getting your location…';

  navigator.geolocation.getCurrentPosition(
    (pos) => {
      const lat = pos.coords.latitude;
      const lng = pos.coords.longitude;
      if(__checkoutMap) __checkoutMap.setView([lat, lng], 16);
      __setPinnedLocation(lat, lng, 'gps');
      reverseGeocodeAndFill(lat, lng, false);
    },
    (err) => {
      console.warn('Auto-locate failed:', err?.message);
      if(hint) hint.textContent = 'Optional: click on the map to add a delivery pin';
    },
    { enableHighAccuracy: true, timeout: 8000, maximumAge: 60000 }
  );
}

/* ---------- SUCCESS ---------- */
Routes.success = function(el, orderId){
  const o = State.orders.find(x=>String(x.id)===String(orderId));
  if(!o){
    el.innerHTML = `<div class="empty-state"><i data-lucide="alert-circle"></i><h3>Order not found</h3><a href="#/orders" class="btn btn-primary">My Orders</a></div>`;
    return;
  }
  el.innerHTML = `<div class="success-card">
    <div class="check"><i data-lucide="check"></i></div>
    <h1>Order Placed Successfully!</h1>
    <p class="text-muted" style="margin-bottom:8px">Thank you ${escapeHtml(o.address?.name||'')}. Your order is confirmed.</p>
    <p style="margin:20px 0"><strong>Order ID:</strong> <span style="color:var(--red);font-family:monospace">${escapeHtml(o.orderNumber||o.id)}</span></p>
    <div style="display:flex;gap:10px;justify-content:center;flex-wrap:wrap">
      <a href="#/order/${o.id}" class="btn btn-primary">View Order</a>
      <a href="#/shop" class="btn btn-ghost">Continue Shopping</a>
    </div>
  </div>`;
};


/* ---------- ACCOUNT ---------- */
Routes.account=function(el){
  const p=State.userProfile||{},signed=!!State.user&&!State.user.isGuest;
  el.innerHTML=`<h1 class="page-title">My Account</h1><div class="page-card">
    <h3 style="margin-bottom:8px">${signed?'Your customer profile':'Guest customer profile'}</h3>
    <p class="text-sm text-muted" style="margin-bottom:14px">${signed?`Signed in as ${escapeHtml(State.user.email||'')}. Your orders are linked to your Firebase account.`:'You are shopping as a guest. Register or sign in to access your account from other devices.'}</p>
    <form onsubmit="event.preventDefault();App.saveGuestProfile(event)">
      <div class="field-row two"><div class="field"><label>Full name</label><input name="name" required minlength="2" value="${escapeHtml(p.name||'')}"></div>
      <div class="field"><label>Phone</label><input name="phone" required pattern="^03\\d{2}-?\\d{7}$" placeholder="03XX-XXXXXXX" value="${escapeHtml(p.phone||'')}"></div></div>
      <div class="field"><label>Email</label><input name="email" type="email" value="${escapeHtml(State.user?.email||p.email||'')}" ${signed?'readonly':''}></div>
      <button class="btn btn-primary" type="submit">Save profile</button>
    </form></div>
    <div class="page-card" style="margin-top:14px">
      <h3 style="margin-bottom:10px">Settings & Help</h3>
      <a href="#/chat" class="btn btn-primary btn-block" style="justify-content:center;margin-bottom:10px">💬 Chat with Us — Message GEN Z Admin</a>
      <p class="text-xs text-muted">Ask about orders, delivery, products or payments. You can attach photos, documents and other files.</p>
    </div>
    <div class="page-card" style="margin-top:14px;display:flex;gap:10px;flex-wrap:wrap">
      <a href="#/orders" class="btn btn-ghost">📦 My Orders (${State.orders.length})</a><a href="#/wishlist" class="btn btn-ghost">♥ Wishlist (${State.wishlist.length})</a><a href="#/notifications" class="btn btn-ghost">🔔 Notifications (${State.notifications.length})</a><a href="#/chat" class="btn btn-primary">💬 Chat with Us</a>
      ${signed?`<button class="btn btn-danger" onclick="App.logout()">Sign out</button>`:`<a href="#/login" class="btn btn-primary">Sign in</a><a href="#/register" class="btn btn-ghost">Create account</a>`}
    </div>`;
};
Routes.myReviews = function(el){
if(State.myReviews.length===0){
    el.innerHTML = `<h1 class="page-title">My Reviews</h1><div class="empty-state"><i data-lucide="star"></i><h3>No reviews yet</h3><p>Review products after your orders are delivered.</p><a href="#/orders" class="btn btn-primary">View Orders</a></div>`;
    return;
  }
  el.innerHTML = `<h1 class="page-title">My Reviews (${State.myReviews.length})</h1>
    ${State.myReviews.map(r=>{
      const p = getProduct(r.productId);
      return `<div class="page-card" style="display:flex;gap:14px;align-items:flex-start;flex-wrap:wrap">
        ${p?`<a href="#/product/${p.id}"><img src="${escapeHtml(p.image||'')}" style="width:64px;height:64px;border-radius:10px;background:var(--dark-2)"></a>`:''}
        <div style="flex:1;min-width:200px">
          <h4 style="font-size:14px">${p?escapeHtml(p.title):'(Product unavailable)'}</h4>
          <div style="color:var(--yellow);margin:4px 0">${'★'.repeat(Number(r.rating)||5)}</div>
          <p class="text-sm text-muted">${escapeHtml(r.text||'')}</p>
          <p class="text-xs text-muted" style="margin-top:6px">${r.date?new Date(r.date).toLocaleDateString():''} ${r.verified?'· ✅ Verified Purchase':''}</p>
        </div>
      </div>`;
    }).join('')}`;
};

/* ---------- FIREBASE CUSTOMER AUTH ---------- */
Routes.login=function(el){
  if(State.user&&!State.user.isGuest){el.innerHTML=`<div class="auth-card"><h1>Already signed in</h1><p class="sub">${escapeHtml(State.user.email||'')}</p><a href="#/account" class="btn btn-primary btn-block">My Account</a></div>`;return;}
  el.innerHTML=`<div class="auth-card"><h1>Welcome Back</h1><p class="sub">Sign in to view your orders and saved details.</p>
    <form onsubmit="event.preventDefault();App.login(event)"><div class="field"><label>Email address</label><input name="email" type="email" autocomplete="email" required placeholder="you@example.com"></div>
    <div class="field"><label>Password</label><input name="password" type="password" autocomplete="current-password" required minlength="6" placeholder="Your password"></div>
    <button class="btn btn-primary btn-block" type="submit" id="loginBtn">Sign In</button></form>
    <button class="btn btn-ghost btn-block" style="margin-top:8px" onclick="App.resetPassword()">Forgot password?</button>
    <p class="text-sm text-muted" style="text-align:center;margin-top:16px">New to GEN Z? <a href="#/register" style="color:var(--red)">Create an account</a></p>
    <a href="#/shop" class="text-sm text-muted" style="display:block;text-align:center;margin-top:12px">Continue as guest</a></div>`;
};
Routes.register=function(el){
  if(State.user&&!State.user.isGuest){
    el.innerHTML=`<div class="auth-card"><h1>Account already active</h1><a href="#/account" class="btn btn-primary btn-block">My Account</a></div>`;
    return;
  }
  el.innerHTML=`<div class="auth-card"><h1>Create Account</h1><p class="sub">Register securely with Firebase Authentication.</p>
    <form id="registerForm" onsubmit="App.register(event)">
      <div class="field"><label>Full name</label><input name="name" required minlength="2" autocomplete="name" placeholder="Your full name"></div>
      <div class="field"><label>Phone</label><input name="phone" required pattern="^03\\d{2}-?\\d{7}$" inputmode="tel" placeholder="03XX-XXXXXXX" title="Enter a Pakistani mobile number"></div>
      <div class="field"><label>Email address</label><input name="email" type="email" required autocomplete="email" placeholder="you@example.com"></div>
      <div class="field"><label>Password</label><input name="password" type="password" required minlength="6" autocomplete="new-password" placeholder="At least 6 characters"></div>
      <div class="field"><label>Confirm password</label><input name="confirmPassword" type="password" required minlength="6" autocomplete="new-password" placeholder="Repeat password"></div>
      <button class="btn btn-primary btn-block" type="submit" id="registerBtn">Create Account</button>
    </form>
    <p class="text-sm text-muted" style="text-align:center;margin-top:16px">Already registered? <a href="#/login" style="color:var(--red)">Sign in</a></p></div>`;
};
Routes.orders=function(el){
  if(!State.user||State.user.isGuest){el.innerHTML=`<h1 class="page-title">My Orders</h1><div class="empty-state"><h3>Sign in to view your orders</h3><a href="#/login" class="btn btn-primary">Sign In</a></div>`;return;}
  if(!State.orders.length){el.innerHTML=`<h1 class="page-title">My Orders</h1><div class="empty-state"><i data-lucide="package"></i><h3>No orders found for this account yet</h3><p>Orders placed from this browser will appear here.</p><a href="#/shop" class="btn btn-primary">Start Shopping</a></div>`;return;}
  el.innerHTML=`<h1 class="page-title">My Orders</h1>${State.orders.map(o=>{
    const canReview=o.status==='delivered'&&(o.items||[]).some(it=>!State.myReviews.some(r=>r.orderId===o.id&&String(r.productId)===String(it.productId)));
    return `<div class="order-card"><div class="head"><div><h4>${escapeHtml(o.orderNumber||o.id)}</h4><p class="date">${new Date(o.date).toLocaleDateString('en-PK',{day:'numeric',month:'short',year:'numeric'})}</p></div><span class="status-pill ${escapeHtml(o.status||'placed')}">${escapeHtml(o.status||'placed')}</span></div>
    <p class="text-sm text-muted">${(o.items||[]).length} item(s) · ${fmt(o.total)}</p>
    <div style="display:flex;gap:8px;margin-top:12px;flex-wrap:wrap"><a href="#/order/${encodeURIComponent(o.id)}" class="btn btn-sm btn-ghost">View Details</a>${canReview?`<a href="#/order/${encodeURIComponent(o.id)}" class="btn btn-sm btn-primary">⭐ Rate & Review</a>`:''}${['placed','confirmed','processing'].includes(o.status)&&Date.now()<Number(o.cancelUntil||(Number(o.createdAt||o.date||0)+24*60*60*1000))?`<button class="btn btn-sm btn-danger" onclick="App.cancelOrder('${o.id}')">Cancel (24h)</button>`:''}<button class="btn btn-sm btn-primary" onclick="App.reorder('${o.id}')">Reorder</button></div></div>`;
  }).join('')}`;
};

Routes.orderDetail = function(el, id){
  if(!State.user||State.user.isGuest){el.innerHTML=`<div class="empty-state"><h3>Sign in to view this order</h3><a href="#/login" class="btn btn-primary">Sign In</a></div>`;return;}
  const o = State.orders.find(x=>String(x.id)===String(id));
  if(!o){ el.innerHTML = `<div class="empty-state"><h3>Order not found</h3><a href="#/orders" class="btn btn-primary">My Orders</a></div>`; return; }
  const steps = ['placed','confirmed','processing','shipped','out-for-delivery','delivered'];
  const idx = steps.indexOf(o.status);
  const safeIdx=Math.max(-1,idx);
  el.innerHTML = `<div class="breadcrumb"><a href="#/orders">My Orders</a> / <span>${escapeHtml(o.orderNumber||o.id)}</span></div>
    <h1 class="page-title">Order ${escapeHtml(o.orderNumber||o.id)}</h1>
    <div class="cart-layout">
      <div>
        <div class="page-card">
          <h3 style="margin-bottom:14px">Items</h3>
          ${(o.items||[]).map(it=>{
            const p = getProduct(it.productId);
            const reviewed = State.myReviews.some(r => r.orderId === o.id && String(r.productId) === String(it.productId));
            const canReview = o.status === 'delivered' && !reviewed;
            const title=it.title||p?.title||'Product unavailable',image=it.image||p?.image||'',unitPrice=Number(it.price??p?.price??0);
            return `<div class="cart-item">${image?`<img src="${escapeHtml(image)}" onerror="this.style.opacity=0.3">`:`<div style="width:64px;height:64px;border-radius:10px;background:var(--dark-2);display:grid;place-items:center">📦</div>`}<div class="info"><h4>${escapeHtml(title)}</h4><div class="price">${fmt(unitPrice)} × ${Number(it.qty)||0}</div>
              ${canReview&&p?`<button class="btn btn-sm btn-primary" style="margin-top:6px" onclick="App.navigateReview('${p.id}','${o.id}')">⭐ Rate & Review</button>`:''}
              ${reviewed?`<p class="text-xs" style="color:var(--green);margin-top:4px">✅ Reviewed</p>`:''}
            </div><div>${fmt(unitPrice*(Number(it.qty)||0))}</div></div>`;
          }).join('')}
          <div class="summary-row"><span>Subtotal (original)</span><span>${fmt(o.originalSubtotal||0)}</span></div>
          ${o.savings>0?`<div class="summary-row discount"><span>Discount</span><span>-${fmt(o.savings)}</span></div>`:''}
          <div class="summary-row"><span>Delivery</span><span>${fmt(o.delivery||0)}</span></div>
          <div class="summary-row total"><span>Total</span><span class="val">${fmt(o.total)}</span></div>
        </div>
        <div class="page-card">
          <h3 style="margin-bottom:14px">Order Status</h3>
          <div class="timeline">
            ${steps.map((s,i)=>`<div class="timeline-step ${i<=safeIdx?'done':''}">
              <div class="dot">${i<=idx?'<i data-lucide="check"></i>':''}</div>
              <div><div class="label">${s.replace(/-/g,' ').replace(/\b\w/g,c=>c.toUpperCase())}</div>${i===idx?`<div class="time">Current</div>`:''}</div>
            </div>`).join('')}
          </div>
        </div>
      </div>
      <div class="summary-card">
        <h3>Shipping Address</h3>
        <p style="font-size:13px;margin-bottom:6px"><strong>${escapeHtml(o.address?.name||'')}</strong></p>
        <p class="text-sm text-muted">${escapeHtml(o.address?.phone||'')}</p>
        <p class="text-sm text-muted">${escapeHtml(o.address?.area||'')}, ${escapeHtml(o.address?.city||'')}, ${escapeHtml(o.address?.province||'')}</p>
        ${o.address?.lat && o.address?.lng ? `<p class="text-sm text-muted">📍 Pinned: ${Number(o.address.lat).toFixed(4)}, ${Number(o.address.lng).toFixed(4)}</p>` : ''}
        <hr style="margin:14px 0;border:none;border-top:1px solid var(--border)">
        <p class="text-sm">Payment: <strong>${o.payment==='cod'?'Cash on Delivery':'Online'}</strong></p>
        <p class="text-sm">Status: <span class="status-pill ${escapeHtml(o.status||'placed')}">${escapeHtml(String(o.status||'placed').replace(/-/g,' '))}</span></p>
      </div>
    </div>`;
};

/* ---------- NOTIFICATIONS ---------- */
Routes.notifications = function(el){
  if(!State.user||State.user.isGuest){ el.innerHTML = `<div class="empty-state"><h3>Sign in required</h3><a href="#/login" class="btn btn-primary">Sign In</a></div>`; return; }
  if(State.notifications.length===0){
    el.innerHTML = `<h1 class="page-title">Notifications</h1><div class="empty-state"><i data-lucide="bell"></i><h3>No notifications</h3><p>Order updates will appear here.</p></div>`;
    return;
  }
  el.innerHTML = `<h1 class="page-title">Notifications</h1>
    ${State.notifications.map(n=>`<div class="notif-item ${n.read?'read':''}">
      <div class="icon"><i data-lucide="${n.icon||'bell'}"></i></div>
      <div><h4>${escapeHtml(n.title||'')}</h4><p>${escapeHtml(n.message||'')}</p><div class="time">${n.date?new Date(n.date).toLocaleString('en-PK'):''}</div></div>
    </div>`).join('')}`;
};

/* ---------- BUYER / ADMIN LIVE CHAT ---------- */
let chatListenerOff=null;
Routes.chat=function(el){
  if(!State.user||State.user.isGuest){el.innerHTML=`<div class="page-card"><h2>Chat with Us</h2><p>Please sign in to chat with GEN Z support and share files.</p><a class="btn btn-primary" href="#/login">Sign in</a></div>`;return;}
  const uid=State.user.uid;
  el.innerHTML=`<h1 class="page-title">Chat with Us</h1><div class="page-card">
    <p class="text-sm text-muted" style="margin-bottom:12px">Chat directly with GEN Z Admin. You can send messages and attachments.</p>
    <div id="buyerChatMessages" style="height: min(55vh,480px);overflow:auto;background:var(--dark-2);border:1px solid var(--border);border-radius:12px;padding:12px;margin-bottom:12px">Loading conversation…</div>
    <form id="buyerChatForm" onsubmit="event.preventDefault();App.sendChatMessage(event)">
      <div class="field"><label>Message</label><textarea name="message" rows="3" placeholder="Write a message to GEN Z Admin…" maxlength="4000"></textarea><p class="text-xs text-muted">You can send text with an attachment or send a file by itself.</p></div>
      <div class="field"><label>📎 Photos / Files (up to 15 MB)</label><input type="file" name="attachment" accept="image/*,application/pdf,video/mp4,video/webm,.doc,.docx,.xls,.xlsx"></div>
      <button class="btn btn-primary btn-block" type="submit" id="buyerChatSend">➤ Send message / file</button>
    </form></div>`;
  if(chatListenerOff){chatListenerOff();chatListenerOff=null;}
  chatListenerOff=onValue(ref(db,'chats/'+uid+'/messages'),snap=>{
    const box=document.getElementById('buyerChatMessages');if(!box)return;
    const msgs=snap.exists()?Object.keys(snap.val()).map(k=>({id:k,...snap.val()[k]})).sort((a,b)=>Number(a.timestamp||0)-Number(b.timestamp||0)):[];
    box.innerHTML=msgs.length?msgs.map(m=>`<div style="margin:8px 0;display:flex;justify-content:${m.sender==='buyer'?'flex-end':'flex-start'}"><div style="max-width:85%;background:${m.sender==='buyer'?'rgba(225,29,72,.2)':'var(--dark)'};border:1px solid var(--border);border-radius:12px;padding:10px"><div class="text-xs text-muted">${m.sender==='buyer'?'You':'GEN Z Admin'} · ${m.timestamp?new Date(m.timestamp).toLocaleString():''}</div>${m.message?`<p style="white-space:pre-wrap;overflow-wrap:anywhere">${escapeHtml(m.message)}</p>`:''}${m.fileUrl?`<a class="btn btn-sm btn-ghost" href="${escapeHtml(m.fileUrl)}" target="_blank" rel="noopener">📎 ${escapeHtml(m.fileName||'Open attachment')}</a>`:''}</div></div>`).join(''):'<p class="text-sm text-muted">No messages yet. Send a message to start the chat.</p>';
    box.scrollTop=box.scrollHeight;
  },err=>{const box=document.getElementById('buyerChatMessages');if(box)box.textContent='Chat access error: '+(err.message||'Check Firebase Realtime Database rules.');});
};

/* ---------- SUPPORT / 404 ---------- */
Routes.support = function(el){
  el.innerHTML = `<h1 class="page-title">Support & Policies</h1>
    <div class="page-card policy-content">
      <h2 id="faq">FAQs</h2>
      <h3>How do I place an order?</h3><p>Browse products, add to cart, and checkout. You can pay cash on delivery.</p>
      <h3>Do you deliver across Pakistan?</h3><p>Yes — we deliver to all major cities. Delivery fee is flat Rs. 250.</p>
      <h2 id="shipping">Shipping Policy</h2><p>Standard delivery 3-7 business days. Remote areas may take longer.</p>
      <h2 id="returns">Return & Refund Policy</h2><p>7-day returns on unused items in original packaging. Refund processed within 5-7 business days after inspection.</p>
      <h2 id="privacy">Privacy Policy</h2><p>We collect only the information needed to fulfil your orders. Your data is never sold to third parties.</p>
      <h2 id="terms">Terms & Conditions</h2><p>By shopping with GEN Z you agree to our terms. Prices are in PKR and may change without notice.</p>
    </div>`;
};
Routes.notfound = function(el){
  el.innerHTML = `<div class="empty-state" style="min-height:60vh">
    <div style="font-size:80px;font-weight:900;color:var(--red);font-style:italic">404</div>
    <h3>Page not found</h3><p>The page you're looking for doesn't exist.</p>
    <a href="#/" class="btn btn-primary">Go Home</a>
  </div>`;
};

/* ---------- APP ACTIONS ---------- */
const App = {
  currentQty: 1, currentColor: null, currentProductId: null,
  async shareProduct(pid){
    const p=getProduct(pid); if(!p){toast('Product unavailable','error');return;}
    const url=new URL('#/product/'+encodeURIComponent(p.id),location.href).href;
    try{if(navigator.share) await navigator.share({title:p.title||'GEN Z product',text:'Check out this product at GEN Z Store',url});
    else if(navigator.clipboard?.writeText){await navigator.clipboard.writeText(url);toast('Product link copied!','success');}
    else prompt('Copy product link:',url);}catch(err){if(err?.name!=='AbortError')toast('Could not share product link','error');}
  },
  async downloadProductImage(pid){
    const p=getProduct(pid);if(!p?.image){toast('Product image unavailable','error');return;}
    try{const response=await fetch(p.image,{mode:'cors'});if(!response.ok)throw new Error('Image download failed');
      const blob=await response.blob(),objectUrl=URL.createObjectURL(blob),a=document.createElement('a');
      a.href=objectUrl;a.download=(String(p.title||'GENZ-product').replace(/[^a-z0-9-_]/gi,'_')+'.'+((blob.type.split('/')[1]||'jpg').replace('jpeg','jpg')));
      document.body.appendChild(a);a.click();a.remove();URL.revokeObjectURL(objectUrl);toast('Product image downloaded','success');
    }catch(err){window.open(p.image,'_blank','noopener');toast('Image opened in new tab; direct download may be blocked by its host','warn');}
  },

  async sendChatMessage(e){
    if(!State.user||State.user.isGuest){toast('Sign in to chat','warn');return;}
    const form=e?.target||document.getElementById('buyerChatForm'),message=String(form?.elements.message.value||'').trim(),file=form?.elements.attachment.files?.[0];
    if(!message&&!file){toast('Write a message or attach a file.','warn');return;}
    const btn=document.getElementById('buyerChatSend');if(btn){btn.disabled=true;btn.textContent='Sending…';}
    try{
      let fileUrl='',fileName='',fileType='';
      if(file){
        const allowed=['image/jpeg','image/png','image/webp','image/gif','application/pdf','video/mp4','video/webm','application/msword','application/vnd.openxmlformats-officedocument.wordprocessingml.document','application/vnd.ms-excel','application/vnd.openxmlformats-officedocument.spreadsheetml.sheet'];
        if(file.size>15*1024*1024)throw new Error('File limit is 15 MB.');
        if(file.type&&!allowed.includes(file.type))throw new Error('File type not supported. Send an image, PDF, video, Word or Excel file.');
        const safeName=file.name.replace(/[^a-zA-Z0-9._-]/g,'_'),path='chatAttachments/'+State.user.uid+'/'+Date.now()+'_'+safeName;
        const snap=await uploadBytes(storageRef(firebaseStorage,path),file,{contentType:file.type||'application/octet-stream'});
        fileUrl=await getDownloadURL(snap.ref);fileName=file.name;fileType=file.type||'application/octet-stream';}
      const msgRef=push(ref(db,'chats/'+State.user.uid+'/messages'));
      await set(msgRef,{sender:'buyer',userId:State.user.uid,message,fileUrl,fileName,fileType,timestamp:Date.now(),readByAdmin:false});
      form.elements.message.value='';form.elements.attachment.value='';toast('Message sent','success');
    }catch(err){console.error(err);toast('Message could not be sent: '+(err.message||'Check Firebase rules'),'error');}
    finally{if(btn){btn.disabled=false;btn.textContent='Send message / file';}}
  },
  toggleMobileNav(){
    const nav = document.getElementById('mobileNav');
    const bd = document.getElementById('mobileNavBackdrop');
    if(!nav) return;
    const open = nav.classList.toggle('open');
    nav.setAttribute('aria-hidden', !open);
    if(bd) bd.classList.toggle('show', open);
  },


  async handleWishlist(id, btn){
    const added = await toggleWishlist(id);
    if(btn) btn.classList.toggle('active', added);
  },

  handleAddToCart(id, qty, color){
    if(addToCart(id, qty, color)){
      toast('Added to cart','success');
      if(State.user&&!State.user.isGuest){ set(ref(db,'users/'+State.user.uid+'/cart'), State.cart).catch(()=>{}); }
    }
  },

  changeImage(el, src){
    document.querySelectorAll('.gallery-thumbs .thumb').forEach(t=>t.classList.remove('active'));
    el.classList.add('active');
    const img = document.getElementById('mainImage');
    if(img) img.src = src;
  },

  openImageViewer(src){
    const v = document.getElementById('imageViewer');
    const img = document.getElementById('imageViewerImg');
    if(v && img && src){ img.src = src; v.classList.add('show'); }
  },
  closeImageViewer(){
    const v = document.getElementById('imageViewer');
    if(v) v.classList.remove('show');
  },

  openVideo(url){
    const modal = document.getElementById('videoModal');
    const player = document.getElementById('videoPlayer');
    if(modal && player){
      player.src = url;
      modal.classList.add('show');
      player.play().catch(()=>{});
    }
  },
  closeVideo(){
    const modal = document.getElementById('videoModal');
    const player = document.getElementById('videoPlayer');
    if(modal && player){
      modal.classList.remove('show');
      player.pause();
      player.src = '';
    }
  },

  changeQty(d){
    App.currentQty = Math.max(1, App.currentQty + d);
    const el = document.getElementById('qtyDisplay');
    if(el) el.textContent = App.currentQty;
  },

  selectColor(btn, hex){
    document.querySelectorAll('.color-dot').forEach(b=>b.classList.remove('active'));
    btn.classList.add('active');
    App.currentColor = hex;
    const t = document.getElementById('selectedColorText');
    if(t) t.textContent = hex;
  },

  switchTab(btn, tabId){
    document.querySelectorAll('.tab-item').forEach(t=>t.classList.remove('active'));
    document.querySelectorAll('.tab-pane').forEach(p=>p.classList.remove('active'));
    btn.classList.add('active');
    const pane = document.getElementById(tabId);
    if(pane) pane.classList.add('active');
  },

  cartQty(pid, color, delta){
    updateCartQty(pid, color||null, delta);
    mount();
    if(State.user&&!State.user.isGuest){ set(ref(db,'users/'+State.user.uid+'/cart'), State.cart).catch(()=>{}); }
  },

  removeCartItem(pid, color){
    removeFromCart(pid, color||null);
    toast('Item removed','warn');
    mount();
    if(State.user&&!State.user.isGuest){ set(ref(db,'users/'+State.user.uid+'/cart'), State.cart).catch(()=>{}); }
  },

  clearCart(){
    if(!confirm('Clear your entire cart?')) return;
    State.cart = []; persistLocal(); updateBadges(); mount();
    if(State.user&&!State.user.isGuest){ set(ref(db,'users/'+State.user.uid+'/cart'), []).catch(()=>{}); }
    toast('Cart cleared','warn');
  },

  buyNow(pid){
    const p = getProduct(pid);
    if(!p || p.stock===0) return;
    if(!addToCart(pid, App.currentQty, App.currentColor)) return;
    if(State.user&&!State.user.isGuest){ set(ref(db,'users/'+State.user.uid+'/cart'), State.cart).catch(()=>{}); }
    navigate('#/checkout');
  },

  submitSearch(inputId){
    const input = document.getElementById(inputId || 'searchPageInput');
    const q = (input?input.value:'').trim();
    if(!q) return;
    navigate('#/search?q='+encodeURIComponent(q));
  },

  changeSort(val){
    const {params} = parseHash();
    params.sort = val;
    navigate('#/shop?'+new URLSearchParams(params).toString());
  },

  applyShopFilter(){
    const {params} = parseHash();
    const fMin = document.getElementById('fMin');
    const fMax = document.getElementById('fMax');
    const fStock = document.getElementById('fStock');
    const cats = Array.from(document.querySelectorAll('[data-fcat]:checked')).map(x=>x.value);
    const brands = Array.from(document.querySelectorAll('[data-fbrand]:checked')).map(x=>x.value);
    if(cats.length) params.cat = cats[0]; else delete params.cat;
    if(fMin&&fMin.value) params.min = fMin.value; else delete params.min;
    if(fMax&&fMax.value) params.max = fMax.value; else delete params.max;
    if(fStock&&fStock.checked) params.stock = '1'; else delete params.stock;
    if(brands.length) params.brand = brands.join(','); else delete params.brand;
    navigate('#/shop?'+new URLSearchParams(params).toString());
  },

  removeChip(key){
    const {params} = parseHash();
    if(key==='cat') delete params.cat;
    else if(key==='min') delete params.min;
    else if(key==='max') delete params.max;
    else if(key==='stock') delete params.stock;
    else if(key.startsWith('brand-')){
      const b = key.replace('brand-','');
      const brands = (params.brand||'').split(',').filter(x=>x && x!==b);
      if(brands.length) params.brand = brands.join(','); else delete params.brand;
    }
    navigate('#/shop?'+new URLSearchParams(params).toString());
  },

  clearFilters(){ navigate('#/shop'); },

  async login(e){
    if(!e)return;const f=e.target,email=formValue(f,'email').trim(),password=formValue(f,'password'),btn=document.getElementById('loginBtn');
    if(btn){btn.disabled=true;btn.textContent='Signing in…';}
    try{await signInWithEmailAndPassword(auth,email,password);toast('Signed in successfully.','success');const next=Storage.get('returnTo','#/account');Storage.remove('returnTo');navigate(next||'#/account');}
    catch(err){toast(authErrorMessage(err),'error');if(btn){btn.disabled=false;btn.textContent='Sign In';}}
  },
  async register(e){
    if(e && typeof e.preventDefault==='function') e.preventDefault();
    const f = e?.currentTarget?.tagName==='FORM'
      ? e.currentTarget
      : (e?.target?.closest?.('form') || document.getElementById('registerForm'));
    if(!f){toast('Registration form was not found. Please refresh and try again.','error');return;}
    if(!f.reportValidity()) return;

    const name=formValue(f,'name').trim();
    const phone=formValue(f,'phone').trim();
    const email=formValue(f,'email').trim().toLowerCase();
    const password=formValue(f,'password');
    const confirm=formValue(f,'confirmPassword');
    const btn=f.querySelector('#registerBtn');

    if(name.length<2){toast('Enter your full name.','error');return;}
    if(!/^03\d{2}-?\d{7}$/.test(phone)){toast('Enter a valid Pakistani mobile number (e.g. 03001234567).','error');return;}
    if(password!==confirm){toast('Passwords do not match.','error');return;}
    if(password.length<6){toast('Password must contain at least 6 characters.','error');return;}
    if(btn){btn.disabled=true;btn.textContent='Creating account…';}

    let cred;
    try{
      cred=await createUserWithEmailAndPassword(auth,email,password);
    }catch(err){
      console.error('Firebase Authentication registration failed:',err);
      toast(authErrorMessage(err),'error');
      if(btn){btn.disabled=false;btn.textContent='Create Account';}
      return;
    }

    // Auth creation has succeeded. A profile-write permission error must not
    // be reported as if the Auth account itself failed to register.
    try{await updateProfile(cred.user,{displayName:name});}
    catch(profileAuthErr){console.warn('Auth display-name update failed:',profileAuthErr);}

    const profile={uid:cred.user.uid,name,phone,email,createdAt:Date.now(),updatedAt:Date.now()};
    State.user={uid:cred.user.uid,email:cred.user.email||email,isGuest:false,displayName:name};
    State.userProfile=profile;

    let profileSaved=true;
    try{await set(ref(db,'users/'+cred.user.uid),profile);}
    catch(dbErr){
      profileSaved=false;
      console.error('Account created, but Realtime Database profile could not be saved:',dbErr);
    }

    const next=Storage.get('returnTo','#/account');
    Storage.remove('returnTo');
    if(profileSaved) toast('Account created successfully.','success');
    else toast('Account created, but profile sync failed. Check Database Rules / permissions.','warn');
    navigate(next||'#/account');
  },
  async resetPassword(){const email=prompt('Enter the email address registered with GEN Z:');if(!email)return;try{await sendPasswordResetEmail(auth,email.trim());toast('Password reset email sent. Check your inbox.','success');}catch(err){toast(authErrorMessage(err),'error');}},
  async logout(){try{await signOut(auth);toast('You have signed out.','success');navigate('#/');}catch(err){toast(authErrorMessage(err),'error');}},
  async saveGuestProfile(e){
    const f=e.target,name=formValue(f,'name').trim(),phone=formValue(f,'phone').trim(),email=State.user?.email||formValue(f,'email').trim();
    if(!name||!/^03\d{2}-?\d{7}$/.test(phone)){toast('Enter a name and valid Pakistani phone number.','error');return;}
    const profile={...(State.userProfile||{}),name,phone,email,updatedAt:Date.now()};
    try{if(State.user&&!State.user.isGuest)await update(ref(db,'users/'+State.user.uid),{...profile,uid:State.user.uid});State.userProfile=profile;Storage.set('guestProfile',profile);toast('Customer profile saved.','success');mount();}
    catch(err){toast('Could not save profile: '+authErrorMessage(err),'error');}
  },
  async updatePhone(e){
    const phone = e.target.phone.value.trim();
    if(!/^03\d{2}-?\d{7}$/.test(phone)){ toast('Invalid phone format','error'); return; }
    try{
      await update(ref(db,'users/'+State.user.uid), { phone });
      State.userProfile = { ...(State.userProfile||{}), phone }; Storage.set('guestProfile',State.userProfile);
      toast('Phone updated','success');
    }catch(err){ toast('Failed: '+err.message,'error'); }
  },

  async addAddress(){
    if(!State.user||State.user.isGuest){ toast('Sign in first','error'); navigate('#/login'); return; }
    const name = prompt('Full name:'); if(!name) return;
    const phone = prompt('Phone (03XX-XXXXXXX):') || '';
    const province = prompt('Province:') || 'Sindh';
    const city = prompt('City:') || '';
    const area = prompt('Area/Street:') || '';
    const key = push(ref(db,'users/'+State.user.uid+'/addresses')).key;
    const addr = { id:key, name, phone, province, city, area, postal:'', isDefault: State.addresses.length===0 };
    try{
      await set(ref(db,'users/'+State.user.uid+'/addresses/'+key), addr);
      State.addresses.push(addr);
      toast('Address added','success');
      mount();
    }catch(e){ toast('Failed: '+e.message,'error'); }
  },


  async setDefaultAddress(id){
    if(!State.user||State.user.isGuest) return;
    const updates = {};
    State.addresses.forEach(a=>{ updates['users/'+State.user.uid+'/addresses/'+a.id+'/isDefault'] = (a.id===id); });
    await update(ref(db), updates);
    State.addresses.forEach(a=>a.isDefault = (a.id===id));
    mount();
  },

  async deleteAddress(id){
    if(!State.user||State.user.isGuest) return;
    if(!confirm('Delete this address?')) return;
    await remove(ref(db,'users/'+State.user.uid+'/addresses/'+id));
    State.addresses = State.addresses.filter(a=>a.id!==id);
    mount();
  },

  async placeOrder(e){
    if(!State.user||State.user.isGuest){Storage.set('returnTo','#/checkout');toast('Please sign in before placing an order.','warn');navigate('#/login');return;}
    if(State.placingOrder){toast('Order is already being placed…','warn');return;}
    const f=e?.target;
    const name=formValue(f,'name').trim(), phone=formValue(f,'phone').trim();
    const province=formValue(f,'province'), city=formValue(f,'city').trim(), area=formValue(f,'area').trim();
    const postal=formValue(f,'postal').trim(), landmark=formValue(f,'landmark').trim();
    const lat=formValue(f,'lat').trim(), lng=formValue(f,'lng').trim(), notes=formValue(f,'notes').trim();
    const payment=formValue(f,'payment');
    if(payment==='cod'&&State.settings.codEnabled===false){toast('Cash on Delivery is currently disabled.','error');return;}
    if(!name||!phone||!province||!city||!area){toast('Please fill required fields','error');return;}
    if(!/^03\d{2}-?\d{7}$/.test(phone)){toast('Invalid Pakistani phone number','error');return;}
    if(!State.cart.length){toast('Cart is empty','error');return;}

    // Persist one request ID and immutable checkout payload before any inventory/order write.
    // Refreshes/retries reuse this payload; the database order path is deterministic.
    const requestStorageKey='checkoutRequest:'+State.user.uid;
    let request=Storage.get(requestStorageKey,null);
    if(!request||!request.requestId||request.uid!==State.user.uid){
      const requestId=(window.crypto?.randomUUID?crypto.randomUUID():Date.now().toString(36)+Math.random().toString(36).slice(2)).replace(/[^A-Za-z0-9_-]/g,'');
      const orderItems=State.cart.map(it=>{
        const p=getProduct(it.productId); if(!p) return null;
        const offer=activeOfferForProduct(p.id);
        return cleanForFirebase({productId:it.productId,productDbKey:p._dbKey||p.id,title:p.title,qty:Math.max(1,Number(it.qty)||1),color:it.color??null,price:effectivePrice(p),finalPrice:effectivePrice(p),originalPrice:offer?Number(offer.originalPrice||p.price):Number(p.price||0),image:p.image||'',discountId:offer?.id??null,sku:p.sku||''});
      });
      if(orderItems.some(x=>!x)){toast('Some items are unavailable. Please refresh your cart.','error');return;}
      for(const it of orderItems){const p=getProduct(it.productId);if(!p||Number(p.stock)<it.qty){toast('Some items are out of stock','error');return;}}
      const subtotal=orderItems.reduce((s,i)=>s+i.price*i.qty,0);
      const originalSubtotal=orderItems.reduce((s,i)=>s+i.originalPrice*i.qty,0);
      const savings=Math.max(0,originalSubtotal-subtotal);
      const threshold=Number(State.settings?.freeDeliveryThreshold||0);
      const delivery=(threshold>0&&subtotal>=threshold)?0:Number(State.settings?.deliveryFee??ENV.STORE.deliveryFee);
      const customerProfile={name,phone,email:State.user?.email||State.userProfile?.email||''};
      const now=Date.now();
      const order={
        id:'', checkoutRequestId:requestId, date:now, createdAt:now,
        orderNumber:'',
        customerName:name,phone,email:customerProfile.email,userId:State.user.uid,userEmail:customerProfile.email,
        items:orderItems,subtotal,originalSubtotal,savings,delivery,total:subtotal+delivery,
        status:'placed',payment,paymentMethod:payment,
        cancelUntil:now+(24*60*60*1000),
        address:{name,phone,province,city,area,address:area,postal,landmark,lat:lat?Number(lat):null,lng:lng?Number(lng):null,locationSource:formValue(f,'locSource')||'manual',addressConfirmed:!!(lat&&lng)},
        notes,statusHistory:[{status:'placed',at:now}]
      };
      request={uid:State.user.uid,requestId,order,customerProfile,createdAt:now};
      Storage.set(requestStorageKey,request);
    }
    const {requestId,order,customerProfile}=request;
    if(request.uid!==State.user.uid){toast('Checkout request belongs to another account.','error');return;}
    if(!order.orderNumber){
      try{
        const seqRef=ref(db,'counters/orderSequence');
        const seqResult=await runTransaction(seqRef,current=>Number(current||0)+1);
        if(!seqResult.committed)throw new Error('Could not allocate order number');
        order.orderNumber='GZ-A1901-'+String(seqResult.snapshot.val());
        request.order=order;Storage.set(requestStorageKey,request);
      }catch(seqErr){console.error(seqErr);toast('Could not generate order number. Check Firebase database rules.','error');return;}
    }
    State.placingOrder=true;
    const btn=document.getElementById('placeOrderBtn');
    if(btn){btn.disabled=true;btn.textContent='Placing order…';}

    const orderPath='orders/'+State.user.uid+'_'+requestId;
    order.id=State.user.uid+'_'+requestId;
    const productDbPath=it=>'products/'+String(it.productDbKey||it.productId);
    try{
      try{await update(ref(db,'users/'+State.user.uid),cleanForFirebase({...customerProfile,uid:State.user.uid,guest:false,lastOrderAt:Date.now()}));}
      catch(profileErr){console.warn('Order profile sync skipped:',profileErr);}

      // Per-product transaction records this checkout request alongside the stock decrement.
      // Re-running the same request cannot deduct stock twice. Do not rollback on uncertain
      // network outcomes: the request marker and deterministic order key make safe recovery possible.
      for(const it of order.items){
        const pRef=ref(db,productDbPath(it));
        const tx=await runTransaction(pRef,current=>{
          if(!current)return;
          const applied=current.checkoutStockRequests||{};
          if(applied[requestId]===true)return;
          const stock=Number(current.stock);
          if(!Number.isFinite(stock)||stock<it.qty)return;
          return {...current,stock:stock-it.qty,checkoutStockRequests:{...applied,[requestId]:true}};
        },{applyLocally:false});
        const latest=tx.snapshot?.val();
        if(!tx.committed && latest?.checkoutStockRequests?.[requestId]!==true){
          const available=Number(latest?.stock);
          if(!latest)throw new Error('Product record was not found in Firebase ('+it.productId+').');
          if(!Number.isFinite(available)||available<it.qty)throw new Error('Insufficient stock for '+it.title+'. Available: '+(Number.isFinite(available)?available:0)+', required: '+it.qty+'.');
          throw new Error('Stock transaction was not committed for '+it.title+'. Check database permissions.');
        }
      }

      // Atomic transaction at a fixed order path: repeated requests converge on the same record.
      const orderRef=ref(db,orderPath);
      const orderTx=await runTransaction(orderRef,current=>{
        if(current){
          if(current.checkoutRequestId===requestId&&String(current.userId)===String(State.user.uid))return;
          throw new Error('Order key collision; checkout stopped for safety.');
        }
        return cleanForFirebase(order);
      },{applyLocally:false});
      const saved=orderTx.snapshot?.val();
      if(!saved||saved.checkoutRequestId!==requestId||String(saved.userId)!==String(State.user.uid)){
        // A transaction may report not-committed for an already existing matching record.
        const verified=await get(orderRef);
        const existing=verified.val();
        if(!existing||existing.checkoutRequestId!==requestId||String(existing.userId)!==String(State.user.uid)){
          throw new Error('Could not confirm this order in Firebase. Keep this checkout request and retry; do not start a new checkout.');
        }
      }
      const confirmed=saved&&saved.checkoutRequestId===requestId?saved:(await get(orderRef)).val();
      (confirmed?.items||order.items).forEach(it=>{const product=getProduct(it.productId);if(product){const marker=product.checkoutStockRequests||{};if(marker[requestId]!==true){product.stock=Math.max(0,Number(product.stock||0)-Number(it.qty||0));product.checkoutStockRequests={...marker,[requestId]:true};}}});
      try{
        const notifRef=ref(db,'notifications/'+State.user.uid+'/'+requestId);
        await runTransaction(notifRef,current=>current||{icon:'package',title:'Order Placed',message:`Your order ${order.orderNumber||order.id} has been placed successfully.`,date:Date.now(),read:false},{applyLocally:false});
      }catch(notifErr){console.warn('Order saved, but notification could not be created:',notifErr);}
      State.orders=State.orders.filter(o=>String(o.id)!==String(order.id));
      State.orders.unshift(confirmed||order);
      State.cart=[];Storage.remove(requestStorageKey);persistLocal();updateBadges();
      try{await set(ref(db,'users/'+State.user.uid+'/cart'),[]);}catch(cartErr){console.warn('Order confirmed; remote cart clear failed:',cartErr);}
      toast('Order placed!','success');navigate('#/success/'+order.id);
    }catch(err){
      console.error('GEN Z checkout/order submission failed:',{code:err?.code||'',message:err?.message||String(err),error:err});
      const detail=err?.code==='PERMISSION_DENIED'||String(err?.message||'').toLowerCase().includes('permission')
        ?'Firebase permission denied. Check authenticated writes for order and product inventory paths.'
        :(err?.message||'Unknown error. Check the browser console for details.');
      toast('Order not confirmed: '+detail+' Retry will use the same checkout request.','error');
      // Keep the request ID/payload durable. Unlock UI for a deliberate retry of the same request.
      if(btn){btn.disabled=false;btn.textContent='Retry Same Order — '+fmt(order.total);}
    }finally{State.placingOrder=false;}
  },

useCurrentLocation(){
  if(!navigator.geolocation){
    toast('Geolocation is not supported by this browser.','error');
    return;
  }
  const btn = document.getElementById('btnUseLocation');
  if(btn){ btn.disabled = true; btn.textContent = 'Locating…'; }
  const hint = document.getElementById('mapHint');
  if(hint) hint.textContent = '📡 Getting your location…';

  navigator.geolocation.getCurrentPosition(
    async (pos) => {
      const lat = pos.coords.latitude;
      const lng = pos.coords.longitude;
      if(__checkoutMap) __checkoutMap.setView([lat, lng], 16);
      __setPinnedLocation(lat, lng, 'gps');
      if(btn){ btn.disabled = false; btn.innerHTML = '<i data-lucide="locate-fixed"></i> Use current location'; refreshIcons(); }
      // Force-overwrite address fields with the true GPS address
      await reverseGeocodeAndFill(lat, lng, true);
    },
    (err) => {
      if(btn){ btn.disabled = false; btn.innerHTML = '<i data-lucide="locate-fixed"></i> Use current location'; refreshIcons(); }
      const msgs = {
        1: 'Permission denied. Enable location access in your browser settings.',
        2: 'Location unavailable. Try again or pin manually.',
        3: 'Timed out while locating. Try again or pin manually.'
      };
      toast(msgs[err?.code] || 'Could not get your location.','error');
      if(hint) hint.textContent = 'Optional: click on the map to add a delivery pin';
    },
    { enableHighAccuracy: true, timeout: 10000, maximumAge: 0 }
  );
},
  async cancelOrder(id){
    const o=State.orders.find(x=>String(x.id)===String(id));
    if(!o||!State.user||State.user.isGuest||String(o.userId)!==String(State.user.uid)){
      toast('You can only cancel your own order.','error');return;
    }
    if(!['placed','confirmed','processing'].includes(String(o.status||'').toLowerCase())){
      toast('This order can no longer be cancelled.','error');return;
    }
    const createdAt=Number(o.createdAt||o.date||0);
    if(!createdAt||Date.now()>=Number(o.cancelUntil||(createdAt+24*60*60*1000))){
      toast('Cancellation is available only during the first 24 hours after placing the order.','warn');return;
    }
    if(!confirm('Cancel this order?'))return;

    try{
      // Claim cancellation once to prevent duplicate inventory restoration.
      const tx=await runTransaction(ref(db,'orders/'+o.id),current=>{
        if(!current||String(current.userId)!==String(State.user.uid)||
          !['placed','confirmed','processing'].includes(String(current.status||'').toLowerCase())||Date.now()>=Number(current.cancelUntil||(Number(current.createdAt||current.date||0)+24*60*60*1000))) return;
        return {...current,status:'cancelled',statusHistory:[...(Array.isArray(current.statusHistory)?current.statusHistory:[]),{status:'cancelled',at:Date.now()}]};
      },{applyLocally:false});

      if(!tx.committed){
        toast('This order has already changed and cannot be cancelled.','warn');
        return;
      }

      // Restore each product separately; do not transact on the entire
      // /products collection, which requires broad parent-level permission.
      const failedItems=[];
      for(const it of (o.items||[])){
        const productId=String(it.productId||'');
        const productDbKey=String(it.productDbKey||getProduct(productId)?._dbKey||productId);
        const qty=Math.max(0,Number(it.qty)||0);
        if(!productId||!productDbKey||qty<=0) continue;
        try{
          const stockTx=await runTransaction(ref(db,'products/'+productDbKey),current=>{
            if(!current)return;
            return {...current,stock:(Number(current.stock)||0)+qty};
          },{applyLocally:false});
          if(!stockTx.committed) failedItems.push(productId);
          else{
            const localProduct=getProduct(productId);
            if(localProduct)localProduct.stock=(Number(localProduct.stock)||0)+qty;
          }
        }catch(stockErr){
          console.error('Stock restoration failed for product '+productId,stockErr);
          failedItems.push(productId);
        }
      }

      o.status='cancelled';
      if(failedItems.length){
        console.error('Inventory reconciliation required for product IDs:',failedItems);
        toast('Order cancelled, but some stock could not be restored. Admin must reconcile inventory.','error');
      }else{
        toast('Order cancelled and stock restored.','success');
      }

      try{
        const nr=push(ref(db,'notifications/'+State.user.uid));
        await set(nr,{icon:'x-circle',title:'Order Cancelled',message:`Your order ${o.orderNumber||o.id} has been cancelled.`,date:Date.now(),read:false});
      }catch(notifErr){console.warn('Cancellation notification failed:',notifErr);}
      mount();
    }catch(err){
      console.error('Order cancellation failed:',err);
      toast('Could not cancel order: '+(err?.message||'Unknown error'),'error');
    }
  },
  reorder(id){
    const o = State.orders.find(x=>String(x.id)===String(id));
    if(!o) return;
    let added = 0;
    o.items.forEach(it=>{ if(addToCart(it.productId, it.qty, it.color)) added++; });
    if(added){ toast(`${added} item(s) added to cart`,'success'); navigate('#/cart'); }
    else toast('Items unavailable','error');
  },

  navigateReview(pid, oid){
    navigate('#/product/'+pid);
    // The review form will detect eligibility on render using getUserEligibleReviewItems()
  },

  async submitReview(e, pid, orderId){
    if(!State.user||State.user.isGuest){ toast('Sign in to review','error'); navigate('#/login'); return; }
    const form = e.target;
    const rating = Number(form.rating.value);
    const review = form.review.value.trim();
    if(review.length < 10){ toast('Review must be at least 10 characters','error'); return; }
    if(!orderId){ toast('Missing order reference','error'); return; }

    // Verify ownership + delivered status + item in order
    const order = State.orders.find(o => String(o.id) === String(orderId));
    if (!order) { toast('Order not found','error'); return; }
    if (order.status !== 'delivered') { toast('You can only review delivered orders','error'); return; }
    const itemInOrder = (order.items||[]).some(it => String(it.productId) === String(pid));
    if (!itemInOrder) { toast('This product is not in that order','error'); return; }
    const already = State.myReviews.some(r => r.orderId === orderId && String(r.productId) === String(pid));
    if (already) { toast('You already reviewed this item','warn'); return; }

    try{
      const rRef = push(ref(db,'reviews/'+pid));
      const reviewObj = {
        name: State.userProfile?.name || 'Guest Customer',
        uid: State.user.uid,
        rating, text: review, date: Date.now(),
        orderId, verified: true
      };
      await set(rRef, reviewObj);
      State.myReviews.push({ id: rRef.key, productId: pid, ...reviewObj });

      const p = getProduct(pid);
      if(p){
        const newCount = Number(String(p.reviews).replace(/\D/g,''))||0;
        const newRating = ((p.rating*newCount) + rating) / (newCount+1);
        await update(ref(db,'products/'+(p._dbKey||pid)), {
          rating: Math.round(newRating*10)/10,
          reviews: String(newCount + 1)
        });
        p.rating = Math.round(newRating*10)/10;
        p.reviews = String(newCount + 1);
      }
      toast('Review submitted!','success');
      form.reset();
      mount();
    }catch(err){ toast('Failed: '+err.message,'error'); }
  },

  heroNav(dir){heroAdvance(dir);},
  heroGoTo(i){const n=State.banners.filter(bannerIsActive).length;if(!n)return;heroSlideIndex=((Number(i)||0)%n+n)%n;updateHeroSlide();},

  toast,
};

window.App = App;
window.App.State = State;
window.App.ENV = ENV;

/* ---------- BOOT: AUTH + PRODUCT DATA START INDEPENDENTLY ---------- */
async function boot(){
  if(!location.hash) location.hash='#/';

  let productsUnsubscribe=null;
  let userDataUnsubs=[];
  let authChangeVersion=0;
  let staticLoadsStarted=false;

  const logBoot=(message,details)=>{
    if(details!==undefined) console.info('[GEN Z boot] '+message,details);
    else console.info('[GEN Z boot] '+message);
  };

  const clearUserDataListeners=()=>{
    userDataUnsubs.forEach(unsub=>{try{unsub();}catch(err){console.warn('[GEN Z] Listener cleanup failed:',err);}});
    userDataUnsubs=[];
  };

  const maybeRenderInitialPage=()=>{
    if(State.authReady && State.productsReady && !State.ready){
      State.ready=true;
      logBoot('Initial data ready; rendering application.',{
        authenticated:!State.user?.isGuest,
        products:State.products.length
      });
      mount();
      refreshIcons();
      updateBadges();
    }
  };

  let appDownloadsUnsubscribe = null;
  const attachAppDownloadsListener=()=>{
    if(appDownloadsUnsubscribe) return;
    try{
      appDownloadsUnsubscribe=onValue(ref(db,'appDownloads'),snap=>{
        const raw=snap.exists()?snap.val():{};
        const linkItem = raw && raw.googleDrive;
        State.appDownloads = linkItem && !['inactive','hidden','draft','disabled'].includes(String(linkItem.status||'active').toLowerCase())
          ? [{ id:'googleDrive', ...linkItem }] : [];
        State.appDownloadsReady=true;
        if(State.ready && (location.hash==='#/' || location.hash==='' || location.hash.startsWith('#/home'))) scheduleMount(0);
      },err=>{
        console.error('[GEN Z] /appDownloads listener failed:',err);
        State.appDownloads=[];
        State.appDownloadsReady=true;
        if(State.ready && (location.hash==='#/' || location.hash==='' || location.hash.startsWith('#/home'))) scheduleMount(0);
      });
    }catch(err){
      console.error('[GEN Z] Could not create /appDownloads listener:',err);
      State.appDownloads=[];
      State.appDownloadsReady=true;
    }
  };

  const attachProductsListener=()=>{
    if(productsUnsubscribe) return;
    try{
      logBoot('Subscribing to /products after Firebase Auth state is known.');
      productsUnsubscribe=onValue(ref(db,'products'),snap=>{
        try{
          const raw=snap.exists()?snap.val():{};
          State.products=Object.keys(raw).map(k=>mapProduct(k,raw[k]))
            .filter(p=>!['inactive','hidden','draft'].includes(String(p.status||'active').toLowerCase()));
          State.productsReady=true;
          logBoot('Products snapshot received.',{count:State.products.length});
          if(!State.ready) maybeRenderInitialPage();
          else{
            const tag=(document.activeElement&&document.activeElement.tagName)||'';
            if(!['INPUT','TEXTAREA','SELECT'].includes(tag)&&!location.hash.startsWith('#/product/')) scheduleMount(0);
          }
        }catch(renderDataErr){
          console.error('[GEN Z] Could not normalize products snapshot:',renderDataErr);
          State.products=[];
          State.productsReady=true;
          maybeRenderInitialPage();
        }
      },err=>{
        console.error('[GEN Z] /products listener failed:',{
          code:err?.code||'',
          message:err?.message||String(err),
          error:err
        });
        State.products=[];
        State.productsReady=true;
        maybeRenderInitialPage();
        if(State.ready) scheduleMount(0);
      });
    }catch(err){
      console.error('[GEN Z] Could not create /products listener:',err);
      State.products=[];
      State.productsReady=true;
      maybeRenderInitialPage();
    }
  };

  const attachUserDataListeners=uid=>{
    clearUserDataListeners();
    const ownOrders=query(ref(db,'orders'),orderByChild('userId'),equalTo(uid));
    userDataUnsubs.push(onValue(ownOrders,snap=>{
      const all=snap.exists()?snap.val():{};
      State.orders=Object.keys(all).map(k=>({id:k,...all[k]}))
        .sort((x,y)=>(Number(y.date)||0)-(Number(x.date)||0));
      if(State.ready&&(location.hash.startsWith('#/orders')||location.hash.startsWith('#/order/'))) scheduleMount();
    },err=>console.error('[GEN Z] Orders listener failed:',err)));
    userDataUnsubs.push(onValue(ref(db,'notifications/'+uid),snap=>{
      const all=snap.exists()?snap.val():{};
      State.notifications=Object.keys(all).map(k=>({id:k,...all[k]}))
        .sort((x,y)=>(Number(y.date)||0)-(Number(x.date)||0));
      if(State.ready&&location.hash.startsWith('#/notifications')) scheduleMount();
    },err=>console.error('[GEN Z] Notifications listener failed:',err)));
  };

  const startStaticLoads=()=>{
    if(staticLoadsStarted) return;
    staticLoadsStarted=true;
    attachAppDownloadsListener();
    Promise.allSettled([
      loadCategories(),loadBanners(),loadDiscounts(),loadSettings(),loadBackground()
    ]).then(()=>{
      logBoot('Non-blocking store configuration reads settled.');
      if(State.ready&&!location.hash.startsWith('#/product/')) scheduleMount(0);
    });
  };

  State.user={uid:guestId,email:'',isGuest:true};
  logBoot('Boot started.',{
    readyState:document.readyState,
    viewport:{width:window.innerWidth,height:window.innerHeight},
    userAgent:navigator.userAgent
  });

  // The module script is at the end of BODY, so the application DOM already exists.
  // Do not wait for all optional database reads before subscribing or rendering.
  onAuthStateChanged(auth, firebaseUser=>{
    const version=++authChangeVersion;
    clearUserDataListeners();

    if(firebaseUser){
      State.user={
        uid:firebaseUser.uid,
        email:firebaseUser.email||'',
        displayName:firebaseUser.displayName||'',
        isGuest:false
      };
      logBoot('Firebase Auth state restored for signed-in user.');
    }else{
      State.user={uid:guestId,email:'',isGuest:true};
      State.userProfile=Storage.get('guestProfile',{});
      State.orders=[];
      State.notifications=[];
      State.addresses=[];
      State.myReviews=[];
      State.cart=Storage.get('cart',[]);
      State.wishlist=Storage.get('wishlist',[]);
      logBoot('Firebase Auth state resolved as guest.');
    }

    State.authReady=true;
    attachProductsListener();
    startStaticLoads();
    maybeRenderInitialPage();

    // User-specific data is intentionally loaded after the first page can render.
    // Slow orders/reviews reads must never hold the entire storefront on skeletons.
    if(firebaseUser){
      loadUserData(firebaseUser.uid).then(()=>{
        if(version!==authChangeVersion) return;
        attachUserDataListeners(firebaseUser.uid);
        logBoot('Signed-in user data loaded.');
        if(State.ready&&(
          location.hash.startsWith('#/account')||
          location.hash.startsWith('#/orders')||
          location.hash.startsWith('#/order/')||
          location.hash.startsWith('#/notifications')||
          location.hash.startsWith('#/myreviews')
        )) scheduleMount(0);
      }).catch(err=>{
        console.error('[GEN Z] Background user-data load failed:',err);
      });
    }
  },err=>{
    console.error('[GEN Z] Firebase Auth state error:',err);
    State.user={uid:guestId,email:'',isGuest:true};
    State.userProfile=Storage.get('guestProfile',{});
    State.cart=Storage.get('cart',[]);
    State.wishlist=Storage.get('wishlist',[]);
    State.authReady=true;
    attachProductsListener();
    startStaticLoads();
    maybeRenderInitialPage();
  });
}

document.getElementById('year').textContent = new Date().getFullYear();
document.getElementById('year2').textContent = new Date().getFullYear();

window.addEventListener('hashchange',()=>mount());
window.addEventListener('online',()=>{
  document.body.classList.remove('offline');
  logNetworkState('online');
});
window.addEventListener('offline',()=>{
  document.body.classList.add('offline');
  logNetworkState('offline');
});
window.addEventListener('pageshow',event=>{
  console.info('[GEN Z lifecycle] pageshow',{persisted:event.persisted,readyState:document.readyState});
  if(State.ready) scheduleMount(0);
});
document.addEventListener('visibilitychange',()=>{
  console.info('[GEN Z lifecycle] visibilitychange',{state:document.visibilityState});
  if(document.visibilityState==='visible'&&State.ready) scheduleMount(0);
});
window.addEventListener('resize',()=>{
  // Diagnostic only: resize is not required to trigger the initial render.
  console.info('[GEN Z lifecycle] resize',{width:window.innerWidth,height:window.innerHeight});
},{passive:true});

function logNetworkState(state){
  console.info('[GEN Z network] '+state,{online:navigator.onLine});
}

// Delegate close-nav (drawer is re-rendered per home render).
document.addEventListener('click',e=>{
  const a=e.target.closest('[data-close-nav]');
  if(a) App.toggleMobileNav();
});

boot().catch(err=>{
  console.error('[GEN Z] Boot failed:',err);
  // A failed optional startup task must not strand the UI behind skeletons.
  State.authReady=true;
  State.productsReady=true;
  State.ready=true;
  mount();
  refreshIcons();
  updateBadges();
});
if(window.lucide&&lucide.createIcons) lucide.createIcons();
</script>
</body>
</html>
