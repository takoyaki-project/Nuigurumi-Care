/* ===== ぬいぐるみおせわ魔法帳 v3 — CSS ===== */
@import url('https://fonts.googleapis.com/css2?family=Zen+Maru+Gothic:wght@400;700;900&family=Yomogi&display=swap');

:root {
  --black:   #0D0A14;
  --deep:    #1A1028;
  --purple:  #6B21A8;
  --purple2: #9333EA;
  --purple3: #C084FC;
  --pink:    #EC4899;
  --pink2:   #F472B6;
  --pink3:   #FBCFE8;
  --white:   #FAF5FF;
  --star:    #E9D5FF;
  --gold:    #FDE68A;
  --glass:   rgba(255,255,255,0.07);
  --border2: rgba(192,132,252,0.5);
}

*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}

body{
  font-family:'Zen Maru Gothic',sans-serif;
  background:var(--black);
  min-height:100vh;
  display:flex;flex-direction:column;align-items:center;
  padding:0 0 60px;overflow-x:hidden;
}

/* ===== 背景 ===== */
.bg-layer{
  position:fixed;inset:0;z-index:0;
  background:
    radial-gradient(ellipse at 30% 0%,rgba(107,33,168,.6) 0%,transparent 55%),
    radial-gradient(ellipse at 80% 20%,rgba(236,72,153,.3) 0%,transparent 45%),
    radial-gradient(ellipse at 10% 70%,rgba(147,51,234,.4) 0%,transparent 50%),
    radial-gradient(ellipse at 90% 90%,rgba(236,72,153,.25) 0%,transparent 45%),
    #0D0A14;
}
.stars{position:fixed;inset:0;z-index:0;overflow:hidden;pointer-events:none;}
.star-dot{
  position:absolute;border-radius:50%;background:white;
  animation:twinkle var(--d) ease-in-out infinite alternate;
}
@keyframes twinkle{
  from{opacity:var(--a1);transform:scale(1);}
  to{opacity:var(--a2);transform:scale(1.6);}
}

/* ===== レイアウト ===== */
.wrapper{
  position:relative;z-index:10;
  width:100%;max-width:400px;
  display:flex;flex-direction:column;align-items:center;
  padding:0 14px;
}

/* ===== ヘッダー ===== */
.site-header{width:100%;text-align:center;padding:28px 0 16px;}
.header-deco{display:flex;align-items:center;justify-content:center;gap:8px;margin-bottom:6px;}
.header-deco span{font-size:1rem;animation:floatDeco 3s ease-in-out infinite;}
.header-deco span:nth-child(1){animation-delay:0s;}
.header-deco span:nth-child(3){animation-delay:.5s;}
.header-deco span:nth-child(5){animation-delay:1s;}
.gold{color:var(--gold);font-size:.9rem !important;}
@keyframes floatDeco{0%,100%{transform:translateY(0);}50%{transform:translateY(-5px);}}

.site-header h1{
  font-weight:900;font-size:1.45rem;letter-spacing:.08em;
  background:linear-gradient(135deg,#F472B6 0%,#C084FC 40%,#F9A8D4 70%,#FDE68A 100%);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
  filter:drop-shadow(0 0 12px rgba(236,72,153,.5));
}
.header-sub{font-family:'Yomogi',sans-serif;font-size:.7rem;color:var(--purple3);margin-top:4px;letter-spacing:.1em;}

/* ===== グラスカード共通 ===== */
.glass-card{
  background:var(--glass);
  backdrop-filter:blur(16px);-webkit-backdrop-filter:blur(16px);
  border:1.5px solid var(--border2);border-radius:26px;
  width:100%;padding:18px 16px;margin-bottom:12px;
  box-shadow:0 8px 32px rgba(0,0,0,.4),inset 0 1px 0 rgba(255,255,255,.1),0 0 0 1px rgba(192,132,252,.15);
  position:relative;overflow:hidden;
}
.glass-card::before{
  content:'';position:absolute;top:0;left:0;right:0;height:1px;
  background:linear-gradient(90deg,transparent,rgba(240,171,252,.6),transparent);
}
.ribbon-corner{
  position:absolute;top:10px;right:12px;font-size:1rem;opacity:.7;
  animation:spinRibbon 6s ease-in-out infinite alternate;
}
@keyframes spinRibbon{from{transform:rotate(-10deg) scale(1);}to{transform:rotate(10deg) scale(1.1);}}
.card-title{font-size:.7rem;font-weight:700;color:var(--purple3);letter-spacing:.1em;margin-bottom:10px;}

/* ===== キャラカード ===== */
.chara-card{display:flex;flex-direction:column;align-items:center;gap:10px;}

/* レベルバッジ */
.level-badge{
  display:flex;align-items:center;gap:8px;
  background:linear-gradient(135deg,rgba(147,51,234,.4),rgba(236,72,153,.3));
  border:1px solid rgba(192,132,252,.5);border-radius:30px;
  padding:4px 14px;
  box-shadow:0 0 12px rgba(147,51,234,.3);
}
.lv-num{
  font-weight:900;font-size:.85rem;
  background:linear-gradient(135deg,var(--gold),var(--pink2));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
}
.lv-name{font-size:.78rem;color:var(--star);font-weight:700;}

/* 写真エリア */
.photo-area{position:relative;display:flex;flex-direction:column;align-items:center;}
.photo-frame-outer{position:relative;width:136px;height:136px;}
.photo-frame-ring{
  position:absolute;inset:-6px;border-radius:50%;
  background:conic-gradient(from 0deg,#EC4899,#9333EA,#C084FC,#F472B6,#FDE68A,#EC4899);
  animation:rotatRing 4s linear infinite;filter:blur(2px);
}
@keyframes rotatRing{to{transform:rotate(360deg);}}
.photo-frame-inner{
  position:absolute;inset:4px;border-radius:50%;background:var(--deep);
  overflow:hidden;cursor:pointer;transition:transform .2s;
}
.photo-frame-inner:active{transform:scale(.95);}
.photo-frame-inner img{width:100%;height:100%;object-fit:cover;display:block;}
.photo-placeholder{
  width:100%;height:100%;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:4px;
  background:radial-gradient(circle at center,rgba(107,33,168,.4) 0%,transparent 70%);
}
.photo-placeholder .cam{font-size:1.6rem;}
.photo-placeholder p{font-size:.58rem;color:var(--purple3);text-align:center;line-height:1.4;font-family:'Yomogi',sans-serif;}
#fileInput{display:none;}

/* ── 表情オーバーレイ ── */
.face-overlay{
  position:absolute;
  bottom:-10px;right:-10px;
  font-size:2.2rem;
  opacity:0;
  transform:scale(0) rotate(-20deg);
  transition:opacity .25s,transform .25s;
  filter:drop-shadow(0 2px 8px rgba(236,72,153,.6));
  pointer-events:none;z-index:20;
}
.face-overlay.show{
  opacity:1;transform:scale(1) rotate(0deg);
  animation:faceBounce .4s cubic-bezier(.34,1.56,.64,1);
}
.face-overlay.hide{opacity:0;transform:scale(0) rotate(20deg);}
@keyframes faceBounce{
  0%{transform:scale(0) rotate(-20deg);}
  60%{transform:scale(1.2) rotate(5deg);}
  100%{transform:scale(1) rotate(0deg);}
}

/* ── 吹き出し ── */
.speech-bubble{
  position:absolute;
  top:-14px;left:50%;transform:translateX(-20%);
  background:white;
  border-radius:18px;
  padding:6px 14px;
  font-family:'Yomogi',sans-serif;font-size:.82rem;
  color:#5C3D5C;font-weight:700;white-space:nowrap;
  box-shadow:0 4px 16px rgba(147,51,234,.25);
  opacity:0;pointer-events:none;z-index:30;
  transition:opacity .2s,transform .2s;
  transform:translateX(-20%) scale(.7) translateY(10px);
}
.speech-bubble::after{
  content:'';position:absolute;bottom:-8px;left:28px;
  border-top:9px solid white;border-left:7px solid transparent;border-right:7px solid transparent;
}
.speech-bubble.show{
  opacity:1;transform:translateX(-20%) scale(1) translateY(0);
  animation:bubblePop .35s cubic-bezier(.34,1.56,.64,1);
}
.speech-bubble.hide{opacity:0;transform:translateX(-20%) scale(.8) translateY(-6px);}
@keyframes bubblePop{
  0%{transform:translateX(-20%) scale(.5) translateY(10px);}
  70%{transform:translateX(-20%) scale(1.05) translateY(-2px);}
  100%{transform:translateX(-20%) scale(1) translateY(0);}
}

/* 名前 */
.name-section{text-align:center;width:100%;}
.name-label-row{display:flex;align-items:center;justify-content:center;gap:6px;margin-bottom:4px;}
.name-label-row span{font-size:.68rem;}
.name-lbl{color:var(--purple3);}
#nameInput{
  font-family:'Zen Maru Gothic',sans-serif;font-weight:700;font-size:1.2rem;
  background:transparent;border:none;
  border-bottom:2px solid transparent;
  border-image:linear-gradient(90deg,var(--pink),var(--purple2)) 1;
  color:var(--white);text-align:center;width:200px;outline:none;
  padding:3px 8px;caret-color:var(--pink2);
}
#nameInput::placeholder{color:rgba(192,132,252,.4);font-size:.82rem;font-weight:400;}

/* ===== お願い ===== */
.wish-card{display:flex;align-items:center;gap:10px;padding:12px 16px;}
.wish-icon{font-size:1.9rem;animation:wishBounce 2s ease-in-out infinite;flex-shrink:0;}
@keyframes wishBounce{0%,100%{transform:scale(1) rotate(-5deg);}50%{transform:scale(1.15) rotate(5deg);}}
.wish-texts{flex:1;}
.wish-label{font-size:.58rem;color:var(--purple3);letter-spacing:.08em;margin-bottom:2px;}
.wish-text{font-size:.88rem;font-weight:700;color:var(--pink3);line-height:1.3;font-family:'Yomogi',sans-serif;}
.wish-hint{
  font-size:.58rem;color:var(--gold);font-family:'Yomogi',sans-serif;
  background:rgba(253,230,138,.1);border:1px solid rgba(253,230,138,.3);
  border-radius:10px;padding:2px 8px;white-space:nowrap;flex-shrink:0;
}

/* ===== ごきげん ===== */
.mood-card{}
.mood-title-row{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;}
.mood-title{font-size:.72rem;font-weight:700;color:var(--pink2);letter-spacing:.1em;}
.mood-num-display{
  font-weight:900;font-size:1.45rem;
  background:linear-gradient(135deg,var(--pink2),var(--purple3));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
}
.mood-num-display sup{font-size:.6rem;opacity:.7;}
.bar-track{
  width:100%;height:18px;background:rgba(255,255,255,.06);
  border-radius:100px;border:1px solid rgba(192,132,252,.3);
  overflow:hidden;margin-bottom:7px;
}
.bar-glow{
  height:100%;border-radius:100px;
  background:linear-gradient(90deg,#9333EA 0%,#EC4899 50%,#FDE68A 100%);
  width:0%;transition:width .6s cubic-bezier(.34,1.56,.64,1);
  position:relative;box-shadow:0 0 12px rgba(236,72,153,.6);
}
.bar-glow::after{
  content:'';position:absolute;right:-2px;top:50%;transform:translateY(-50%);
  width:20px;height:20px;border-radius:50%;background:white;
  box-shadow:0 0 8px rgba(236,72,153,.9),0 0 16px rgba(147,51,234,.5);
  border:2px solid rgba(255,255,255,.8);
}
.bar-glow[data-z="1"]::after{display:none;}
.mood-emoji-row{display:flex;justify-content:space-between;padding:0 3px;}
.mood-emoji-row span{font-size:.58rem;color:rgba(192,132,252,.7);}

/* ===== ボタン ===== */
.btn-section{width:100%;gap:9px;margin-bottom:9px;display:grid;}
.btn-row3{grid-template-columns:repeat(3,1fr);}
.btn-row2{grid-template-columns:repeat(2,1fr);}

.action-btn{
  position:relative;border:none;outline:none;border-radius:20px;
  padding:14px 6px 12px;cursor:pointer;
  display:flex;flex-direction:column;align-items:center;gap:6px;
  font-family:'Zen Maru Gothic',sans-serif;
  transition:transform .12s,box-shadow .12s;
  -webkit-tap-highlight-color:transparent;overflow:visible;
}
.btn-gohan{background:linear-gradient(180deg,#F472B6,#DB2777);box-shadow:0 5px 0 #9D174D,0 7px 14px rgba(236,72,153,.5),inset 0 1px 0 rgba(255,255,255,.35);}
.btn-ofuro{background:linear-gradient(180deg,#C084FC,#7C3AED);box-shadow:0 5px 0 #4C1D95,0 7px 14px rgba(147,51,234,.5),inset 0 1px 0 rgba(255,255,255,.35);}
.btn-asobu{background:linear-gradient(180deg,#818CF8,#4F46E5);box-shadow:0 5px 0 #312E81,0 7px 14px rgba(99,102,241,.5),inset 0 1px 0 rgba(255,255,255,.35);}
.btn-sanpo{background:linear-gradient(180deg,#34D399,#059669);box-shadow:0 5px 0 #064E3B,0 7px 14px rgba(5,150,105,.5),inset 0 1px 0 rgba(255,255,255,.35);}
.btn-neru{background:linear-gradient(180deg,#60A5FA,#2563EB);box-shadow:0 5px 0 #1E3A8A,0 7px 14px rgba(37,99,235,.5),inset 0 1px 0 rgba(255,255,255,.35);}
.action-btn:active{transform:translateY(4px) scale(.97);}
.btn-gohan:active{box-shadow:0 1px 0 #9D174D,0 2px 5px rgba(236,72,153,.3),inset 0 1px 0 rgba(255,255,255,.2);}
.btn-ofuro:active{box-shadow:0 1px 0 #4C1D95,0 2px 5px rgba(147,51,234,.3),inset 0 1px 0 rgba(255,255,255,.2);}
.btn-asobu:active{box-shadow:0 1px 0 #312E81,0 2px 5px rgba(99,102,241,.3),inset 0 1px 0 rgba(255,255,255,.2);}
.btn-sanpo:active{box-shadow:0 1px 0 #064E3B,0 2px 5px rgba(5,150,105,.3),inset 0 1px 0 rgba(255,255,255,.2);}
.btn-neru:active{box-shadow:0 1px 0 #1E3A8A,0 2px 5px rgba(37,99,235,.3),inset 0 1px 0 rgba(255,255,255,.2);}

.action-btn::before{
  content:'';position:absolute;top:0;left:0;right:0;height:44%;
  border-radius:20px 20px 50% 50%;background:rgba(255,255,255,.18);pointer-events:none;
}
/* お願いマッチ */
.action-btn.wish-match{outline:2px solid var(--gold);outline-offset:2px;}
.action-btn.wish-match::after{
  content:'⭐ボーナス！';
  position:absolute;top:-22px;left:50%;transform:translateX(-50%);
  font-size:.58rem;color:var(--gold);white-space:nowrap;
  background:rgba(0,0,0,.55);border-radius:8px;padding:2px 6px;
  font-family:'Yomogi',sans-serif;animation:badgePop .4s ease;
}
@keyframes badgePop{from{opacity:0;transform:translateX(-50%) scale(.5);}}

.btn-emoji{font-size:1.75rem;filter:drop-shadow(0 2px 4px rgba(0,0,0,.3));}
.btn-label{font-size:.72rem;font-weight:700;color:white;text-shadow:0 1px 3px rgba(0,0,0,.3);letter-spacing:.04em;}
.btn-badge{background:rgba(255,255,255,.25);border-radius:20px;font-size:.58rem;color:white;padding:1px 7px;font-weight:700;}

/* ===== アイテム ===== */
.item-card{}
.item-grid{display:flex;flex-wrap:wrap;gap:7px;min-height:40px;}
.item-empty{font-size:.7rem;color:rgba(192,132,252,.5);font-family:'Yomogi',sans-serif;padding:4px;line-height:1.5;}
.item-chip{
  display:flex;align-items:center;gap:5px;
  background:rgba(255,255,255,.08);border:1px solid rgba(192,132,252,.3);
  border-radius:30px;padding:4px 11px;font-size:.78rem;color:var(--star);
  animation:chipIn .35s cubic-bezier(.34,1.56,.64,1);
}
@keyframes chipIn{from{transform:scale(0);opacity:0;}}
.chip-icon{font-size:1rem;}
.chip-name{font-size:.65rem;font-family:'Yomogi',sans-serif;}
.chip-cnt{font-size:.55rem;background:rgba(192,132,252,.25);border-radius:20px;padding:1px 5px;color:var(--purple3);font-weight:700;}

/* ===== ログ ===== */
.log-card{}
#activityList{list-style:none;display:flex;flex-direction:column;gap:5px;}
#activityList li{
  font-size:.72rem;color:var(--star);
  background:rgba(255,255,255,.05);border:1px solid rgba(192,132,252,.2);
  border-radius:11px;padding:6px 11px;
  animation:slideInLog .3s ease;font-family:'Yomogi',sans-serif;
}
@keyframes slideInLog{from{opacity:0;transform:translateX(-12px);}}
.log-empty{font-size:.7rem;color:rgba(192,132,252,.5);text-align:center;font-family:'Yomogi',sans-serif;}

/* ===== フロートメッセージ ===== */
.float-msg{
  position:fixed;left:50%;top:45%;
  transform:translate(-50%,-50%) scale(.8);
  background:linear-gradient(135deg,rgba(107,33,168,.95),rgba(30,0,50,.95));
  border:1.5px solid var(--pink2);border-radius:20px;padding:10px 22px;
  font-weight:700;font-size:1rem;color:var(--pink3);
  pointer-events:none;opacity:0;z-index:500;
  box-shadow:0 8px 32px rgba(236,72,153,.4);
  white-space:nowrap;text-align:center;
}
.float-msg.show{animation:floatPop 1.8s ease forwards;}
@keyframes floatPop{
  0%{opacity:0;transform:translate(-50%,-30%) scale(.7);}
  15%{opacity:1;transform:translate(-50%,-50%) scale(1.05);}
  70%{opacity:1;transform:translate(-50%,-60%) scale(1);}
  100%{opacity:0;transform:translate(-50%,-80%) scale(.9);}
}

/* ===== ごほうびポップアップ ===== */
.reward-popup{
  position:fixed;left:50%;bottom:20%;transform:translateX(-50%) scale(0);
  background:white;border-radius:20px;padding:12px 22px;
  display:flex;flex-direction:column;align-items:center;gap:4px;
  box-shadow:0 8px 28px rgba(147,51,234,.4);
  pointer-events:none;opacity:0;z-index:600;
  border:2px solid var(--purple3);
}
.reward-popup.show{animation:rewardPop 2.2s ease forwards;}
@keyframes rewardPop{
  0%{opacity:0;transform:translateX(-50%) scale(0);}
  12%{opacity:1;transform:translateX(-50%) scale(1.1);}
  20%{transform:translateX(-50%) scale(1);}
  75%{opacity:1;transform:translateX(-50%) scale(1) translateY(0);}
  100%{opacity:0;transform:translateX(-50%) scale(.9) translateY(-20px);}
}
.reward-icon{font-size:2rem;animation:rewardSpin 1s ease infinite alternate;}
@keyframes rewardSpin{from{transform:rotate(-10deg) scale(1);}to{transform:rotate(10deg) scale(1.15);}}
.reward-text{font-family:'Yomogi',sans-serif;font-size:.82rem;color:#5C3D5C;font-weight:700;text-align:center;}

/* ===== レアリアクション ===== */
.rare-overlay{
  display:none;position:fixed;inset:0;z-index:800;
  background:radial-gradient(ellipse at center,rgba(107,33,168,.6) 0%,rgba(10,5,20,.9) 70%);
  flex-direction:column;align-items:center;justify-content:center;
  text-align:center;padding:24px;
}
.rare-overlay.active{display:flex;animation:rareIn .4s ease;}
@keyframes rareIn{from{opacity:0;}to{opacity:1;}}
.rare-inner{display:flex;flex-direction:column;align-items:center;gap:6px;}
.rare-emoji{font-size:4rem;animation:rareSpin 1.5s ease-in-out infinite;}
@keyframes rareSpin{0%,100%{transform:scale(1) rotate(-10deg);}50%{transform:scale(1.25) rotate(10deg);}}
.rare-title{
  font-weight:900;font-size:2.2rem;letter-spacing:.06em;
  background:linear-gradient(135deg,#FDE68A,#F472B6,#C084FC,#FDE68A);
  background-size:200% auto;
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
  animation:rareShimmer 1.2s linear infinite;
  filter:drop-shadow(0 0 18px rgba(236,72,153,.8));
}
@keyframes rareShimmer{to{background-position:200% center;}}
.rare-sub{font-family:'Yomogi',sans-serif;font-size:.85rem;color:var(--purple3);}

/* ===== オーバーレイ共通 ===== */
.overlay{
  display:none;position:fixed;inset:0;z-index:900;
  background:rgba(10,5,20,.92);backdrop-filter:blur(8px);
  flex-direction:column;align-items:center;justify-content:center;
  text-align:center;padding:28px;
}
.overlay.active{display:flex;}
.overlay-btn{
  margin-top:18px;
  background:linear-gradient(135deg,#EC4899,#9333EA);
  border:none;border-radius:30px;padding:12px 30px;
  font-family:'Zen Maru Gothic',sans-serif;font-weight:700;font-size:.95rem;
  color:white;cursor:pointer;
  box-shadow:0 6px 0 #581C87,0 10px 24px rgba(147,51,234,.5);
  transition:transform .12s;letter-spacing:.05em;
}
.overlay-btn:active{transform:translateY(4px);box-shadow:0 2px 0 #581C87;}

/* ===== レベルアップ ===== */
#lvupOverlay{gap:0;}
.lvup-box{
  position:relative;
  background:rgba(20,10,35,.95);border:2px solid var(--purple3);border-radius:30px;
  padding:28px 24px 20px;width:100%;max-width:310px;
  display:flex;flex-direction:column;align-items:center;
}
.lvup-stars-bg{position:absolute;inset:0;pointer-events:none;overflow:hidden;border-radius:28px;}
.lvup-emoji{font-size:2.6rem;animation:floatDeco 2s ease-in-out infinite;}
.lvup-title{
  font-weight:900;font-size:1.9rem;letter-spacing:.08em;margin:8px 0 4px;
  background:linear-gradient(135deg,#FDE68A,#F472B6,#C084FC);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
  filter:drop-shadow(0 0 14px rgba(236,72,153,.6));
}
.lvup-lv{font-weight:700;font-size:1rem;color:var(--star);margin-bottom:14px;letter-spacing:.05em;}
.lvup-item-wrap{
  background:rgba(255,255,255,.06);border:1px solid rgba(192,132,252,.4);
  border-radius:18px;padding:12px 22px;
  display:flex;flex-direction:column;align-items:center;gap:3px;width:100%;
}
.lvup-item-label{font-size:.65rem;color:var(--purple3);letter-spacing:.08em;font-family:'Yomogi',sans-serif;}
.lvup-item-icon{font-size:2.3rem;animation:itemSpin 1s ease-in-out infinite alternate;}
@keyframes itemSpin{from{transform:rotate(-10deg) scale(1);}to{transform:rotate(10deg) scale(1.2);}}
.lvup-item-name{font-size:.85rem;font-weight:700;color:var(--gold);font-family:'Yomogi',sans-serif;}

/* ===== だいまんぞく ===== */
#perfectOverlay{gap:6px;}
.perf-ribbon{font-size:2.8rem;animation:ribbonSpin 2s ease-in-out infinite alternate;}
@keyframes ribbonSpin{from{transform:rotate(-15deg) scale(1);}to{transform:rotate(15deg) scale(1.15);}}
.perf-title{
  font-weight:900;font-size:2.6rem;letter-spacing:.05em;
  background:linear-gradient(135deg,#F472B6,#FDE68A,#C084FC,#F9A8D4);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
  filter:drop-shadow(0 0 20px rgba(236,72,153,.7));
  animation:shimmer 1.5s ease-in-out infinite alternate;
}
@keyframes shimmer{
  from{filter:drop-shadow(0 0 12px rgba(236,72,153,.7));}
  to{filter:drop-shadow(0 0 28px rgba(240,171,252,.9));}
}
.perf-hearts{font-size:1.3rem;letter-spacing:6px;animation:heartBeat .8s ease infinite;}
@keyframes heartBeat{0%,100%{transform:scale(1);}50%{transform:scale(1.15);}}
.perf-sub{font-size:.9rem;color:var(--purple3);font-family:'Yomogi',sans-serif;line-height:1.6;}

/* ===== パーティクル ===== */
.kira{position:fixed;pointer-events:none;z-index:950;font-size:var(--ks);animation:kiraFly var(--kt) ease forwards;}
@keyframes kiraFly{
  0%{opacity:1;transform:translate(0,0) scale(.3) rotate(0deg);}
  80%{opacity:1;}
  100%{opacity:0;transform:translate(var(--kx),var(--ky)) scale(1.2) rotate(var(--kr));}
}
.heart-pop{position:fixed;pointer-events:none;z-index:800;font-size:1rem;animation:heartPop 1s ease forwards;}
@keyframes heartPop{
  0%{opacity:1;transform:translateY(0) scale(.5) rotate(var(--hr));}
  100%{opacity:0;transform:translateY(-80px) scale(1.1) rotate(var(--hr));}
}