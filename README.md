// ===== ぬいぐるみおせわ魔法帳 v3 — JavaScript =====

// ──────────────────────────────────────────
// 定数
// ──────────────────────────────────────────
var LEVELS = [
  {lv:1,name:'みならい'},
  {lv:2,name:'なかよし'},
  {lv:3,name:'おしゃれさん'},
  {lv:4,name:'きらきらスター'},
  {lv:5,name:'だいすきパートナー'}
];

var LEVEL_ITEMS = [
  {icon:'🎀',name:'リボン'},
  {icon:'👑',name:'ティアラ'},
  {icon:'⭐',name:'ほし'},
  {icon:'💎',name:'ジュエル'},
  {icon:'🖤',name:'小悪魔ハート'},
  {icon:'🌙',name:'まほうのつき'},
  {icon:'💜',name:'むらさきハート'}
];

var REACTIONS = {
  gohan:{
    face: ['😋','😊','🥰'],
    lines:['おいしい〜♪','もぐもぐ！','しあわせ♡','うまうま〜！']
  },
  ofuro:{
    face: ['😊','🥰','😆'],
    lines:['ピカピカ！','あわあわ〜♪','きもちいい！','つるつる〜♪']
  },
  asobu:{
    face: ['😆','🤩','😊'],
    lines:['たのしい！','わーい！','もっとあそぼ！','ひゃっほう♪']
  },
  sanpo:{
    face: ['😊','😆','🥰'],
    lines:['おそとだいすき！','いいかぜ〜♪','るんるん♪','どこいこっか！']
  },
  neru:{
    face: ['😴','🥰','😊'],
    lines:['すやぁ…','おやすみ〜','いいゆめみるね','zzz…']
  }
};

var SANPO_LOG = ['おそとたのしい♪','いいおてんき！','たくさんあるいたよ！'];
var NERU_LOG  = ['すやすや…','おやすみなさい♪','いいゆめみるね！'];

var REWARDS = [
  {icon:'🎁',name:'クッキー',label:'クッキーをみつけた！'},
  {icon:'⭐',name:'ほしのかけら',label:'おほしさまをひろった！'},
  {icon:'💎',name:'キラキラストーン',label:'キラキラストーンをゲット！'},
  {icon:'🎀',name:'リボン',label:'リボンをひろった！'},
  {icon:'🍭',name:'キャンディ',label:'キャンディがあった！'},
  {icon:'🌸',name:'さくらのはな',label:'さくらのはなびらをひろった！'}
];

var RARES = [
  {icon:'✨',title:'ひみつのダンス！'},
  {icon:'🌈',title:'にじいろまほう発動！'},
  {icon:'🖤',title:'きらきらへんしん！'},
  {icon:'⭐',title:'ラッキースター出現！'}
];

var WISHES = [
  {key:'gohan',icon:'🍙',text:'ごはんが たべたいな〜'},
  {key:'ofuro',icon:'🛁',text:'おふろに はいりたいな〜'},
  {key:'asobu',icon:'🎀',text:'いっしょに あそびたいな〜'},
  {key:'sanpo',icon:'🚶',text:'おさんぽ したいな〜'},
  {key:'neru', icon:'😴',text:'ねむくなってきたよ〜'}
];

// ──────────────────────────────────────────
// ステート
// ──────────────────────────────────────────
var mood         = 0;
var level        = 1;
var items        = {};   // {name:{icon,name,count}}
var logs         = [];
var currentWish  = null;
var pendingLvup  = false;
var busy         = false; // アニメ重複防止

// ──────────────────────────────────────────
// 初期化
// ──────────────────────────────────────────
makeStar();
pickNewWish();
updateLevelUI();

// ──────────────────────────────────────────
// 星空
// ──────────────────────────────────────────
function makeStar(){
  var c=document.getElementById('starsContainer');
  for(var i=0;i<80;i++){
    var d=document.createElement('div');
    d.className='star-dot';
    var s=1+Math.random()*2.5;
    d.style.cssText='width:'+s+'px;height:'+s+'px;left:'+(Math.random()*100)+'vw;top:'+(Math.random()*100)+'vh;--d:'+(2+Math.random()*4)+'s;--a1:'+(0.1+Math.random()*.5)+';--a2:'+(0.5+Math.random()*.5);
    c.appendChild(d);
  }
}

// ──────────────────────────────────────────
// 写真
// ──────────────────────────────────────────
document.getElementById('fileInput').addEventListener('change',function(e){
  var f=e.target.files[0];if(!f)return;
  var r=new FileReader();
  r.onload=function(ev){
    var img=document.getElementById('plushPhoto');
    img.src=ev.target.result;img.style.display='block';
    document.getElementById('placeholder').style.display='none';
  };
  r.readAsDataURL(f);
});

// ──────────────────────────────────────────
// メインアクション
// ──────────────────────────────────────────
function doAction(btn, label, emoji, key, basePts){
  if(busy) return;
  busy = true;

  spawnHearts(btn);

  // お願いマッチ判定
  var bonus = currentWish && currentWish.key === key;
  var pts   = bonus ? basePts + 15 : basePts;

  // ① 表情
  var reac  = REACTIONS[key];
  var face  = pick(reac.face);
  showFace(face);

  // ② 吹き出し
  var line  = pick(reac.lines);
  showBubble(line);

  // バー更新
  var prev = mood;
  mood = Math.min(100, mood + pts);
  animateBar(prev, mood);

  // フロートメッセージ
  showFloatMsg(bonus
    ? emoji+' ボーナス！+'+pts+' ごきげんUp！⭐'
    : emoji+' ごきげん +'+pts+'！'
  );

  // ログ
  var plushName = getPlushName();
  var t = pad(new Date().getHours())+':'+pad(new Date().getMinutes());
  var logTxt = emoji+' '+plushName+'に'+label+'をした';

  // おさんぽ・ねかしつけ特有ログ
  if(key==='sanpo') logTxt += ' — '+pick(SANPO_LOG);
  if(key==='neru')  logTxt += ' — '+pick(NERU_LOG);
  if(bonus) logTxt += ' ★ボーナス！';
  logTxt += ' ('+t+')';

  logs.unshift(logTxt);
  if(logs.length>6) logs.pop();
  renderLogs();

  // お願いをかなえたら新しいお願いへ
  if(bonus) setTimeout(pickNewWish, 600);

  // ③④ ごほうび・レア抽選（少し遅延してから）
  setTimeout(function(){
    var rand = Math.random();
    if(rand < 0.05){
      // レア (5%)
      doRare();
    } else if(rand < 0.17){
      // ごほうび (12%)
      doReward();
    }
  }, 500);

  // 満足チェック
  if(mood >= 100){
    pendingLvup = true;
    setTimeout(showPerfect, 1000);
  }

  // busy解除
  setTimeout(function(){ busy = false; }, 600);
}

// ──────────────────────────────────────────
// ① 表情
// ──────────────────────────────────────────
function showFace(emoji){
  var el = document.getElementById('faceOverlay');
  el.textContent = emoji;
  el.className = 'face-overlay';
  void el.offsetWidth;
  el.className = 'face-overlay show';
  setTimeout(function(){
    el.className = 'face-overlay hide';
    setTimeout(function(){ el.className='face-overlay'; }, 300);
  }, 1800);
}

// ──────────────────────────────────────────
// ② 吹き出し
// ──────────────────────────────────────────
function showBubble(text){
  var el = document.getElementById('speechBubble');
  el.textContent = text;
  el.className = 'speech-bubble';
  void el.offsetWidth;
  el.className = 'speech-bubble show';
  setTimeout(function(){
    el.className = 'speech-bubble hide';
    setTimeout(function(){ el.className='speech-bubble'; }, 300);
  }, 2000);
}

// ──────────────────────────────────────────
// ③ ごほうび
// ──────────────────────────────────────────
function doReward(){
  var r = pick(REWARDS);
  // コレクションに追加
  addItem({icon:r.icon, name:r.name});

  // ポップアップ
  var popup = document.getElementById('rewardPopup');
  document.getElementById('rewardIcon').textContent = r.icon;
  document.getElementById('rewardText').textContent = r.label;
  popup.className = 'reward-popup';
  void popup.offsetWidth;
  popup.className = 'reward-popup show';

  // ログ
  logs.unshift('🎁 '+r.label+' ('+pad(new Date().getHours())+':'+pad(new Date().getMinutes())+')');
  if(logs.length>6) logs.pop();
  renderLogs();

  // 小キラキラ
  for(var i=0;i<3;i++){
    (function(i){setTimeout(function(){ spawnKira(8); },i*350);})(i);
  }

  setTimeout(function(){ popup.className='reward-popup'; }, 2500);
}

// ──────────────────────────────────────────
// ④ レアリアクション
// ──────────────────────────────────────────
function doRare(){
  var r = pick(RARES);
  var overlay = document.getElementById('rareOverlay');
  document.getElementById('rareEmoji').textContent  = r.icon;
  document.getElementById('rareTitle').textContent  = r.title;
  overlay.classList.add('active');

  // 大キラキラ連射
  for(var w=0;w<5;w++){
    (function(w){ setTimeout(function(){ spawnKira(16); }, w*400); })(w);
  }

  // ログ
  logs.unshift('✨ レアリアクション！「'+r.title+'」('+pad(new Date().getHours())+':'+pad(new Date().getMinutes())+')');
  if(logs.length>6) logs.pop();
  renderLogs();

  // 2.5秒後自動閉じ
  setTimeout(function(){
    overlay.classList.remove('active');
  }, 2500);
}

// ──────────────────────────────────────────
// お願い
// ──────────────────────────────────────────
function pickNewWish(){
  var pool = WISHES.filter(function(w){ return !currentWish || w.key !== currentWish.key; });
  currentWish = pool[Math.floor(Math.random()*pool.length)];
  document.getElementById('wishIcon').textContent = currentWish.icon;
  document.getElementById('wishText').textContent = currentWish.text;
  updateWishHighlight();
}

function updateWishHighlight(){
  var map = {gohan:'btnGohan',ofuro:'btnOfuro',asobu:'btnAsobu',sanpo:'btnSanpo',neru:'btnNeru'};
  Object.keys(map).forEach(function(k){
    var el = document.getElementById(map[k]);
    if(el) el.classList.toggle('wish-match', currentWish && k===currentWish.key);
  });
}

// ──────────────────────────────────────────
// バーアニメ
// ──────────────────────────────────────────
function animateBar(from, to){
  var start=null;
  var fill=document.getElementById('barGlow');
  var num=document.getElementById('moodNum');
  function step(ts){
    if(!start) start=ts;
    var p=Math.min((ts-start)/650,1);
    var e=1-Math.pow(1-p,3);
    var cur=Math.round(from+(to-from)*e);
    fill.style.width=cur+'%';
    if(cur>0) fill.removeAttribute('data-z'); else fill.setAttribute('data-z','1');
    num.textContent=cur;
    if(p<1) requestAnimationFrame(step);
  }
  requestAnimationFrame(step);
}

// ──────────────────────────────────────────
// だいまんぞく
// ──────────────────────────────────────────
function showPerfect(){
  var name=getPlushName();
  document.getElementById('perfSub').innerHTML='<strong style="color:#F9A8D4">'+name+'</strong>、<br>とってもよろこんでいるよ！💖';
  document.getElementById('perfectOverlay').classList.add('active');
  spawnKira(20); setTimeout(function(){spawnKira(16);},700);
}
function closePerfect(){
  document.getElementById('perfectOverlay').classList.remove('active');
  mood=0; animateBar(100,0);
  if(pendingLvup){ pendingLvup=false; setTimeout(doLevelUp,400); }
}

// ──────────────────────────────────────────
// レベルアップ
// ──────────────────────────────────────────
function doLevelUp(){
  if(level>=LEVELS.length) return;
  level++;
  var lvData=LEVELS[level-1];
  var got=pick(LEVEL_ITEMS);
  addItem(got);

  document.getElementById('lvupLv').textContent='Lv.'+level+' '+lvData.name;
  document.getElementById('lvupItemIcon').textContent=got.icon;
  document.getElementById('lvupItemName').textContent=got.name;
  spawnLvupStars();
  document.getElementById('lvupOverlay').classList.add('active');
  updateLevelUI();

  logs.unshift('🎉 Lv.'+level+' '+lvData.name+' にレベルアップ！'+got.icon+got.name+'ゲット！');
  if(logs.length>6) logs.pop();
  renderLogs();
}
function closeLvup(){
  document.getElementById('lvupOverlay').classList.remove('active');
  pickNewWish();
}
function updateLevelUI(){
  var d=LEVELS[Math.min(level,LEVELS.length)-1];
  document.getElementById('lvNum').textContent='Lv.'+level;
  document.getElementById('lvName').textContent=d.name;
}

// ──────────────────────────────────────────
// アイテム
// ──────────────────────────────────────────
function addItem(def){
  var k=def.name;
  if(items[k]){ items[k].count++; } else { items[k]={icon:def.icon,name:def.name,count:1}; }
  renderItems();
}
function renderItems(){
  var grid=document.getElementById('itemGrid');
  var keys=Object.keys(items);
  if(!keys.length){
    grid.innerHTML='<div class="item-empty">まだないよ 🌙<br>レベルアップやごほうびでゲット！</div>';
    return;
  }
  grid.innerHTML='';
  keys.forEach(function(k){
    var it=items[k];
    var chip=document.createElement('div');
    chip.className='item-chip';
    chip.innerHTML='<span class="chip-icon">'+it.icon+'</span>'
      +'<span class="chip-name">'+it.name+'</span>'
      +(it.count>1?'<span class="chip-cnt">×'+it.count+'</span>':'');
    grid.appendChild(chip);
  });
}

// ──────────────────────────────────────────
// ログ
// ──────────────────────────────────────────
function renderLogs(){
  var ul=document.getElementById('activityList');
  if(!logs.length){ ul.innerHTML='<li class="log-empty">まだきろくはないよ 🌙</li>'; return; }
  ul.innerHTML='';
  logs.forEach(function(log){
    var li=document.createElement('li'); li.textContent=log; ul.appendChild(li);
  });
}

// ──────────────────────────────────────────
// フロートメッセージ
// ──────────────────────────────────────────
function showFloatMsg(text){
  var el=document.getElementById('floatMsg');
  el.textContent=text; el.className='float-msg';
  void el.offsetWidth; el.className='float-msg show';
  setTimeout(function(){ el.className='float-msg'; },1900);
}

// ──────────────────────────────────────────
// ハートエフェクト
// ──────────────────────────────────────────
function spawnHearts(btn){
  var rect=btn.getBoundingClientRect();
  var cx=rect.left+rect.width/2, cy=rect.top+rect.height/2;
  var pool=['💖','💜','✨','🌟','♥','⭐','💗'];
  for(var i=0;i<5;i++){
    (function(i){ setTimeout(function(){
      var el=document.createElement('div'); el.className='heart-pop';
      el.textContent=pool[Math.floor(Math.random()*pool.length)];
      el.style.left=(cx+(Math.random()-.5)*50)+'px'; el.style.top=cy+'px';
      el.style.setProperty('--hr',(Math.random()*30-15)+'deg');
      document.body.appendChild(el); setTimeout(function(){ el.remove(); },1050);
    },i*60); })(i);
  }
}

// ──────────────────────────────────────────
// キラキラ
// ──────────────────────────────────────────
function spawnKira(count){
  var pool=['✨','⭐','🌟','💫','🌸','💖','💜','🎀','✦'];
  count=count||12;
  for(var i=0;i<count;i++){
    (function(i){ setTimeout(function(){
      var el=document.createElement('div'); el.className='kira';
      el.textContent=pool[Math.floor(Math.random()*pool.length)];
      el.style.left=(10+Math.random()*80)+'vw'; el.style.top=(10+Math.random()*80)+'vh';
      var angle=Math.random()*Math.PI*2, dist=50+Math.random()*100;
      el.style.setProperty('--kx',Math.cos(angle)*dist+'px');
      el.style.setProperty('--ky',Math.sin(angle)*dist+'px');
      el.style.setProperty('--kt',(.7+Math.random()*.7)+'s');
      el.style.setProperty('--ks',(.8+Math.random()*1.2)+'rem');
      el.style.setProperty('--kr',(Math.random()*720-360)+'deg');
      document.body.appendChild(el); setTimeout(function(){ el.remove(); },1500);
    },i*55); })(i);
  }
}

// ──────────────────────────────────────────
// レベルアップボックス星
// ──────────────────────────────────────────
function spawnLvupStars(){
  var box=document.getElementById('lvupStarsBg'); box.innerHTML='';
  var pool=['✦','★','✨','⭐'];
  for(var i=0;i<10;i++){
    var s=document.createElement('span');
    s.textContent=pool[Math.floor(Math.random()*pool.length)];
    s.style.cssText='position:absolute;font-size:'+(0.5+Math.random()*.7)+'rem;'
      +'left:'+(Math.random()*90)+'%;top:'+(Math.random()*90)+'%;'
      +'color:rgba(253,230,138,'+(0.3+Math.random()*.5)+');'
      +'animation:twinkle '+(1+Math.random()*2)+'s ease-in-out infinite alternate;'
      +'--d:'+(1+Math.random()*2)+'s;--a1:0.2;--a2:0.9;';
    box.appendChild(s);
  }
}

// ──────────────────────────────────────────
// ユーティリティ
// ──────────────────────────────────────────
function pick(arr){ return arr[Math.floor(Math.random()*arr.length)]; }
function pad(n){ return ('0'+n).slice(-2); }
function getPlushName(){ return document.getElementById('nameInput').value.trim()||'ぬいぐるみ'; }
// ──────────────────────────────────────────
// 保存機能（TAKOYAKI共通キット v1）
// レベル・アイテム・きろく・なまえ・しゃしんを自動保存。
// ページを閉じても「だいすきパートナー」が消えないように。
// ──────────────────────────────────────────
var STORAGE_KEY = 'nuigurumi-savedata-v1';

function saveState(){
  try{
    var img = document.getElementById('plushPhoto');
    localStorage.setItem(STORAGE_KEY, JSON.stringify({
      mood: mood,
      level: level,
      items: items,
      logs: logs.slice(0, 50), // 直近50件だけ保存（容量対策）
      name: document.getElementById('nameInput').value,
      photo: (img && img.style.display !== 'none') ? img.src : null
    }));
  }catch(e){
    console.warn('保存に失敗しました（写真が大きすぎる場合は写真なしで保存を試みます）', e);
    try{
      localStorage.setItem(STORAGE_KEY, JSON.stringify({
        mood: mood, level: level, items: items,
        logs: logs.slice(0, 50),
        name: document.getElementById('nameInput').value,
        photo: null
      }));
    }catch(e2){ /* それでもダメなら諦める（アプリは動き続ける） */ }
  }
}

function restoreState(){
  var saved = null;
  try{
    var raw = localStorage.getItem(STORAGE_KEY);
    if(raw) saved = JSON.parse(raw);
  }catch(e){
    console.warn('保存データが読めませんでした。最初から始めます。', e);
  }
  if(!saved || typeof saved !== 'object') return;

  mood  = typeof saved.mood  === 'number' ? saved.mood  : 0;
  level = typeof saved.level === 'number' ? saved.level : 1;
  items = saved.items && typeof saved.items === 'object' ? saved.items : {};
  logs  = Array.isArray(saved.logs) ? saved.logs : [];

  if(saved.name) document.getElementById('nameInput').value = saved.name;
  if(saved.photo){
    var img = document.getElementById('plushPhoto');
    img.src = saved.photo;
    img.style.display = 'block';
    var ph = document.getElementById('placeholder');
    if(ph) ph.style.display = 'none';
  }

  // 画面に反映
  updateLevelUI();
  renderItems();
  renderLogs();
  animateBar(0, mood);
}

// 復元 → 以後は2秒ごと＆画面を離れるときに自動保存
restoreState();
setInterval(saveState, 2000);
window.addEventListener('beforeunload', saveState);
document.getElementById('nameInput').addEventListener('change', saveState);

// ──────────────────────────────────────────
// はじめからボタン（リセット機能）
// きろくカードの下に小さなボタンを自動で追加する。
// 2段階の確認つき（子どもがうっかり押しても消えないように）。
// ──────────────────────────────────────────
(function addResetButton(){
  var logCard = document.querySelector('.log-card');
  if(!logCard) return;
  var btn = document.createElement('button');
  btn.id = 'resetBtn';
  btn.textContent = '🌙 はじめから やりなおす';
  btn.style.cssText = 'display:block;margin:14px auto 0;padding:8px 18px;font-size:12px;font-family:inherit;color:rgba(255,255,255,.55);background:rgba(255,255,255,.08);border:1px dashed rgba(255,255,255,.25);border-radius:20px;cursor:pointer;';
  btn.addEventListener('click', function(){
    var name = getPlushName();
    if(!confirm('ほんとうに さいしょから はじめる？\n' + name + 'との おもいでが きえちゃうよ')) return;
    if(!confirm('レベルも アイテムも きろくも ぜんぶ きえます。\nほんとうの ほんとうに いい？')) return;
    try{ localStorage.removeItem(STORAGE_KEY); }catch(e){}
    location.reload();
  });
  logCard.appendChild(btn);
})();