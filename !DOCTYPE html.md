<!DOCTYPE html>  
<html lang="ar" dir="rtl">  
<head>  
<meta charset="UTF-8">  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
<title>SOLIX</title>  
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;900&family=Orbitron:wght@700;900&display=swap" rel="stylesheet">  
<style>  
*{margin:0;padding:0;box-sizing:border-box;}  
:root{  
  --bg:#050A14;--bg2:#080F1E;--card:#0A1628;--border:#00BFFF22;  
  --blue:#00BFFF;--blue-dim:#0077AA;--glow:#00BFFF44;  
  --text:#D0E8F8;--muted:#5A7A99;--white:#FFFFFF;  
}  
html{scroll-behavior:smooth;}  
body{font-family:'Cairo',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;overflow-x:hidden;}  
body::before{content:'';position:fixed;inset:0;background-image:linear-gradient(rgba(0,191,255,.04) 1px,transparent 1px),linear-gradient(90deg,rgba(0,191,255,.04) 1px,transparent 1px);background-size:40px 40px;pointer-events:none;z-index:0;}  
body::after{content:'';position:fixed;inset:0;background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,.15) 2px,rgba(0,0,0,.15) 4px);pointer-events:none;z-index:0;opacity:.4;}  
  
/* LOGIN OVERLAY */  
#login-overlay{display:none;position:fixed;inset:0;background:rgba(2,8,20,.98);z-index:9000;align-items:center;justify-content:center;animation:fadeIn .2s ease;}  
#login-overlay.show{display:flex;}  
.login-box{background:linear-gradient(160deg,#0A1628,#050E1C);border:1px solid var(--blue);border-radius:18px;padding:36px 32px;width:320px;text-align:center;box-shadow:0 0 60px rgba(0,191,255,.18);}  
.login-box h2{font-family:'Orbitron',sans-serif;font-size:16px;color:var(--blue);letter-spacing:3px;margin-bottom:6px;}  
.login-box p{font-size:12px;color:var(--muted);margin-bottom:24px;}  
.login-input{width:100%;padding:12px 16px;background:#050E1C;border:1px solid var(--border);border-radius:8px;color:var(--white);font-family:'Cairo',sans-serif;font-size:14px;outline:none;transition:border .2s;text-align:center;letter-spacing:4px;margin-bottom:12px;}  
.login-input:focus{border-color:var(--blue);}  
.login-btn{width:100%;padding:12px;background:linear-gradient(135deg,var(--blue),var(--blue-dim));border:none;border-radius:8px;color:#000;font-family:'Cairo',sans-serif;font-size:14px;font-weight:700;cursor:pointer;transition:all .2s;margin-bottom:10px;}  
.login-btn:hover{box-shadow:0 0 20px rgba(0,191,255,.4);}  
.login-cancel{background:none;border:none;color:var(--muted);font-family:'Cairo',sans-serif;font-size:13px;cursor:pointer;}  
.login-cancel:hover{color:var(--text);}  
.login-error{color:#FF4444;font-size:12px;margin-top:8px;min-height:16px;}  
  
/* HEADER */  
header{position:relative;z-index:10;text-align:center;padding:50px 20px 30px;border-bottom:1px solid var(--border);}  
.logo-wrap{display:inline-flex;align-items:center;gap:16px;margin-bottom:12px;}  
header h1{font-family:'Orbitron',sans-serif;font-size:clamp(28px,5vw,52px);color:var(--white);letter-spacing:6px;text-shadow:0 0 30px var(--blue),0 0 60px rgba(0,191,255,.3);}  
.header-sub{font-size:14px;color:var(--muted);letter-spacing:1px;margin-top:6px;}  
.header-badges{display:flex;justify-content:center;gap:12px;flex-wrap:wrap;margin-top:16px;}  
.badge{font-size:11px;padding:5px 14px;border:1px solid var(--blue);border-radius:20px;color:var(--blue);background:rgba(0,191,255,.06);letter-spacing:1px;}  
  
/* SEARCH */  
.search-wrap{position:relative;z-index:10;max-width:500px;margin:24px auto 0;padding:0 20px;}  
.search-inner{position:relative;}  
.search-icon{position:absolute;right:14px;top:50%;transform:translateY(-50%);color:var(--muted);font-size:16px;pointer-events:none;}  
#search-input{width:100%;padding:12px 44px 12px 16px;background:var(--card);border:1px solid var(--border);border-radius:10px;color:var(--white);font-family:'Cairo',sans-serif;font-size:14px;outline:none;transition:border .2s;}  
#search-input:focus{border-color:var(--blue);box-shadow:0 0 16px rgba(0,191,255,.15);}  
#search-input::placeholder{color:var(--muted);}  
.search-clear{position:absolute;left:14px;top:50%;transform:translateY(-50%);background:none;border:none;color:var(--muted);cursor:pointer;font-size:16px;display:none;}  
  
/* NAV */  
.nav-strip{position:relative;z-index:10;display:flex;justify-content:center;gap:6px;padding:14px 20px;border-bottom:1px solid var(--border);flex-wrap:wrap;}  
.nav-btn{padding:7px 18px;font-size:13px;font-family:'Cairo',sans-serif;background:transparent;border:1px solid var(--border);border-radius:6px;color:var(--muted);cursor:pointer;transition:all .25s;}  
.nav-btn:hover,.nav-btn.active{border-color:var(--blue);color:var(--blue);background:rgba(0,191,255,.07);box-shadow:0 0 12px rgba(0,191,255,.2);}  
  
/* DEAL */  
#deal{position:relative;z-index:10;margin:30px auto;max-width:700px;padding:24px 30px;background:linear-gradient(135deg,#0A1E35 0%,#051020 100%);border:1px solid var(--blue);border-radius:16px;box-shadow:0 0 40px rgba(0,191,255,.12),inset 0 0 40px rgba(0,191,255,.03);text-align:center;animation:pulse 3s infinite;}  
#deal::before{content:'🔥 **أفضل** **عرض** **اليوم**';display:block;font-size:11px;letter-spacing:3px;color:var(--blue);margin-bottom:10px;font-weight:600;}  
#deal-product{font-size:22px;font-weight:700;color:var(--white);margin-bottom:10px;}  
.deal-prices{display:flex;justify-content:center;align-items:center;gap:20px;flex-wrap:wrap;margin-bottom:14px;}  
.deal-old{font-size:15px;color:var(--muted);text-decoration:line-through;}  
.deal-new{font-size:26px;font-weight:900;color:var(--blue);text-shadow:0 0 16px var(--blue);}  
#timer{font-family:'Orbitron',sans-serif;font-size:28px;font-weight:700;color:var(--white);letter-spacing:4px;text-shadow:0 0 20px var(--blue);}  
.timer-label{font-size:11px;color:var(--muted);letter-spacing:2px;margin-bottom:4px;}  
  
/* HOW TO ORDER */  
.how-section{position:relative;z-index:10;max-width:700px;margin:0 auto 30px;padding:0 20px;}  
.how-toggle{width:100%;padding:14px 20px;background:var(--card);border:1px solid var(--border);border-radius:10px;color:var(--text);font-family:'Cairo',sans-serif;font-size:14px;font-weight:600;cursor:pointer;display:flex;justify-content:space-between;align-items:center;transition:all .2s;}  
.how-toggle:hover{border-color:rgba(0,191,255,.4);}  
.how-toggle .arrow{color:var(--blue);transition:transform .3s;font-size:12px;}  
.how-toggle.open .arrow{transform:rotate(180deg);}  
.how-content{display:none;background:var(--card);border:1px solid var(--border);border-top:none;border-radius:0 0 10px 10px;padding:20px;}  
.how-content.open{display:block;}  
.how-steps{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:14px;margin-top:4px;}  
.how-step{text-align:center;padding:14px 10px;}  
.how-step .num{width:36px;height:36px;background:rgba(0,191,255,.12);border:1px solid rgba(0,191,255,.3);border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:'Orbitron',sans-serif;font-size:13px;color:var(--blue);margin:0 auto 10px;}  
.how-step p{font-size:12px;color:var(--muted);line-height:1.6;}  
  
/* SECTION */  
.section-title{position:relative;z-index:10;text-align:center;font-size:13px;letter-spacing:4px;color:var(--blue);margin:40px 0 24px;display:flex;align-items:center;justify-content:center;gap:16px;}  
.section-title::before,.section-title::after{content:'';flex:1;max-width:120px;height:1px;background:linear-gradient(90deg,transparent,var(--blue));}  
.section-title::after{background:linear-gradient(270deg,transparent,var(--blue));}  
  
/* SKELETON */  
.skeleton{background:linear-gradient(90deg,#0A1628 25%,#0D1E38 50%,#0A1628 75%);background-size:200% 100%;animation:shimmer 1.4s infinite;border-radius:14px;}  
@keyframes shimmer{0%{background-position:200% 0}100%{background-position:-200% 0}}  
.skel-card{height:220px;}  
  
/* PRODUCTS */  
.products{position:relative;z-index:10;display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:18px;max-width:1100px;margin:0 auto 40px;padding:0 20px;}  
.product-card{background:var(--card);border:1px solid var(--border);border-radius:14px;padding:24px 18px 18px;text-align:center;transition:transform .3s,border-color .3s,box-shadow .3s;cursor:pointer;position:relative;overflow:hidden;}  
.product-card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,transparent,var(--blue),transparent);opacity:0;transition:opacity .3s;}  
.product-card:hover{transform:translateY(-6px);border-color:rgba(0,191,255,.5);box-shadow:0 12px 40px rgba(0,191,255,.15),0 0 0 1px rgba(0,191,255,.1);}  
.product-card:hover::before{opacity:1;}  
.product-img-wrap{width:80px;height:80px;border-radius:16px;border:1px solid rgba(0,191,255,.2);margin:0 auto 14px;overflow:hidden;display:flex;align-items:center;justify-content:center;background:linear-gradient(135deg,rgba(0,191,255,.12),rgba(0,191,255,.04));transition:transform .3s;}  
.product-card:hover .product-img-wrap{transform:scale(1.08);}  
.product-img-wrap img{width:100%;height:100%;object-fit:cover;}  
.product-img-wrap .emoji-icon{font-size:38px;}  
.product-card h3{font-size:15px;font-weight:700;color:var(--white);margin-bottom:6px;}  
.product-card .sub{font-size:11px;color:var(--muted);margin-bottom:14px;}  
.show-btn{width:100%;padding:10px;background:linear-gradient(135deg,rgba(0,191,255,.15),rgba(0,191,255,.05));border:1px solid rgba(0,191,255,.3);border-radius:8px;color:var(--blue);font-family:'Cairo',sans-serif;font-size:13px;font-weight:600;cursor:pointer;transition:all .25s;}  
.show-btn:hover{background:linear-gradient(135deg,rgba(0,191,255,.3),rgba(0,191,255,.1));box-shadow:0 0 16px rgba(0,191,255,.3);}  
.options,.prices{display:none;margin-top:12px;}  
.options.open,.prices.open{display:block;}  
.opt-grid{display:grid;grid-template-columns:1fr 1fr;gap:6px;}  
.opt-btn{padding:7px 6px;font-size:12px;font-family:'Cairo',sans-serif;background:rgba(0,191,255,.06);border:1px solid rgba(0,191,255,.2);border-radius:6px;color:var(--text);cursor:pointer;transition:all .2s;}  
.opt-btn:hover{background:rgba(0,191,255,.15);border-color:var(--blue);color:var(--blue);}  
.price-list{display:flex;flex-direction:column;gap:6px;}  
.price-btn{width:100%;padding:8px 10px;font-family:'Cairo',sans-serif;font-size:13px;font-weight:600;background:linear-gradient(135deg,rgba(0,191,255,.18),rgba(0,191,255,.06));border:1px solid rgba(0,191,255,.35);border-radius:7px;color:var(--white);cursor:pointer;display:flex;justify-content:space-between;align-items:center;transition:all .2s;}  
.price-btn:hover{background:linear-gradient(135deg,rgba(0,191,255,.35),rgba(0,191,255,.15));box-shadow:0 0 14px rgba(0,191,255,.25);transform:translateX(-2px);}  
.price-btn .lyd{font-size:11px;color:var(--blue);}  
.price-btn .add-icon{font-size:16px;color:var(--blue);}  
  
/* EMPTY STATE */  
.empty-state{position:relative;z-index:10;text-align:center;padding:60px 20px;max-width:400px;margin:0 auto;}  
.empty-icon{font-size:56px;margin-bottom:16px;opacity:.5;}  
.empty-state h3{font-size:16px;color:var(--text);margin-bottom:8px;}  
.empty-state p{font-size:13px;color:var(--muted);}  
  
/* CART */  
#cart-btn{position:fixed;bottom:24px;left:24px;width:58px;height:58px;background:linear-gradient(135deg,var(--blue),var(--blue-dim));border:none;border-radius:50%;font-size:22px;cursor:pointer;box-shadow:0 0 24px rgba(0,191,255,.5);z-index:1000;transition:transform .2s,box-shadow .2s;display:flex;align-items:center;justify-content:center;}  
#cart-btn:hover{transform:scale(1.1);box-shadow:0 0 36px rgba(0,191,255,.7);}  
#cart-count{position:absolute;top:-4px;right:-4px;background:#FF2020;color:#fff;width:20px;height:20px;border-radius:50%;font-size:11px;font-weight:700;display:none;align-items:center;justify-content:center;}  
#cart-panel{position:fixed;bottom:94px;left:24px;width:300px;background:linear-gradient(160deg,#0A1628,#050E1C);border:1px solid var(--blue);border-radius:16px;padding:20px;display:none;z-index:1000;box-shadow:0 0 40px rgba(0,191,255,.2);}  
#cart-panel h3{font-size:14px;letter-spacing:2px;color:var(--blue);margin-bottom:14px;border-bottom:1px solid var(--border);padding-bottom:10px;}  
#cart-items{max-height:180px;overflow-y:auto;margin-bottom:12px;}  
#cart-items::-webkit-scrollbar{width:4px;}  
#cart-items::-webkit-scrollbar-thumb{background:var(--blue-dim);border-radius:4px;}  
.cart-item-row{display:flex;justify-content:space-between;align-items:center;padding:7px 0;border-bottom:1px solid var(--border);font-size:13px;}  
.cart-item-row .name{color:var(--text);}  
.cart-item-row .price{color:var(--blue);font-weight:700;}  
.cart-item-row .rm{background:none;border:none;color:#FF4444;cursor:pointer;font-size:14px;padding:2px 6px;}  
.cart-total{display:flex;justify-content:space-between;font-size:15px;font-weight:700;padding:10px 0;border-top:1px solid rgba(0,191,255,.2);margin-bottom:8px;}  
.cart-total .amount{color:var(--blue);}  
.clear-cart-btn{width:100%;padding:8px;background:rgba(255,68,68,.08);border:1px solid rgba(255,68,68,.25);border-radius:7px;color:#FF6666;font-family:'Cairo',sans-serif;font-size:12px;cursor:pointer;margin-bottom:8px;transition:all .2s;}  
.clear-cart-btn:hover{background:rgba(255,68,68,.15);}  
.whatsapp-btn{width:100%;padding:12px;background:linear-gradient(135deg,#25D366,#128C7E);border:none;border-radius:8px;color:#fff;font-family:'Cairo',sans-serif;font-size:14px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px;transition:all .2s;}  
.whatsapp-btn:hover{box-shadow:0 0 20px rgba(37,211,102,.4);}  
  
/* CONFIRM MODAL */  
#confirm-modal{display:none;position:fixed;inset:0;background:rgba(2,8,20,.9);z-index:8000;align-items:center;justify-content:center;}  
#confirm-modal.show{display:flex;}  
.confirm-box{background:linear-gradient(160deg,#0A1628,#050E1C);border:1px solid var(--blue);border-radius:16px;padding:28px 24px;width:340px;max-width:90vw;box-shadow:0 0 50px rgba(0,191,255,.2);}  
.confirm-box h3{font-size:15px;color:var(--white);margin-bottom:6px;font-weight:700;}  
.order-id-display{font-family:'Orbitron',sans-serif;font-size:18px;color:var(--blue);text-align:center;padding:12px;background:rgba(0,191,255,.06);border:1px solid rgba(0,191,255,.2);border-radius:8px;margin:14px 0;letter-spacing:2px;}  
.confirm-items{max-height:140px;overflow-y:auto;margin-bottom:12px;}  
.confirm-item{display:flex;justify-content:space-between;font-size:12px;padding:5px 0;border-bottom:1px solid var(--border);color:var(--text);}  
.confirm-item .c-price{color:var(--blue);}  
.confirm-total{display:flex;justify-content:space-between;font-size:15px;font-weight:700;padding:10px 0;border-top:1px solid rgba(0,191,255,.2);margin-bottom:14px;}  
.confirm-total span:last-child{color:var(--blue);}  
.confirm-btns{display:flex;gap:8px;}  
.confirm-btns button{flex:1;padding:11px;border-radius:8px;font-family:'Cairo',sans-serif;font-size:13px;font-weight:700;cursor:pointer;border:none;transition:all .2s;}  
.btn-cancel-order{background:rgba(255,68,68,.1);border:1px solid rgba(255,68,68,.3)!important;color:#FF6666;}  
.btn-confirm-order{background:linear-gradient(135deg,#25D366,#128C7E);color:#fff;}  
.btn-confirm-order:hover{box-shadow:0 0 16px rgba(37,211,102,.4);}  
  
/* NOTIFICATION BELL */  
#notif-bell{position:fixed;top:20px;left:20px;width:44px;height:44px;background:var(--card);border:1px solid var(--border);border-radius:50%;display:flex;align-items:center;justify-content:center;cursor:pointer;z-index:999;font-size:18px;transition:all .2s;}  
#notif-bell:hover{border-color:var(--blue);}  
#notif-dot{position:absolute;top:4px;right:4px;width:10px;height:10px;background:#FF2020;border-radius:50%;display:none;animation:blink 1s infinite;}  
@keyframes blink{0%,100%{opacity:1}50%{opacity:.3}}  
#notif-panel{position:fixed;top:74px;left:20px;width:280px;background:linear-gradient(160deg,#0A1628,#050E1C);border:1px solid var(--blue);border-radius:12px;padding:16px;display:none;z-index:1000;box-shadow:0 0 30px rgba(0,191,255,.15);max-height:300px;overflow-y:auto;}  
#notif-panel h4{font-size:12px;letter-spacing:2px;color:var(--blue);margin-bottom:12px;}  
.notif-item{font-size:12px;padding:8px 0;border-bottom:1px solid var(--border);color:var(--text);}  
.notif-item .n-time{font-size:10px;color:var(--muted);margin-top:3px;}  
.notif-empty{font-size:12px;color:var(--muted);text-align:center;padding:10px;}  
  
/* FOOTER */  
footer{position:relative;z-index:10;text-align:center;padding:30px 20px;border-top:1px solid var(--border);color:var(--muted);font-size:12px;letter-spacing:1px;}  
footer span{color:var(--blue);}  
  
/* TOAST */  
#toast{position:fixed;top:20px;right:20px;background:linear-gradient(135deg,#0A1E35,#050E1C);border:1px solid var(--blue);border-radius:10px;padding:12px 20px;color:var(--white);font-size:13px;z-index:9999;display:none;box-shadow:0 0 24px rgba(0,191,255,.3);}  
  
/* ANIMATIONS */  
@keyframes pulse{0%,100%{box-shadow:0 0 10px rgba(0,191,255,.3)}50%{box-shadow:0 0 24px rgba(0,191,255,.6)}}  
@keyframes fadeIn{from{opacity:0;transform:translateY(-10px)}to{opacity:1;transform:translateY(0)}}  
  
/* ADMIN PANEL */  
#admin-overlay{display:none;position:fixed;inset:0;background:rgba(2,8,20,.97);z-index:5000;overflow-y:auto;animation:fadeIn .2s ease;}  
.admin-wrap{max-width:860px;margin:0 auto;padding:30px 20px 60px;}  
.admin-header{display:flex;justify-content:space-between;align-items:center;padding:20px 0 20px;border-bottom:1px solid var(--border);margin-bottom:30px;}  
.admin-header h2{font-family:'Orbitron',sans-serif;font-size:18px;color:var(--blue);letter-spacing:3px;}  
.admin-close{background:none;border:1px solid #FF4444;color:#FF4444;padding:7px 16px;border-radius:6px;cursor:pointer;font-family:'Cairo',sans-serif;font-size:13px;}  
.admin-close:hover{background:#FF444422;}  
.admin-tabs{display:flex;gap:6px;margin-bottom:24px;flex-wrap:wrap;}  
.a-tab{padding:9px 20px;border:1px solid var(--border);border-radius:8px;background:transparent;color:var(--muted);font-family:'Cairo',sans-serif;font-size:13px;cursor:pointer;transition:all .2s;}  
.a-tab.active,.a-tab:hover{border-color:var(--blue);color:var(--blue);background:rgba(0,191,255,.08);}  
.admin-section{display:none;}  
.admin-section.active{display:block;}  
.a-card{background:#0A1628;border:1px solid var(--border);border-radius:12px;padding:20px;margin-bottom:16px;}  
.a-card h4{font-size:13px;color:var(--blue);letter-spacing:2px;margin-bottom:14px;padding-bottom:8px;border-bottom:1px solid var(--border);}  
.a-row{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:10px;}  
.a-row.one{grid-template-columns:1fr;}  
.a-input{width:100%;padding:10px 14px;background:#050E1C;border:1px solid var(--border);border-radius:7px;color:var(--white);font-family:'Cairo',sans-serif;font-size:13px;outline:none;transition:border .2s;}  
.a-input:focus{border-color:var(--blue);}  
.a-btn{padding:10px 22px;border:none;border-radius:7px;font-family:'Cairo',sans-serif;font-size:13px;font-weight:700;cursor:pointer;transition:all .2s;}  
.a-btn.primary{background:linear-gradient(135deg,var(--blue),var(--blue-dim));color:#000;}  
.a-btn.primary:hover{box-shadow:0 0 16px rgba(0,191,255,.4);}  
.a-btn.danger{background:linear-gradient(135deg,#FF4444,#AA2222);color:#fff;}  
.a-btn.danger:hover{box-shadow:0 0 16px rgba(255,68,68,.4);}  
.a-btn.success{background:linear-gradient(135deg,#25D366,#128C7E);color:#fff;}  
.orders-table{width:100%;border-collapse:collapse;font-size:13px;}  
.orders-table th{padding:10px;text-align:right;color:var(--blue);border-bottom:1px solid var(--border);font-weight:600;font-size:11px;letter-spacing:1px;}  
.orders-table td{padding:10px;border-bottom:1px solid var(--border);color:var(--text);vertical-align:top;}  
.orders-table tr:hover td{background:rgba(0,191,255,.03);}  
.order-badge{display:inline-block;padding:3px 10px;border-radius:20px;font-size:11px;font-weight:700;}  
.order-badge.new{background:rgba(0,191,255,.15);color:var(--blue);border:1px solid rgba(0,191,255,.3);}  
.order-badge.done{background:rgba(37,211,102,.15);color:#25D366;border:1px solid rgba(37,211,102,.3);}  
.prod-row{display:flex;justify-content:space-between;align-items:center;padding:12px 0;border-bottom:1px solid var(--border);}  
.prod-row:last-child{border:none;}  
.prod-name{font-size:13px;color:var(--white);display:flex;align-items:center;gap:8px;}  
.prod-thumb{width:30px;height:30px;border-radius:6px;background:rgba(0,191,255,.08);border:1px solid rgba(0,191,255,.15);display:flex;align-items:center;justify-content:center;font-size:16px;overflow:hidden;}  
.prod-thumb img{width:100%;height:100%;object-fit:cover;}  
.prod-actions{display:flex;gap:6px;}  
.icon-btn{background:none;border:1px solid var(--border);border-radius:6px;color:var(--muted);padding:5px 10px;cursor:pointer;font-size:12px;transition:all .2s;}  
.icon-btn:hover{border-color:var(--blue);color:var(--blue);}  
.icon-btn.del:hover{border-color:#FF4444;color:#FF4444;}  
.stat-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:12px;margin-bottom:16px;}  
.stat-box{background:#050E1C;border:1px solid var(--border);border-radius:10px;padding:14px;text-align:center;}  
.stat-box .val{font-family:'Orbitron',sans-serif;font-size:22px;color:var(--blue);font-weight:700;}  
.stat-box .lbl{font-size:11px;color:var(--muted);margin-top:4px;letter-spacing:1px;}  
  
/* EDIT PRODUCT MODAL */  
#edit-modal{display:none;position:fixed;inset:0;background:rgba(2,8,20,.95);z-index:6000;align-items:center;justify-content:center;}  
#edit-modal.show{display:flex;}  
.edit-box{background:linear-gradient(160deg,#0A1628,#050E1C);border:1px solid var(--blue);border-radius:16px;padding:28px 24px;width:420px;max-width:92vw;max-height:90vh;overflow-y:auto;box-shadow:0 0 50px rgba(0,191,255,.2);}  
.edit-box h3{font-size:14px;letter-spacing:2px;color:var(--blue);margin-bottom:20px;}  
.edit-btns{display:flex;gap:8px;margin-top:16px;}  
  
/* IMAGE UPLOAD */  
.img-upload-area{border:2px dashed rgba(0,191,255,.3);border-radius:10px;padding:20px;text-align:center;cursor:pointer;transition:all .2s;margin-bottom:8px;}  
.img-upload-area:hover{border-color:var(--blue);background:rgba(0,191,255,.04);}  
.img-upload-area p{font-size:12px;color:var(--muted);margin-top:8px;}  
.img-preview{width:60px;height:60px;border-radius:8px;object-fit:cover;border:1px solid rgba(0,191,255,.3);margin:8px auto 0;display:block;}  
  
/* PRICE MANAGEMENT */  
.price-manage-list{display:flex;flex-direction:column;gap:6px;margin:10px 0;}  
.price-manage-item{display:flex;gap:6px;align-items:center;}  
.price-manage-item .a-input{flex:1;}  
.price-remove{background:none;border:1px solid rgba(255,68,68,.3);color:#FF6666;border-radius:6px;padding:8px 10px;cursor:pointer;font-size:12px;white-space:nowrap;}  
  
@media(max-width:600px){  
  .products{grid-template-columns:repeat(2,1fr);gap:12px;padding:0 12px;}  
  #cart-panel{width:calc(100vw - 48px);}  
  header h1{letter-spacing:2px;}  
  .a-row{grid-template-columns:1fr;}  
  .confirm-box{width:92vw;}  
}  
</style>  
</head>  
<body>  
  
<header>  
  <div class="logo-wrap">  
    <h1>SOLIX</h1>  
  </div>  
  <p class="header-sub">**الاحترافية** **ليست** **خيارًا** — **بل** **معيارنا**</p>  
  <div class="header-badges">  
    <span class="badge">⚡ **تسليم** **فوري**</span>  
    <span class="badge">🔐 **دفع** **آمن**</span>  
    <span class="badge">✅ **موثوق** 100%</span>  
    <span class="badge">🌍 **جميع** **المنصات**</span>  
  </div>  
</header>  
  
<div class="search-wrap">  
  <div class="search-inner">  
    <span class="search-icon">🔍</span>  
    <input type="text" id="search-input" placeholder="**ابحث** **عن** **منتج**..." oninput="handleSearch(this.value)">  
    <button class="search-clear" id="search-clear" onclick="clearSearch()">✕</button>  
  </div>  
</div>  
  
<nav class="nav-strip" id="main-nav">  
  <button class="nav-btn active">**الكل**</button>  
</nav>  
  
<div id="deal">  
  <p id="deal-product">PUBG 600 UC</p>  
  <div class="deal-prices">  
    <span class="deal-old">**السعر** **القديم**: <span id="old-price">6600 **د**.**ل**</span></span>  
    <span class="deal-new" id="new-price">1210 **د**.**ل**</span>  
  </div>  
  <div class="timer-label">**ينتهي** **العرض** **خلال**</div>  
  <div id="timer">24:00:00</div>  
</div>  
  
<div class="how-section">  
  <button class="how-toggle" onclick="toggleHow(this)">  
    <span>📋 **كيف** **تطلب؟**</span>  
    <span class="arrow">▼</span>  
  </button>  
  <div class="how-content">  
    <div class="how-steps">  
      <div class="how-step"><div class="num">1</div><p>**اختر** **المنتج** **والفئة** **المطلوبة**</p></div>  
      <div class="how-step"><div class="num">2</div><p>**أضف** **للسلة** **وراجع** **طلبك**</p></div>  
      <div class="how-step"><div class="num">3</div><p>**اضغط** "**اطلب** **عبر** **واتساب**"</p></div>  
      <div class="how-step"><div class="num">4</div><p>**أكمل** **الدفع** **واستلم** **فوراً**</p></div>  
    </div>  
  </div>  
</div>  
  
<div class="section-title">**المنتجات** **المتاحة**</div>  
<div class="products" id="products-grid"></div>  
<div id="empty-state" style="display:none;">  
  <div class="empty-state">  
    <div class="empty-icon">🔍</div>  
    <h3>**لا** **توجد** **نتائج**</h3>  
    <p>**لم** **نجد** **منتجات** **تطابق** **بحثك،** **جرب** **كلمة** **أخرى**</p>  
  </div>  
</div>  
  
<footer>  
  **جميع** **الحقوق** **محفوظة** ©️ <span>SOLIX</span> 2025 — **تنفيذ** **فوري** · **ثقة** **دائمة**  
</footer>  
  
<!-- NOTIFICATION BELL -->  
<button id="notif-bell" onclick="toggleNotif()">🔔<span id="notif-dot"></span></button>  
<div id="notif-panel">  
  <h4>🔔 **الإشعارات**</h4>  
  <div id="notif-list"><p class="notif-empty">**لا** **توجد** **إشعارات**</p></div>  
</div>  
  
<!-- CART -->  
<button id="cart-btn" onclick="toggleCart()">🛒<span id="cart-count">0</span></button>  
<div id="cart-panel">  
  <h3>🛒 **سلة** **المشتريات**</h3>  
  <div id="cart-items"><p style="color:var(--muted);font-size:13px;text-align:center;padding:10px 0;">**السلة** **فارغة**</p></div>  
  <div class="cart-total"><span>**الإجمالي**</span><span class="amount"><span id="total">0</span> **د**.**ل**</span></div>  
  <button class="clear-cart-btn" onclick="clearCart()">🗑 **إفراغ** **السلة**</button>  
  <button class="whatsapp-btn" onclick="initiateCheckout()">  
    <svg width="18" height="18" viewBox="0 0 24 24" fill="white"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347z"/><path d="M12 0C5.373 0 0 5.373 0 12c0 2.123.554 4.112 1.524 5.84L0 24l6.336-1.502A11.954 11.954 0 0012 24c6.627 0 12-5.373 12-12S18.627 0 12 0zm0 21.818a9.818 9.818 0 01-5.003-1.368l-.36-.214-3.727.883.916-3.617-.235-.372A9.818 9.818 0 1112 21.818z"/></svg>  
    **اطلب** **عبر** **واتساب**  
  </button>  
</div>  
  
<!-- CONFIRM MODAL -->  
<div id="confirm-modal">  
  <div class="confirm-box">  
    <h3>**تأكيد** **الطلب**</h3>  
    <div class="order-id-display" id="modal-order-id">SX-000000</div>  
    <div class="confirm-items" id="modal-items"></div>  
    <div class="confirm-total">  
      <span>**الإجمالي**</span>  
      <span id="modal-total">0 **د**.**ل**</span>  
    </div>  
    <div class="confirm-btns">  
      <button class="btn-cancel-order" onclick="closeConfirm()">**إلغاء**</button>  
      <button class="btn-confirm-order" onclick="confirmOrder()">**تأكيد** **وإرسال** ✓</button>  
    </div>  
  </div>  
</div>  
  
<!-- LOGIN OVERLAY -->  
<div id="login-overlay">  
  <div class="login-box">  
    <h2>ADMIN ACCESS</h2>  
    <p>**أدخل** **كلمة** **المرور** **للدخول**</p>  
    <input type="password" class="login-input" id="login-input" placeholder="••••••••" onkeydown="if(event.key==='Enter')doLogin()">  
    <button class="login-btn" onclick="doLogin()">**دخول**</button>  
    <button class="login-cancel" onclick="closeLogin()">**إلغاء**</button>  
    <p class="login-error" id="login-error"></p>  
  </div>  
</div>  
  
<div id="toast"></div>  
  
<!-- EDIT PRODUCT MODAL -->  
<div id="edit-modal">  
  <div class="edit-box">  
    <h3>✏️ **تعديل** **المنتج**</h3>  
    <div class="a-row">  
      <div>  
        <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**اسم** **المنتج**</label>  
        <input class="a-input" id="e-name" placeholder="**اسم** **المنتج**">  
      </div>  
      <div>  
        <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**أيقونة** (**إيموجي**)</label>  
        <input class="a-input" id="e-icon" placeholder="🎮">  
      </div>  
    </div>  
    <div class="a-row one" style="margin-bottom:10px;">  
      <div>  
        <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**وصف** **قصير**</label>  
        <input class="a-input" id="e-sub" placeholder="**وصف** **المنتج**">  
      </div>  
    </div>  
    <div class="a-row one" style="margin-bottom:10px;">  
      <div>  
        <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**رابط** **الصورة** (**اختياري**)</label>  
        <input class="a-input" id="e-img" placeholder="https://... **أو** **اتركه** **فارغاً** **للإيموجي**">  
      </div>  
    </div>  
    <div id="e-prices-section" style="display:none;">  
      <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:8px;">**الأسعار** **المخصصة** (**الاسم** — **السعر**)</label>  
      <div class="price-manage-list" id="e-price-list"></div>  
      <button class="a-btn primary" style="padding:7px 14px;font-size:12px;margin-top:6px;" onclick="addEditPrice()">+ **إضافة** **سعر**</button>  
    </div>  
    <input type="hidden" id="e-id">  
    <div class="edit-btns">  
      <button class="a-btn primary" onclick="saveEdit()">💾 **حفظ**</button>  
      <button class="a-btn danger" onclick="closeEdit()">**إلغاء**</button>  
    </div>  
  </div>  
</div>  
  
<!-- ADMIN PANEL -->  
<div id="admin-overlay">  
  <div class="admin-wrap">  
    <div class="admin-header">  
      <h2>⚙ **لوحة** **التحكم**</h2>  
      <button class="admin-close" onclick="closeAdmin()">✕ **إغلاق**</button>  
    </div>  
    <div class="admin-tabs">  
      <button class="a-tab active" onclick="showTab('tab-deal',this)">🔥 **عرض** **اليوم**</button>  
      <button class="a-tab" onclick="showTab('tab-products',this)">📦 **المنتجات**</button>  
      <button class="a-tab" onclick="showTab('tab-settings',this)">⚙ **الإعدادات**</button>  
      <button class="a-tab" onclick="showTab('tab-orders',this)">📋 **الطلبات**</button>  
    </div>  
  
    <!-- TAB: DEAL -->  
    <div class="admin-section active" id="tab-deal">  
      <div class="a-card">  
        <h4>**تعديل** **عرض** **اليوم**</h4>  
        <div class="a-row">  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**اسم** **المنتج**</label>  
            <input class="a-input" id="d-name" placeholder="**مثال**: PUBG 600 UC">  
          </div>  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**السعر** **الجديد** (**د**.**ل**)</label>  
            <input class="a-input" id="d-new" type="number" placeholder="1210">  
          </div>  
        </div>  
        <div class="a-row">  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**السعر** **القديم** (**د**.**ل**)</label>  
            <input class="a-input" id="d-old" type="number" placeholder="6600">  
          </div>  
        </div>  
        <button class="a-btn primary" onclick="saveDeal()">💾 **حفظ** **العرض**</button>  
      </div>  
    </div>  
  
    <!-- TAB: PRODUCTS -->  
    <div class="admin-section" id="tab-products">  
      <div class="a-card">  
        <h4>**إضافة** **منتج** **جديد**</h4>  
        <div class="a-row">  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**اسم** **المنتج**</label>  
            <input class="a-input" id="p-name" placeholder="**مثال**: Steam">  
          </div>  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**أيقونة** (**إيموجي**)</label>  
            <input class="a-input" id="p-icon" placeholder="🎮">  
          </div>  
        </div>  
        <div class="a-row one">  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**وصف** **قصير**</label>  
            <input class="a-input" id="p-sub" placeholder="**بطاقات** **هدايا** Steam">  
          </div>  
        </div>  
        <div class="a-row one" style="margin-bottom:10px;">  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**رابط** **صورة** **المنتج** (**اختياري**)</label>  
            <input class="a-input" id="p-img" placeholder="https://... **أو** **اتركه** **فارغاً** **للإيموجي**">  
          </div>  
        </div>  
        <div class="a-row one" style="margin-bottom:10px;">  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**النوع**</label>  
            <select class="a-input" id="p-type">  
              <option value="countries">**بطاقات** (**يختار** **الدولة** **ثم** **الفئة**)</option>  
              <option value="direct">**مباشر** **بأسعار** **محددة**</option>  
            </select>  
          </div>  
        </div>  
        <button class="a-btn primary" onclick="addProduct()">➕ **إضافة** **المنتج**</button>  
      </div>  
      <div class="a-card">  
        <h4>**المنتجات** **الحالية**</h4>  
        <div id="admin-prod-list"></div>  
      </div>  
    </div>  
  
    <!-- TAB: SETTINGS -->  
    <div class="admin-section" id="tab-settings">  
      <div class="a-card">  
        <h4>**سعر** **الصرف**</h4>  
        <div class="a-row">  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**سعر** **الدولار** **مقابل** **الدينار** **الليبي**</label>  
            <input class="a-input" id="s-rate" type="number" placeholder="11">  
          </div>  
        </div>  
        <button class="a-btn primary" onclick="saveRate()">💾 **حفظ**</button>  
      </div>  
      <div class="a-card">  
        <h4>**رقم** **الواتساب**</h4>  
        <div class="a-row one">  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**الرقم** **مع** **رمز** **الدولة** (**بدون** +)</label>  
            <input class="a-input" id="s-wa" placeholder="218948002556">  
          </div>  
        </div>  
        <button class="a-btn primary" onclick="saveWA()">💾 **حفظ**</button>  
      </div>  
      <div class="a-card">  
        <h4>🔐 **تغيير** **كلمة** **مرور** **الإدمن**</h4>  
        <div class="a-row one">  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**كلمة** **المرور** **الحالية**</label>  
            <input class="a-input" type="password" id="s-old-pass" placeholder="••••••••">  
          </div>  
        </div>  
        <div class="a-row">  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**كلمة** **المرور** **الجديدة**</label>  
            <input class="a-input" type="password" id="s-new-pass" placeholder="••••••••">  
          </div>  
          <div>  
            <label style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px;">**تأكيد** **كلمة** **المرور**</label>  
            <input class="a-input" type="password" id="s-confirm-pass" placeholder="••••••••">  
          </div>  
        </div>  
        <button class="a-btn primary" onclick="changePassword()">🔐 **تغيير** **كلمة** **المرور**</button>  
      </div>  
    </div>  
  
    <!-- TAB: ORDERS -->  
    <div class="admin-section" id="tab-orders">  
      <div class="stat-grid" id="order-stats"></div>  
      <div class="a-card">  
        <h4>**سجل** **الطلبات** **الواردة**</h4>  
        <div style="overflow-x:auto;">  
          <table class="orders-table">  
            <thead>  
              <tr>  
                <th>#</th><th>**رقم** **الطلب**</th><th>**المنتجات**</th><th>**الإجمالي**</th><th>**الوقت**</th><th>**الحالة**</th><th></th>  
              </tr>  
            </thead>  
            <tbody id="orders-body"></tbody>  
          </table>  
        </div>  
        <div style="margin-top:12px;">  
          <button class="a-btn danger" onclick="clearOrders()">🗑 **مسح** **الكل**</button>  
        </div>  
      </div>  
    </div>  
  </div>  
</div>  
  
<script>  
/* ===== STATE ===== */  
const DEFAULT_PASS = btoa('Asdweb2009');  
  
let state = JSON.parse(localStorage.getItem('solixstor_v2') || 'null') || {  
  USD: 11,  
  waNumber: '218948002556',  
  adminPass: DEFAULT_PASS,  
  deal: { name: 'PUBG 600 UC', newPrice: 1210, oldPrice: 6600 },  
  products: [  
    { id:1, name:'iTunes',      icon:'🎵', img:'', sub:'**بطاقات** **هدايا** **أمريكية** **وأكثر**', type:'countries', prices:[] },  
    { id:2, name:'PlayStation', icon:'🎮', img:'', sub:'PSN **بطاقات** **شحن** **رسمية**',       type:'countries', prices:[] },  
    { id:3, name:'Xbox',        icon:'🕹', img:'', sub:'**بطاقات** Microsoft Store',     type:'countries', prices:[] },  
    { id:4, name:'Snapchat+',   icon:'👻', img:'', sub:'**اشتراكات** **بريميوم**',           type:'countries', prices:[] },  
    { id:5, name:'PUBG',        icon:'🎯', img:'', sub:'**شحن** UC **مباشر** **وسريع**',         type:'direct',    prices:[] },  
    { id:6, name:'Google Play', icon:'▶️', img:'', sub:'**بطاقات** **شحن** **جوجل**',           type:'countries', prices:[] }  
  ],  
  orders: [],  
  notifications: []  
};  
  
// Migration: ensure all products have img and prices fields  
state.products = state.products.map(p => ({img:'', prices:[], ...p}));  
  
let cart = JSON.parse(sessionStorage.getItem('solix_cart') || '[]');  
let nextId = state.products.reduce((m,p)=>Math.max(m,p.id),0)+1;  
let pendingOrder = null;  
  
function save(){  
  localStorage.setItem('solixstor_v2', JSON.stringify(state));  
}  
function saveCart(){  
  sessionStorage.setItem('solix_cart', JSON.stringify(cart));  
}  
  
/* ===== TIMER ===== */  
function getLibyaSecsLeft(){  
  const now = new Date();  
  const libyaMs = now.getTime() + (now.getTimezoneOffset()*60000) + (2*3600000);  
  const d = new Date(libyaMs);  
  return 86400 - (d.getHours()*3600 + d.getMinutes()*60 + d.getSeconds());  
}  
function tick(){  
  const secs = getLibyaSecsLeft();  
  const h = String(Math.floor(secs/3600)).padStart(2,'0');  
  const m = String(Math.floor((secs%3600)/60)).padStart(2,'0');  
  const s = String(secs%60).padStart(2,'0');  
  document.getElementById('timer').textContent = `${h}:${m}:${s}`;  
}  
setInterval(tick,1000); tick();  
  
/* ===== RENDER ===== */  
function renderDeal(){  
  document.getElementById('deal-product').textContent = state.deal.name;  
  document.getElementById('new-price').textContent = state.deal.newPrice + ' **د**.**ل**';  
  document.getElementById('old-price').textContent = state.deal.oldPrice + ' **د**.**ل**';  
}  
  
function renderNav(){  
  const nav = document.getElementById('main-nav');  
  nav.innerHTML = '<button class="nav-btn active" onclick="filterProducts(this,\'**الكل**\')">**الكل**</button>';  
  state.products.forEach(p=>{  
    const b = document.createElement('button');  
    b.className='nav-btn';  
    b.textContent = p.name;  
    b.onclick = function(){ filterProducts(this, p.name); };  
    nav.appendChild(b);  
  });  
}  
  
function filterProducts(btn, name){  
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));  
  btn.classList.add('active');  
  document.querySelectorAll('.product-card').forEach(c=>{  
    c.style.display=(name==='**الكل**'||c.dataset.name===name)?'':'none';  
  });  
}  
  
const COUNTRIES = ['🇺🇸 **أمريكا**','🇹🇷 **تركيا**','🇸🇦 **السعودية**','🇦🇪 **الإمارات**','🇬🇧 **بريطانيا**'];  
const STD_AMOUNTS = [5,10,25,50,100];  
const PUBG_UC = [60,300,600,1500,3000];  
  
function makeImgHTML(p){  
  if(p.img) return `<img src="${p.img}" alt="${p.name}" onerror="this.style.display='none';this.nextElementSibling.style.display='flex'"><span class="emoji-icon" style="display:none">${p.icon}</span>`;  
  return `<span class="emoji-icon">${p.icon}</span>`;  
}  
  
function renderProducts(){  
  // Show skeleton briefly  
  const grid = document.getElementById('products-grid');  
  grid.innerHTML = Array(state.products.length||6).fill(0).map(()=>`<div class="product-card skeleton skel-card"></div>`).join('');  
  document.getElementById('empty-state').style.display='none';  
  
  setTimeout(()=>{  
    grid.innerHTML='';  
    if(!state.products.length){  
      document.getElementById('empty-state').style.display='block';  
      return;  
    }  
    state.products.forEach(p=>{  
      const card = document.createElement('div');  
      card.className='product-card';  
      card.dataset.name = p.name;  
  
      let optionsHTML='', pricesHTML='';  
      if(p.type==='countries'){  
        optionsHTML=`<div class="options"><div class="opt-grid">`+  
          COUNTRIES.map(c=>`<button class="opt-btn" onclick="selectCountry(this)">${c}</button>`).join('')+  
          `</div></div><div class="prices"><div class="price-list"></div></div>`;  
      } else {  
        // Use custom prices if defined, else default PUBG_UC  
        const priceItems = (p.prices && p.prices.length > 0) ? p.prices : PUBG_UC.map(uc=>({label:`${uc} UC`, price: Math.round(uc*0.11*state.USD)}));  
        const items = priceItems.map(item=>`<button class="price-btn" onclick="addToCart('${p.name} ${item.label}',${item.price})">  
          <span>${item.label}</span><span class="lyd">${item.price} **د**.**ل** <span class="add-icon">+</span></span></button>`).join('');  
        pricesHTML=`<div class="prices open"><div class="price-list">${items}</div></div>`;  
      }  
      const btnLabel = p.type==='countries'?'**عرض** **الأسعار** ↓':'**إخفاء** **الأسعار** ↑';  
      const btnClick = p.type==='countries'?'showOptions(this)':'showDirect(this)';  
      card.innerHTML=`  
        <div class="product-img-wrap">${makeImgHTML(p)}</div>  
        <h3>${p.name}</h3><p class="sub">${p.sub}</p>  
        <button class="show-btn" onclick="${btnClick}">${btnLabel}</button>  
        ${optionsHTML}${pricesHTML}`;  
      grid.appendChild(card);  
    });  
  }, 400);  
}  
  
function renderAll(){ renderDeal(); renderNav(); renderProducts(); }  
renderAll();  
  
/* ===== SEARCH ===== */  
function handleSearch(val){  
  const v = val.trim().toLowerCase();  
  const clear = document.getElementById('search-clear');  
  clear.style.display = v ? 'block' : 'none';  
  const cards = document.querySelectorAll('.product-card');  
  let visible = 0;  
  cards.forEach(c=>{  
    const name = c.dataset.name?.toLowerCase()||'';  
    const sub = c.querySelector('.sub')?.textContent.toLowerCase()||'';  
    const match = !v || name.includes(v) || sub.includes(v);  
    c.style.display = match ? '' : 'none';  
    if(match) visible++;  
  });  
  document.getElementById('empty-state').style.display = (!v && !visible) || (v && !visible) ? 'block' : 'none';  
  // Reset nav  
  if(v) document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));  
}  
function clearSearch(){  
  document.getElementById('search-input').value='';  
  document.getElementById('search-clear').style.display='none';  
  document.querySelectorAll('.product-card').forEach(c=>c.style.display='');  
  document.getElementById('empty-state').style.display='none';  
  document.querySelector('.nav-btn').classList.add('active');  
}  
  
/* ===== PRODUCT INTERACTION ===== */  
function showOptions(btn){  
  const card=btn.parentElement;  
  const opts=card.querySelector('.options');  
  const prices=card.querySelector('.prices');  
  const isOpen=opts.classList.contains('open');  
  opts.classList.toggle('open',!isOpen);  
  if(isOpen) prices.classList.remove('open');  
  btn.textContent=isOpen?'**عرض** **الأسعار** ↓':'**إخفاء** ↑';  
}  
function showDirect(btn){  
  const card=btn.parentElement;  
  const prices=card.querySelector('.prices');  
  const isOpen=prices.classList.contains('open');  
  prices.classList.toggle('open',!isOpen);  
  btn.textContent=isOpen?'**عرض** **الأسعار** ↓':'**إخفاء** **الأسعار** ↑';  
}  
function selectCountry(btn){  
  const card=btn.closest('.product-card');  
  const name=card.dataset.name;  
  const p=state.products.find(x=>x.name===name);  
  const pricesDiv=card.querySelector('.prices');  
  const list=pricesDiv.querySelector('.price-list');  
  list.innerHTML='';  
  pricesDiv.classList.add('open');  
  STD_AMOUNTS.forEach(amt=>{  
    const lyd=Math.round(amt*state.USD);  
    const b=document.createElement('button');  
    b.className='price-btn';  
    b.innerHTML=`<span>${name} $${amt} (${btn.textContent.trim()})</span><span class="lyd">${lyd} **د**.**ل** <span class="add-icon">+</span></span>`;  
    b.onclick=()=>addToCart(`${name} $${amt} (${btn.textContent.trim()})`,lyd);  
    list.appendChild(b);  
  });  
}  
  
/* ===== HOW TO ===== */  
function toggleHow(btn){  
  const content=btn.nextElementSibling;  
  const isOpen=content.classList.contains('open');  
  content.classList.toggle('open',!isOpen);  
  btn.classList.toggle('open',!isOpen);  
}  
  
/* ===== CART ===== */  
function toggleCart(){  
  const p=document.getElementById('cart-panel');  
  p.style.display=p.style.display==='block'?'none':'block';  
}  
function addToCart(name,price){  
  cart.push({name,price});  
  saveCart();  
  renderCart();  
  showToast(`✅ **تمت** **الإضافة**: ${name}`);  
  document.getElementById('cart-panel').style.display='block';  
}  
function removeFromCart(i){ cart.splice(i,1); saveCart(); renderCart(); }  
function clearCart(){  
  if(!cart.length){showToast('⚠️ **السلة** **فارغة**');return;}  
  cart=[];saveCart();renderCart();showToast('🗑 **تم** **إفراغ** **السلة**');  
}  
function renderCart(){  
  const itemsEl=document.getElementById('cart-items');  
  const totalEl=document.getElementById('total');  
  const countEl=document.getElementById('cart-count');  
  if(cart.length===0){  
    itemsEl.innerHTML='<p style="color:var(--muted);font-size:13px;text-align:center;padding:10px 0;">**السلة** **فارغة**</p>';  
    countEl.style.display='none';  
  } else {  
    itemsEl.innerHTML=cart.map((item,i)=>  
      `<div class="cart-item-row">  
        <span class="name">${item.name}</span>  
        <span style="display:flex;align-items:center;gap:6px;">  
          <span class="price">${item.price} **د**.**ل**</span>  
          <button class="rm" onclick="removeFromCart(${i})">✕</button>  
        </span>  
      </div>`).join('');  
    countEl.textContent=cart.length;  
    countEl.style.display='flex';  
  }  
  totalEl.textContent=cart.reduce((s,i)=>s+i.price,0);  
}  
renderCart();  
  
/* ===== ORDER FLOW ===== */  
function generateOrderId(){  
  return 'SX-' + Math.floor(100000 + Math.random()*900000);  
}  
function initiateCheckout(){  
  if(cart.length===0){showToast('⚠️ **السلة** **فارغة**!');return;}  
  const orderId = generateOrderId();  
  pendingOrder = {  
    id: orderId,  
    dbId: Date.now(),  
    items: [...cart],  
    total: cart.reduce((s,i)=>s+i.price,0),  
    time: new Date().toLocaleString('ar-LY',{timeZone:'Africa/Tripoli'}),  
    status:'new'  
  };  
  // Fill confirm modal  
  document.getElementById('modal-order-id').textContent = orderId;  
  document.getElementById('modal-items').innerHTML = pendingOrder.items.map(item=>  
    `<div class="confirm-item"><span>${item.name}</span><span class="c-price">${item.price} **د**.**ل**</span></div>`  
  ).join('');  
  document.getElementById('modal-total').textContent = pendingOrder.total + ' **د**.**ل**';  
  document.getElementById('confirm-modal').classList.add('show');  
}  
function closeConfirm(){  
  document.getElementById('confirm-modal').classList.remove('show');  
  pendingOrder = null;  
}  
function confirmOrder(){  
  if(!pendingOrder) return;  
  state.orders.unshift(pendingOrder);  
  // Add notification  
  const notif = {msg:`**طلب** **جديد** ${pendingOrder.id} — ${pendingOrder.total} **د**.**ل**`, time: pendingOrder.time};  
  state.notifications.unshift(notif);  
  if(state.notifications.length>50) state.notifications=state.notifications.slice(0,50);  
  save();  
  updateNotifDot();  
  
  let msg=`🛒 **طلب** **من** SOLIX\n **رقم** **الطلب**: ${pendingOrder.id}\n**━━━━━━━━━━━━━━━**\n`;  
  pendingOrder.items.forEach(item=>msg+=`• ${item.name} — ${item.price} **د**.**ل**\n`);  
  msg+=`**━━━━━━━━━━━━━━━**\n💰 **الإجمالي**: ${pendingOrder.total} **د**.**ل**`;  
  
  window.open(`[https://wa.me/${state.waNumber}?text=`+encodeURIComponent(msg),'_blank')](https://wa.me/$%7Bstate.waNumber%7D?text=%60+encodeURIComponent(msg),'_blank'));  
  cart=[]; saveCart(); renderCart();  
  closeConfirm();  
  document.getElementById('cart-panel').style.display='none';  
  showToast(`✅ **تم** **إرسال** **الطلب** ${pendingOrder?.id||''}`);  
}  
  
/* ===== NOTIFICATIONS ===== */  
function updateNotifDot(){  
  const dot=document.getElementById('notif-dot');  
  dot.style.display=state.notifications.length?'block':'none';  
}  
function toggleNotif(){  
  const p=document.getElementById('notif-panel');  
  const isOpen=p.style.display==='block';  
  p.style.display=isOpen?'none':'block';  
  if(!isOpen) renderNotifs();  
}  
function renderNotifs(){  
  const list=document.getElementById('notif-list');  
  if(!state.notifications.length){  
    list.innerHTML='<p class="notif-empty">**لا** **توجد** **إشعارات**</p>';  
    return;  
  }  
  list.innerHTML=state.notifications.slice(0,10).map(n=>  
    `<div class="notif-item">${n.msg}<div class="n-time">${n.time}</div></div>`  
  ).join('');  
}  
updateNotifDot();  
  
/* ===== TOAST ===== */  
let toastTimer;  
function showToast(msg){  
  const t=document.getElementById('toast');  
  t.textContent=msg; t.style.display='block';  
  clearTimeout(toastTimer);  
  toastTimer=setTimeout(()=>t.style.display='none',2500);  
}  
  
/* ===== LOGIN ===== */  
function openLogin(){  
  document.getElementById('login-overlay').classList.add('show');  
  document.getElementById('login-input').value='';  
  document.getElementById('login-error').textContent='';  
  setTimeout(()=>document.getElementById('login-input').focus(),100);  
}  
function closeLogin(){  
  document.getElementById('login-overlay').classList.remove('show');  
}  
function doLogin(){  
  const val=document.getElementById('login-input').value;  
  if(btoa(val)===state.adminPass){  
    closeLogin();  
    openAdmin();  
  } else {  
    document.getElementById('login-error').textContent='❌ **كلمة** **مرور** **خاطئة**';  
    document.getElementById('login-input').value='';  
  }  
}  
  
/* ===== ADMIN ===== */  
function showTab(id, btn){  
  document.querySelectorAll('.admin-section').forEach(s=>s.classList.remove('active'));  
  document.querySelectorAll('.a-tab').forEach(t=>t.classList.remove('active'));  
  document.getElementById(id).classList.add('active');  
  if(btn) btn.classList.add('active');  
  if(id==='tab-products') renderAdminProducts();  
  if(id==='tab-orders') renderOrders();  
  if(id==='tab-settings'){  
    document.getElementById('s-rate').value=state.USD;  
    document.getElementById('s-wa').value=state.waNumber;  
  }  
  if(id==='tab-deal'){  
    document.getElementById('d-name').value=state.deal.name;  
    document.getElementById('d-new').value=state.deal.newPrice;  
    document.getElementById('d-old').value=state.deal.oldPrice;  
  }  
}  
function openAdmin(){  
  document.getElementById('admin-overlay').style.display='block';  
  document.body.style.overflow='hidden';  
  renderAdminProducts();  
  document.getElementById('d-name').value=state.deal.name;  
  document.getElementById('d-new').value=state.deal.newPrice;  
  document.getElementById('d-old').value=state.deal.oldPrice;  
  document.getElementById('s-rate').value=state.USD;  
  document.getElementById('s-wa').value=state.waNumber;  
}  
function closeAdmin(){  
  document.getElementById('admin-overlay').style.display='none';  
  document.body.style.overflow='';  
}  
function saveDeal(){  
  const n=document.getElementById('d-name').value.trim();  
  const nw=parseFloat(document.getElementById('d-new').value);  
  const ol=parseFloat(document.getElementById('d-old').value);  
  if(!n||!nw){showToast('⚠️ **أكمل** **البيانات**');return;}  
  state.deal={name:n,newPrice:nw,oldPrice:ol||0};  
  save(); renderDeal(); showToast('✅ **تم** **حفظ** **العرض**');  
}  
function saveRate(){  
  const v=parseFloat(document.getElementById('s-rate').value);  
  if(v>0){state.USD=v;save();renderProducts();showToast(`✅ **سعر** **الصرف**: ${v}`);}  
  else showToast('⚠️ **أدخل** **قيمة** **صحيحة**');  
}  
function saveWA(){  
  const v=document.getElementById('s-wa').value.trim().replace(/\D/g,'');  
  if(v.length>6){state.waNumber=v;save();showToast('✅ **تم** **حفظ** **رقم** **الواتساب**');}  
  else showToast('⚠️ **رقم** **غير** **صحيح**');  
}  
function changePassword(){  
  const old=document.getElementById('s-old-pass').value;  
  const nw=document.getElementById('s-new-pass').value;  
  const conf=document.getElementById('s-confirm-pass').value;  
  if(btoa(old)!==state.adminPass){showToast('❌ **كلمة** **المرور** **الحالية** **خاطئة**');return;}  
  if(nw.length<6){showToast('⚠️ **كلمة** **المرور** **الجديدة** **قصيرة** **جداً** (6 **أحرف** **على** **الأقل**)');return;}  
  if(nw!==conf){showToast('⚠️ **كلمتا** **المرور** **غير** **متطابقتين**');return;}  
  state.adminPass=btoa(nw);  
  save();  
  document.getElementById('s-old-pass').value='';  
  document.getElementById('s-new-pass').value='';  
  document.getElementById('s-confirm-pass').value='';  
  showToast('✅ **تم** **تغيير** **كلمة** **المرور** **بنجاح**');  
}  
function addProduct(){  
  const name=document.getElementById('p-name').value.trim();  
  const icon=document.getElementById('p-icon').value.trim()||'📦';  
  const sub=document.getElementById('p-sub').value.trim()||'';  
  const img=document.getElementById('p-img').value.trim()||'';  
  const type=document.getElementById('p-type').value;  
  if(!name){showToast('⚠️ **أدخل** **اسم** **المنتج**');return;}  
  state.products.push({id:nextId++,name,icon,img,sub,type,prices:[]});  
  save(); renderAll(); renderAdminProducts();  
  document.getElementById('p-name').value='';  
  document.getElementById('p-icon').value='';  
  document.getElementById('p-sub').value='';  
  document.getElementById('p-img').value='';  
  showToast(`✅ **تمت** **إضافة** ${name}`);  
}  
function deleteProduct(id){  
  state.products=state.products.filter(p=>p.id!==id);  
  save(); renderAll(); renderAdminProducts(); showToast('🗑 **تم** **الحذف**');  
}  
function renderAdminProducts(){  
  const list=document.getElementById('admin-prod-list');  
  if(!state.products.length){list.innerHTML='<p style="color:var(--muted);font-size:13px;">**لا** **توجد** **منتجات**</p>';return;}  
  list.innerHTML=state.products.map(p=>`  
    <div class="prod-row">  
      <span class="prod-name">  
        <span class="prod-thumb">${p.img?`<img src="${p.img}" alt="" onerror="this.style.display='none'">`:p.icon}</span>  
        ${p.name}  
      </span>  
      <div class="prod-actions">  
        <button class="icon-btn" onclick="openEdit(${p.id})">✏️ **تعديل**</button>  
        <button class="icon-btn del" onclick="deleteProduct(${p.id})">🗑 **حذف**</button>  
      </div>  
    </div>`).join('');  
}  
  
/* ===== EDIT PRODUCT ===== */  
function openEdit(id){  
  const p=state.products.find(x=>x.id===id);  
  if(!p) return;  
  document.getElementById('e-id').value=id;  
  document.getElementById('e-name').value=p.name;  
  document.getElementById('e-icon').value=p.icon;  
  document.getElementById('e-sub').value=p.sub;  
  document.getElementById('e-img').value=p.img||'';  
  const pricesSec=document.getElementById('e-prices-section');  
  if(p.type==='direct'){  
    pricesSec.style.display='block';  
    renderEditPrices(p.prices||[]);  
  } else {  
    pricesSec.style.display='none';  
  }  
  document.getElementById('edit-modal').classList.add('show');  
}  
function renderEditPrices(prices){  
  const list=document.getElementById('e-price-list');  
  list.innerHTML=prices.map((pr,i)=>`  
    <div class="price-manage-item">  
      <input class="a-input" placeholder="**الاسم** (**مثال**: 600 UC)" value="${pr.label}" oninput="updateEditPrice(${i},'label',this.value)">  
      <input class="a-input" type="number" placeholder="**السعر** (**د**.**ل**)" value="${pr.price}" oninput="updateEditPrice(${i},'price',parseInt(this.value)||0)">  
      <button class="price-remove" onclick="removeEditPrice(${i})">✕</button>  
    </div>`).join('');  
}  
let editPricesTemp=[];  
function openEditFull(id){  
  const p=state.products.find(x=>x.id===id);  
  editPricesTemp=[...(p.prices||[])];  
}  
function updateEditPrice(i,key,val){  
  const id=parseInt(document.getElementById('e-id').value);  
  const p=state.products.find(x=>x.id===id);  
  if(!p||!p.prices[i]) return;  
  p.prices[i][key]=val;  
}  
function addEditPrice(){  
  const id=parseInt(document.getElementById('e-id').value);  
  const p=state.products.find(x=>x.id===id);  
  if(!p) return;  
  if(!p.prices) p.prices=[];  
  p.prices.push({label:'',price:0});  
  renderEditPrices(p.prices);  
}  
function removeEditPrice(i){  
  const id=parseInt(document.getElementById('e-id').value);  
  const p=state.products.find(x=>x.id===id);  
  if(!p) return;  
  p.prices.splice(i,1);  
  renderEditPrices(p.prices);  
}  
function saveEdit(){  
  const id=parseInt(document.getElementById('e-id').value);  
  const p=state.products.find(x=>x.id===id);  
  if(!p) return;  
  p.name=document.getElementById('e-name').value.trim()||p.name;  
  p.icon=document.getElementById('e-icon').value.trim()||p.icon;  
  p.sub=document.getElementById('e-sub').value.trim();  
  p.img=document.getElementById('e-img').value.trim();  
  save(); renderAll(); renderAdminProducts();  
  closeEdit(); showToast('✅ **تم** **تعديل** **المنتج**');  
}  
function closeEdit(){  
  document.getElementById('edit-modal').classList.remove('show');  
}  
  
/* ===== ORDERS ===== */  
function renderOrders(){  
  const tbody=document.getElementById('orders-body');  
  const stats=document.getElementById('order-stats');  
  const total=state.orders.reduce((s,o)=>s+o.total,0);  
  const newCount=state.orders.filter(o=>o.status==='new').length;  
  stats.innerHTML=`  
    <div class="stat-box"><div class="val">${state.orders.length}</div><div class="lbl">**إجمالي** **الطلبات**</div></div>  
    <div class="stat-box"><div class="val">${newCount}</div><div class="lbl">**طلبات** **جديدة**</div></div>  
    <div class="stat-box"><div class="val">${total}</div><div class="lbl">**إجمالي** **المبيعات** **د**.**ل**</div></div>`;  
  if(!state.orders.length){  
    tbody.innerHTML='<tr><td colspan="7" style="text-align:center;color:var(--muted);padding:20px;">**لا** **توجد** **طلبات** **بعد**</td></tr>';  
    return;  
  }  
  tbody.innerHTML=state.orders.map((o,i)=>`  
    <tr>  
      <td style="color:var(--muted)">#${state.orders.length-i}</td>  
      <td style="font-family:'Orbitron',sans-serif;font-size:11px;color:var(--blue)">${o.id||'—'}</td>  
      <td style="max-width:180px;font-size:12px;">${o.items.map(it=>it.name).join('<br>')}</td>  
      <td style="color:var(--blue);font-weight:700;">${o.total} **د**.**ل**</td>  
      <td style="font-size:11px;color:var(--muted);">${o.time}</td>  
      <td><span class="order-badge ${o.status==='new'?'new':'done'}">${o.status==='new'?'**جديد**':'**منجز**'}</span></td>  
      <td>  
        ${o.status==='new'?`<button class="icon-btn" onclick="markDone(${o.dbId})">✅</button>`:''}  
        <button class="icon-btn del" onclick="deleteOrder(${o.dbId})">🗑</button>  
      </td>  
    </tr>`).join('');  
}  
function markDone(id){  
  const o=state.orders.find(x=>x.dbId===id);  
  if(o){o.status='done';save();renderOrders();}  
}  
function deleteOrder(id){  
  state.orders=state.orders.filter(x=>x.dbId!==id);  
  save(); renderOrders(); showToast('🗑 **تم** **حذف** **الطلب**');  
}  
function clearOrders(){  
  if(confirm('**هل** **أنت** **متأكد** **من** **مسح** **جميع** **الطلبات؟**')){  
    state.orders=[];save();renderOrders();showToast('🗑 **تم** **مسح** **الطلبات**');  
  }  
}  
  
/* ===== SECRET KEY: Ctrl+Shift+Q ===== */  
(function(){  
  document.addEventListener('keydown',e=>{  
    if(e.ctrlKey&&e.shiftKey&&e.key==='Q'){  
      openLogin();  
    }  
  });  
})();  
</script>  
</body>  
</html>  
