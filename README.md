<!DOCTYPE html><html lang="vi"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover"><title>Ashen Vigil</title>
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@500;700&family=Spectral:wght@400;600&display=swap" rel="stylesheet">
<style>
:root{--bg:#0d0a14;--pn:#171224;--bone:#d8cdb8;--vi:#9a6bff;--em:#d08a3a;--bl:#8a2434;--ln:#3a2f52;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
html{scroll-padding-top:env(safe-area-inset-top,0px)}html,body{height:100%;margin:0;background:var(--bg);color:var(--bone);font:16px/1.4 Spectral,Georgia,serif;overflow:hidden}
*{box-sizing:border-box}h1,h2,h3,button,.hd{font-family:Cinzel,Georgia,serif}
canvas#c{position:fixed;inset:0;width:100%;height:100%}
button{background:var(--pn);color:var(--bone);border:1px solid var(--ln);padding:8px 14px;cursor:pointer;font-size:14px}button:hover,button:focus-visible{border-color:var(--vi);outline:none}
button.p{background:var(--vi);color:#100a1c;border-color:var(--vi)}button:disabled{opacity:.4}
#lobby{position:fixed;inset:0;display:flex;background:radial-gradient(ellipse at 70% 40%,#2a1a4a 0,#0d0a14 70%);z-index:5}
#lm{width:260px;padding:20px;display:flex;flex-direction:column;gap:6px;overflow:auto;border-right:1px solid var(--ln)}
#lm h1{margin:0 0 8px;font-size:26px;letter-spacing:.06em}#lm button{text-align:left;font-family:Cinzel,serif}
#lh{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center}#lh canvas{height:min(60vh,420px);filter:drop-shadow(0 0 24px #7a4cff88)}
#panel{position:fixed;inset:0;background:#000a;display:none;align-items:center;justify-content:center;z-index:9}
#pb{background:var(--pn);border:1px solid var(--ln);width:min(720px,94vw);max-height:86vh;overflow:auto;padding:18px}
#pb h2{margin:0 0 10px}.row{display:flex;gap:8px;align-items:center;justify-content:space-between;border-top:1px solid var(--ln);padding:8px 0;flex-wrap:wrap}
.tag{color:var(--em)}.myth{color:#ff9c4a}.dim{opacity:.65;font-size:14px}
input{background:#0d0a14;color:var(--bone);border:1px solid var(--ln);padding:8px;min-width:170px}input:focus{border-color:var(--vi);outline:none}.online{color:#72e6a0}.offline{color:#ff8a8a}
#hud{position:fixed;inset:0;pointer-events:none;display:none;z-index:2}#hud *{pointer-events:auto}
#party{position:absolute;left:10px;top:10px;display:flex;flex-direction:column;gap:6px}
.pc{width:210px;background:#0d0a14cc;border:1px solid var(--ln);padding:4px 6px;font-size:13px}.pc.on{border-color:var(--vi)}
.bar{height:7px;background:#000;margin:2px 0}.bar i{display:block;height:100%;background:var(--bl)}
#sk{position:absolute;left:50%;bottom:14px;transform:translateX(-50%);display:flex;gap:6px}
.sb{width:62px;height:62px;border:1px solid var(--ln);background:#0d0a14dd;text-align:center;font-size:11px;position:relative;padding-top:6px}
.sb b{display:block;font:700 18px Cinzel,serif}.sb u{position:absolute;left:0;bottom:0;width:100%;background:#000c;text-decoration:none;text-align:center;font-size:13px}
#minimapWrap{position:absolute;right:10px;top:10px;width:190px;background:#0d0a14dd;border:1px solid var(--ln);padding:5px;text-align:center}#minimap{display:block;width:178px;height:178px;border-radius:50%;background:#090711;border:1px solid #6d5a8d}#miniTitle{font:700 11px Cinzel,serif;letter-spacing:.08em;margin:1px 0 4px;color:#d8cdb8}#tr{position:absolute;right:10px;top:215px;text-align:right;background:#0d0a14cc;padding:8px;max-width:300px;font-size:13px;border:1px solid var(--ln)}#questArrow{display:inline-block;font-size:20px;color:#ffd56a;transform-origin:50% 55%;margin-left:5px}
#msg{position:absolute;left:50%;top:14%;transform:translateX(-50%);font:700 20px Cinzel,serif;text-shadow:0 0 8px #000;text-align:center}
#xh{position:absolute;left:50%;top:50%;width:12px;height:12px;margin:-6px;border:1px solid #fff9;border-radius:50%;display:none}
.dn{position:fixed;font:700 16px Cinzel,serif;pointer-events:none;text-shadow:0 0 4px #000;animation:up .8s forwards;z-index:3}
@keyframes up{to{transform:translateY(-40px);opacity:0}}
@media(max-width:640px){#lobby{flex-direction:column}#lm{width:auto;flex-direction:row;flex-wrap:wrap;border:0}#lh{display:none}#minimapWrap{width:140px;padding:4px}#minimap{width:130px;height:130px}#tr{top:160px;max-width:230px;font-size:11px}.pc{width:175px}#sk{max-width:96vw;overflow-x:auto}}
</style></head><body>
<canvas id="c"></canvas><div id="xh"></div>
<div id="hud"><div id="party"></div><div id="minimapWrap"><div id="miniTitle">BẢN ĐỒ NHỎ</div><canvas id="minimap" width="180" height="180"></canvas></div><div id="tr"></div><div id="msg"></div><div id="sk"></div></div>
<div id="lobby"><div id="lm"></div><div id="lh"><div id="lc"></div><h2 class="hd" id="ln"></h2><div class="dim" id="ls"></div></div></div>
<div id="panel"><div id="pb"></div></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.5/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.5/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.5/firebase-database-compat.js"></script>
<script>
const $=id=>document.getElementById(id),rn=(a,b)=>b===undefined?Math.random()*a:a+Math.random()*(b-a),D=Math.hypot;

/* ---------- GITHUB PAGES MULTIPLAYER (Firebase Realtime Database) ----------
GitHub Pages is static hosting, so real matchmaking needs an external realtime backend.
1) Create a Firebase project.
2) Enable Authentication -> Anonymous.
3) Create Realtime Database.
4) Paste the Firebase web config below.
This config is public client configuration; protect data with Firebase rules.
-------------------------------------------------------------------------- */
const FIREBASE_CONFIG = {
  apiKey: "AIzaSyC2TDD2TmTtJPU77lNUQxIRMWI2mBQzz00",
  authDomain: "gmaesieuhay.firebaseapp.com",
  databaseURL: "https://gmaesieuhay-default-rtdb.asia-southeast1.firebasedatabase.app",
  projectId: "gmaesieuhay",
  storageBucket: "gmaesieuhay.firebasestorage.app",
  messagingSenderId: "302003485152",
  appId: "1:302003485152:web:d9c75fd733d11d9c065385",
  measurementId: "G-K5BXDLX2E5"
};
const FB_CONFIGURED=!Object.values(FIREBASE_CONFIG).some(v=>String(v).includes('PASTE_'));
const NET={ready:false,db:null,uid:null,status:'Not configured',search:null,incoming:[],friends:{},active:false,room:null,remoteId:null,remoteObj:null,roomRef:null,roomCb:null,sendT:0,dead:false,respawnT:0,outRef:null};
function safeKey(s){return String(s||'').replace(/[.#$\[\]\/]/g,'_')}
async function netInit(){
 if(!FB_CONFIGURED){NET.status='Firebase config required';return}
 try{
  if(!firebase.apps.length)firebase.initializeApp(FIREBASE_CONFIG);
  const cred=await firebase.auth().signInAnonymously();NET.uid=cred.user.uid;NET.db=firebase.database();NET.ready=true;NET.status='Online';
  const pr=NET.db.ref('players/'+safeKey(S.id));
  await pr.update({id:S.id,uid:NET.uid,name:S.name,hero:S.av,online:true,lastSeen:firebase.database.ServerValue.TIMESTAMP});
  pr.onDisconnect().update({online:false,lastSeen:firebase.database.ServerValue.TIMESTAMP});
  NET.db.ref('challenges/'+safeKey(S.id)).on('value',snap=>{NET.incoming=[];snap.forEach(ch=>{const v=ch.val();if(v&&v.status==='pending')NET.incoming.push({...v,key:ch.key})});if($('panel').style.display==='flex'&&$('pb').dataset.page==='friends')pFr()});
  NET.db.ref('friends/'+safeKey(S.id)).on('value',snap=>{NET.friends=snap.val()||{};if($('panel').style.display==='flex'&&$('pb').dataset.page==='friends')pFr()});
 }catch(e){NET.ready=false;NET.status='Connection error: '+e.message}
}
async function netRefreshProfile(){if(!NET.ready)return;await NET.db.ref('players/'+safeKey(S.id)).update({name:S.name,hero:S.av,online:true,lastSeen:firebase.database.ServerValue.TIMESTAMP})}
async function netSearch(){
 if(!NET.ready)return msg2('Configure Firebase first');const id=String(($('fid')&&$('fid').value)||'').trim();if(!id||id===S.id){NET.search=null;pFr();return}
 const snap=await NET.db.ref('players/'+safeKey(id)).once('value');NET.search=snap.exists()?snap.val():{missing:true,id};pFr()
}
async function netAddFriend(id){if(!NET.ready)return;await NET.db.ref('friendRequests/'+safeKey(id)+'/'+safeKey(S.id)).set({from:S.id,name:S.name,ts:firebase.database.ServerValue.TIMESTAMP});msg2('Friend request sent')}
async function netLoadRequests(){if(!NET.ready)return[];const snap=await NET.db.ref('friendRequests/'+safeKey(S.id)).once('value'),a=[];snap.forEach(x=>a.push({...x.val(),key:x.key}));return a}
async function netAcceptFriend(id){if(!NET.ready)return;const a={};a['friends/'+safeKey(S.id)+'/'+safeKey(id)]=true;a['friends/'+safeKey(id)+'/'+safeKey(S.id)]=true;a['friendRequests/'+safeKey(S.id)+'/'+safeKey(id)]=null;await NET.db.ref().update(a);pFr()}
async function netChallenge(id){
 if(!NET.ready)return msg2('Configure Firebase first');const target=await NET.db.ref('players/'+safeKey(id)).once('value');if(!target.exists()||!target.val().online)return msg2('Player is offline');
 const room=String(100000+Math.random()*900000|0),ref=NET.db.ref('challenges/'+safeKey(id)).push();
 await ref.set({fromId:S.id,fromName:S.name,fromHero:S.av,room,status:'pending',ts:firebase.database.ServerValue.TIMESTAMP});
 NET.outRef=ref;ref.on('value',s=>{const v=s.val();if(v&&v.status==='accepted'&&v.room){ref.off();joinBattleRoom(v.room)}});msg2('Duel invitation sent')
}
async function netAcceptChallenge(key){
 if(!NET.ready)return;const ref=NET.db.ref('challenges/'+safeKey(S.id)+'/'+key),s=await ref.once('value');if(!s.exists())return;const ch=s.val(),room=ch.room||String(100000+Math.random()*900000|0);
 await NET.db.ref('rooms/'+room).set({mode:'1v1',host:ch.fromId,guest:S.id,status:'playing',createdAt:firebase.database.ServerValue.TIMESTAMP});
 await ref.update({status:'accepted',room});joinBattleRoom(room)
}
function netArenaClear(){
 if(NPC&&NPC.g)W.remove(NPC.g);NPC=null;for(const q of SH)if(q.m)W.remove(q.m);SH=[];for(const e of E)if(e.g)W.remove(e.g);E=[];G.kills=0;G.total=0;
}
async function joinBattleRoom(room){
 if(!NET.ready)return;closeP();$('lobby').style.display='none';$('hud').style.display='block';play=true;build(2);netArenaClear();
 NET.active=true;NET.room=String(room);NET.dead=false;NET.respawnT=0;const rr=NET.db.ref('rooms/'+NET.room);NET.roomRef=rr;
 const rs=await rr.once('value');if(!rs.exists()){NET.active=false;toLobby();return msg2('Room no longer exists')}
 const rv=rs.val(),isHost=String(rv.host)===String(S.id);P.x=isHost?-14:14;P.z=0;P.y=gy(P.x,P.z,99);P.dest=null;P.tgt=null;
 const hero=S.av;setHero(hero);const hr=heroSt(hero);hr.hp=hr.st.hp;
 const me=rr.child('players/'+safeKey(S.id));await me.set({id:S.id,name:S.name,hero,uid:NET.uid,x:P.x,z:P.z,y:P.y,f:P.f,hp:hr.hp,maxHp:hr.st.hp,alive:true,ts:firebase.database.ServerValue.TIMESTAMP});me.onDisconnect().remove();
 NET.roomCb=rr.child('players').on('value',snap=>{
  let remote=null;snap.forEach(ch=>{const v=ch.val();if(String(v.id)!==String(S.id))remote=v});
  if(remote){NET.remoteId=String(remote.id);if(!NET.remoteObj||NET.remoteObj.hero!==remote.hero){if(NET.remoteObj&&NET.remoteObj.g)scene.remove(NET.remoteObj.g);const tex=TX[remote.hero]||TX.NYX,g=actor(tex,1,1);scene.add(g);NET.remoteObj={remote:true,id:remote.id,hero:remote.hero,name:remote.name||'Opponent',x:remote.x||0,z:remote.z||0,y:remote.y||0,hp:remote.hp||1,mx:remote.maxHp||1,ex:1,g,dead:false,st:0,sl:0}}
   const r=NET.remoteObj;r.x=remote.x||0;r.z=remote.z||0;r.y=remote.y||gy(r.x,r.z,99);r.hp=Math.max(0,remote.hp||0);r.mx=remote.maxHp||r.mx||1;r.dead=remote.alive===false||r.hp<=0;
  }
  const mine=snap.child(safeKey(S.id)).val();if(mine){const h=heroSt(P.h);h.hp=Math.max(0,Math.min(h.st.hp,mine.hp??h.hp));if((mine.alive===false||h.hp<=0)&&!NET.dead){NET.dead=true;NET.respawnT=3;msg('Defeated — respawning in 3s')}}
 });
 msg('PvP room '+NET.room+' — duel started')
}
async function netDealDamage(e,a,ty){
 if(!NET.active||!NET.roomRef||!e||!e.remote||e.dead)return;const path=NET.roomRef.child('players/'+safeKey(e.id)+'/hp');
 await path.transaction(v=>Math.max(0,(Number(v)||e.mx||1)-Math.max(1,Math.round(a))));
 const s=await NET.roomRef.child('players/'+safeKey(e.id)).once('value');const v=s.val();if(v&&Number(v.hp)<=0){await NET.roomRef.child('players/'+safeKey(e.id)).update({alive:false})}
}
function combatTargets(){const a=E.filter(e=>!e.dead);if(NET.active&&NET.remoteObj&&!NET.remoteObj.dead)a.push(NET.remoteObj);return a}
function netTick(dt){
 if(!NET.active||!NET.roomRef)return;NET.sendT-=dt;if(NET.sendT<=0){NET.sendT=.08;const h=heroSt(P.h);NET.roomRef.child('players/'+safeKey(S.id)).update({name:S.name,hero:P.h,x:P.x,z:P.z,y:P.y,f:P.f,hp:h.hp,maxHp:h.st.hp,alive:!NET.dead,ts:firebase.database.ServerValue.TIMESTAMP})}
 const r=NET.remoteObj;if(r&&r.g){r.g.visible=!r.dead;r.g.position.set(r.x,r.y,r.z);r.g.rotation.y=Math.atan2(cam.position.x-r.x,cam.position.z-r.z);if(r.g.userData.bar){r.g.userData.bar.scale.x=Math.max(.01,r.hp/r.mx);r.g.userData.bar.position.x=-(1-r.hp/r.mx)*.8}}
 if(NET.dead){NET.respawnT-=dt;if(NET.respawnT<=0){NET.dead=false;const mine=NET.roomRef.child('players/'+safeKey(S.id)),hostSide=P.x<0;P.x=hostSide?-14:14;P.z=0;P.y=gy(P.x,P.z,99);const h=heroSt(P.h);h.hp=h.st.hp;mine.update({x:P.x,z:P.z,y:P.y,hp:h.hp,maxHp:h.st.hp,alive:true});msg('Respawned')}}
}
function netLeaveBattle(){
 if(!NET.active)return;try{if(NET.roomRef&&NET.roomCb)NET.roomRef.child('players').off('value',NET.roomCb);if(NET.roomRef)NET.roomRef.child('players/'+safeKey(S.id)).remove()}catch(e){}if(NET.remoteObj&&NET.remoteObj.g)scene.remove(NET.remoteObj.g);NET.active=false;NET.room=null;NET.roomRef=null;NET.roomCb=null;NET.remoteObj=null;NET.remoteId=null;NET.dead=false
}
/* ---------- DATA ---------- */
const CH=[
{n:'Hollow Wood',lv:1,env:'forest',gr:[0x2b3a22,0x4a3a2a],fog:0x0c1218,trees:240,boss:'Stag Wraith',en:'Ash Wolf, Bone Ghoul',mul:1,rw:'5 tickets, gold'},
{n:'Drowned Mere',lv:5,env:'swamp',gr:[0x263a34,0x3a3a26],fog:0x0b1614,trees:110,water:1,boss:'Mere Leviathan',en:'Mire Leech, Bog Hag',mul:1.9,rw:'6 tickets, gold'},
{n:'Ruined Bastion',lv:10,env:'ruins',gr:[0x3a3a3f,0x4a4038],fog:0x100c14,trees:40,boss:'The Pale Warden',en:'Hollow Knight, Crypt Bat',mul:3.2,rw:'8 tickets, gold'},
{n:'Crypt of Ash (Dungeon)',lv:8,env:'ruins',gr:[0x2c2a30,0x38323a],fog:0x0a0810,trees:0,dg:1,boss:'Ashen Colossus',en:'Crypt Bat, Hollow Knight',mul:2.6,rw:'Guaranteed MYTHIC item'}];
const HERO={
NYX:{c:'#9a6bff',hp:900,ad:20,ap:95,bt:'m',rng:3,as:.5,rg:0,spd:12,cd:[5,7,8,28],sk:['Tia Nguyệt','Vồ Bóng','Lướt Hư Không','Nhật Thực'],pas:'Bước Hắc Ảnh: sau khi dùng kỹ năng, đòn đánh thường kế tiếp gây thêm 40% sát thương phép.'},
SELENA:{c:'#5fd0ff',hp:1000,ad:25,ap:85,bt:'m',rng:3,as:.55,rg:0,spd:12,cd:[5,8,14,40],sk:['Cầu Bí Thuật','Truy Kích','Quỹ Đạo Linh Hồn','Ảnh Giới'],pas:'Hưng Phấn Chiến Đấu: gây thêm 15% sát thương khi dưới 50% máu.'},
RAVENNA:{c:'#ff7a5a',hp:750,ad:70,ap:10,bt:'p',rng:15,as:.35,rg:1,spd:11,cd:[6,6,9,32],sk:['Tam Xạ','Lăn Chiến Thuật','Bom Thuốc Súng','Bão Đạn'],pas:'Mắt Săn: mỗi phát bắn thường thứ 4 gây gấp đôi sát thương vật lý.'},
VELORA:{c:'#e8a6ff',hp:930,ad:30,ap:88,bt:'m',rng:3.2,as:.48,rg:0,spd:13,cd:[5,7,10,30],sk:['Liềm Sao','Bước Khe Nứt','Ấn Tinh Vân','Vũ Điệu Thiên Thạch'],pas:'Dư Âm Tinh Giới: sau khi lướt, đòn đánh kế tiếp được cường hóa.'},
MYRIEL:{c:'#8edcff',hp:780,ad:22,ap:105,bt:'m',rng:14,as:.5,rg:1,spd:11.5,cd:[5,8,11,34],sk:['Mảnh Băng','Dịch Chuyển Sương','Vòng Giá Lạnh','Vương Miện Mùa Đông'],pas:'Hàn Tâm: kỹ năng trúng mục tiêu đang bị làm chậm gây thêm sát thương phép.'},
CAELYN:{c:'#a8d66d',hp:820,ad:76,ap:12,bt:'p',rng:16,as:.32,rg:1,spd:12.5,cd:[6,7,12,32],sk:['Tên Xuyên Lá','Bước Thợ Săn','Bẫy Gai','Mưa Quạ'],pas:'Tầm Săn: đòn đánh từ khoảng cách xa gây thêm sát thương vật lý.'}};
const TYPE={p:['Physical','⚔'],m:['Magic','✦'],d:['Defense','🛡']};
const NM={p:['Rusted Saber','Wolfsbane Blade','Ashen Fang'],m:['Cracked Grimoire','Moon Sigil','Witch Lantern'],d:['Chain Vest','Warden Aegis','Bone Plate']};
const MY={p:'Eclipse Reaver',m:'Voidheart Staff',d:'Crown of Ashes'};
const today=()=>new Date().toDateString();
/* ---------- SAVE ---------- */
let S={name:'Wanderer',id:String(100000+Math.random()*899999|0),gold:300,tk:12,pity:0,lv:1,xp:0,av:'NYX',own:['NYX','SELENA','RAVENNA'],party:['NYX','SELENA','RAVENNA'],hl:{},inv:[],eq:{},nid:1,maxCh:0,cleared:[],comp:{},daily:'',wk:0,kills:0,skins:{},trial:{},opt:{fov:80,shake:1,shk:1,rs:1,sh:1,bob:1},
mail:[{t:'Developer test gift',f:'Dev',m:'Tickets and gold for testing.',a:{tk:10,gold:500}},{t:'Nyx Trial Card',f:'Dev',m:'Trial for Nyx.',a:{trial:'NYX'}},{t:'Selena Trial Card',f:'Dev',m:'Trial for Selena.',a:{trial:'SELENA'}},{t:'Ravenna Trial Card',f:'Dev',m:'Trial for Ravenna.',a:{trial:'RAVENNA'}},{t:'Kaela EPIC Skin Trial Card — 7 Days',f:'Dev',m:'EPIC skin trial.',a:{skin:'KAELA'}},{t:'Aurelia EPIC Skin Trial Card — 7 Days',f:'Dev',m:'EPIC skin trial.',a:{skin:'AURELIA'}}]};
try{Object.assign(S,JSON.parse(localStorage.getItem('av1')||'{}'))}catch(e){}
const save=()=>{try{localStorage.setItem('av1',JSON.stringify(S))}catch(e){}};
const item=id=>S.inv.find(i=>i.id==id);
function mk(t,m){const n=m?MY[t]+' (Mythic)':NM[t][rn(3)|0];return{id:S.nid++,t,m:!!m,n,v:Math.round((m?45:10+rn(12))*(1+.3*S.maxCh))}}
function stat(n){const b=HERO[n],l=S.hl[n]||1,k=1+.12*(l-1),e={ad:0,ap:0,hp:0,as:0,cdr:0,ls:0,arm:0};
for(const t of'pmd'){const it=item(S.eq[n]&&S.eq[n][t]);if(!it)continue;if(t=='p'){e.ad+=it.v;e.as+=it.v/300}if(t=='m'){e.ap+=it.v;e.cdr+=it.v/400}if(t=='d'){e.hp+=it.v*8;e.arm+=it.v/2}if(it.m)e.ls+=.08}
return{ad:b.ad*k+e.ad,ap:b.ap*k+e.ap,hp:b.hp*k+e.hp,as:e.as,cdr:Math.min(.4,e.cdr),ls:e.ls,arm:e.arm,base:{ad:b.ad,ap:b.ap,hp:b.hp},up:k-1,e}}
/* ---------- THREE ---------- */
const cv=$('c'),R=new THREE.WebGLRenderer({canvas:cv,antialias:true});R.shadowMap.enabled=true;R.shadowMap.type=THREE.PCFSoftShadowMap;
const scene=new THREE.Scene(),cam=new THREE.PerspectiveCamera(80,1,.1,300);
function resize(){R.setPixelRatio(Math.min(devicePixelRatio,1.5)*S.opt.rs);R.setSize(innerWidth,innerHeight,false);cam.aspect=innerWidth/innerHeight;cam.fov=S.opt.fov;cam.updateProjectionMatrix();R.shadowMap.enabled=!!S.opt.sh}
addEventListener('resize',resize);
const moon=new THREE.DirectionalLight(0xa8b8ff,.95);moon.castShadow=true;moon.shadow.mapSize.set(1024,1024);const sc=moon.shadow.camera;sc.left=sc.bottom=-40;sc.right=sc.top=40;sc.far=200;
scene.add(moon,moon.target,new THREE.HemisphereLight(0x39385a,0x150e12,.7));
const torch=new THREE.PointLight(0xff8a3a,1.3,24);scene.add(torch);
const CT=(()=>{const c=document.createElement('canvas');c.width=c.height=64;const x=c.getContext('2d'),g=x.createRadialGradient(32,32,2,32,32,30);g.addColorStop(0,'rgba(0,0,0,.55)');g.addColorStop(1,'rgba(0,0,0,0)');x.fillStyle=g;x.fillRect(0,0,64,64);return new THREE.CanvasTexture(c)})();
/* ---- 2.5D art (placeholder; swap HERO[n].glb / ART slots for real GLB models later) ---- */
function art(kind,col){const c=document.createElement('canvas');c.width=128;c.height=256;const x=c.getContext('2d');
if(kind=='e'||kind=='b'){x.fillStyle=col;x.beginPath();x.ellipse(64,150,46,80,0,0,7);x.fill();for(let i=0;i<7;i++){x.beginPath();x.moveTo(20+i*14,90);x.lineTo(27+i*14,40+(i%2)*20);x.lineTo(34+i*14,90);x.fill()}x.fillStyle='#ffdf6a';x.shadowColor='#fa0';x.shadowBlur=12;x.beginPath();x.arc(48,120,7,0,7);x.arc(80,120,7,0,7);x.fill()}
else if(kind=='n'){x.fillStyle='#4a3a2a';x.beginPath();x.moveTo(42,90);x.lineTo(20,240);x.lineTo(108,240);x.lineTo(86,90);x.fill();x.fillStyle='#e8d2c0';x.beginPath();x.arc(64,62,18,0,7);x.fill();x.fillStyle='#ffd84a';x.font='bold 40px Cinzel';x.fillText('!',54,30)}
else{const g=x.createLinearGradient(0,80,0,240);g.addColorStop(0,col);g.addColorStop(1,'#120a1c');x.fillStyle=g;x.beginPath();x.moveTo(44,88);x.lineTo(16,242);x.lineTo(112,242);x.lineTo(84,88);x.fill();
x.fillStyle=col;x.beginPath();x.ellipse(64,66,26,30,0,0,7);x.fill();x.fillStyle='#e8d2c0';x.beginPath();x.arc(64,66,17,0,7);x.fill();x.fillStyle=col;x.beginPath();x.ellipse(64,52,20,10,0,3.14,0);x.fill();
x.fillRect(38,60,8,80);x.fillRect(82,60,8,80);x.fillStyle='#fff';x.shadowColor=col;x.shadowBlur=10;x.fillRect(55,68,4,4);x.fillRect(70,68,4,4);
x.strokeStyle=col;x.lineWidth=5;x.beginPath();if(kind=='NYX'){x.arc(100,130,22,1.2,5)}else if(kind=='SELENA'){x.arc(100,130,14,0,7)}else{x.moveTo(84,140);x.lineTo(124,130)}x.stroke()}
return new THREE.CanvasTexture(c)}
function actor(tex,s,bar){const g=new THREE.Group(),sp=new THREE.Mesh(new THREE.PlaneGeometry(2.2*s,4.4*s),new THREE.MeshBasicMaterial({map:tex,transparent:true,alphaTest:.3,side:2}));sp.position.y=2.2*s;
const bl=new THREE.Mesh(new THREE.PlaneGeometry(2.4*s,2.4*s),new THREE.MeshBasicMaterial({map:CT,transparent:true,depthWrite:false}));bl.rotation.x=-Math.PI/2;bl.position.y=.06;g.add(bl,sp);
if(bar){const b=new THREE.Mesh(new THREE.PlaneGeometry(1.6*s,.16),new THREE.MeshBasicMaterial({color:0xc03040}));b.position.y=4.7*s;g.add(b);g.userData.bar=b}g.userData.sp=sp;return g}
const TX={};for(const k in HERO)TX[k]=art(k,HERO[k].c);
/* ---------- WORLD ---------- */
let W,TER,COL=[],E=[],PR=[],Cl=[],TM=[],FX=[],SH=[],NPC=null,HF=()=>0,ci=0,altar={x:0,z:0};
const hf=(x,z)=>Math.sin(x*.07)*2.2+Math.cos(z*.09)*1.8+Math.sin((x+z)*.19)*.6+Math.max(0,D(x,z)-70)*.35;
const gh=(x,z)=>HF(x,z);
function gy(x,z,y){let g=HF(x,z);for(const c of COL)if(c.t<50&&y>=c.t-.4&&D(x-c.x,z-c.z)<c.r*.85)g=Math.max(g,c.t);return g}
function solid(x,z,y){for(const c of COL)if(D(x-c.x,z-c.z)<c.r&&y<c.t-.35)return c;return null}
function step(o,dx,dz){if(!solid(o.x+dx,o.z+dz,o.y)){o.x+=dx;o.z+=dz}else if(!solid(o.x+dx,o.z,o.y))o.x+=dx;else if(!solid(o.x,o.z+dz,o.y))o.z+=dz;const d=D(o.x,o.z);if(d>95){o.x*=95/d;o.z*=95/d}}
const dm=new THREE.Object3D();
function inst(geo,mat,n,fn,shadow){const m=new THREE.InstancedMesh(geo,mat,n);for(let i=0;i<n;i++){fn(dm,i);dm.updateMatrix();m.setMatrixAt(i,dm.matrix)}m.castShadow=!!shadow;W.add(m);return m}
function free(r){for(let k=0;k<30;k++){const a=rn(6.28),d=rn(r[0],r[1]),x=Math.cos(a)*d,z=Math.sin(a)*d;if(!solid(x,z,0))return{x,z}}return{x:r[0],z:0}}
function build(i){
if(W)scene.remove(W);W=new THREE.Group();scene.add(W);COL=[];E=[];PR=[];Cl=[];TM=[];FX=[];SH=[];ci=i;const c=CH[i];
scene.background=new THREE.Color(c.fog);scene.fog=new THREE.FogExp2(c.fog,.02);HF=(x,z)=>hf(x,z)-(c.water?1.6:0);
const g=new THREE.PlaneGeometry(200,200,110,110);g.rotateX(-Math.PI/2);const p=g.attributes.position,col=new Float32Array(p.count*3),cs=c.gr.map(h=>new THREE.Color(h)),K=[0x4b4a50,0x2c3f2a,0x2a1f18,0x5a3a1c,0x55524d].map(h=>new THREE.Color(h));
for(let k=0;k<p.count;k++){const x=p.getX(k),z=p.getZ(k),h=HF(x,z);p.setY(k,h);const n=Math.sin(x*.45)*Math.sin(z*.4)+Math.sin(x*1.3+z)*.4,sl=Math.abs(HF(x+1,z)-h)+Math.abs(HF(x,z+1)-h);let q=cs[n>0?0:1].clone();
if(sl>.55)q.lerp(K[0],Math.min(1,(sl-.55)*2));else if(n<-.6)q.lerp(K[2],.7);else if(n>.9)q.lerp(K[1],.6);else if(Math.sin(x*.8)*Math.cos(z*.9)>.8)q.lerp(K[3],.6);else if(n>.4&&n<.5)q.lerp(K[4],.5);col.set([q.r,q.g,q.b],k*3)}
g.setAttribute('color',new THREE.BufferAttribute(col,3));g.computeVertexNormals();TER=new THREE.Mesh(g,new THREE.MeshLambertMaterial({vertexColors:true}));TER.receiveShadow=true;W.add(TER);
if(c.water){const w=new THREE.Mesh(new THREE.PlaneGeometry(200,200),new THREE.MeshLambertMaterial({color:0x1b3a4a,transparent:true,opacity:.75}));w.rotation.x=-Math.PI/2;w.position.y=-.3;W.add(w)}
const tp=[];for(let k=0;k<c.trees;k++){const f=free([9,92]);tp.push(f);COL.push({x:f.x,z:f.z,r:.7,t:999})}
inst(new THREE.ConeGeometry(1.7,5.5,7),new THREE.MeshLambertMaterial({color:c.env=='swamp'?0x2a3320:0x16261a}),c.trees,(d,k)=>{const s=rn(.8,1.5),q=tp[k];d.position.set(q.x,HF(q.x,q.z)+3.5*s,q.z);d.scale.set(s,s,s);d.rotation.y=rn(6)},1);
inst(new THREE.CylinderGeometry(.25,.4,2.5,6),new THREE.MeshLambertMaterial({color:0x2a1c12}),c.trees,(d,k)=>{const q=tp[k];d.position.set(q.x,HF(q.x,q.z)+1,q.z);d.scale.set(1,1,1);d.rotation.y=0});
const rp=[];for(let k=0;k<70;k++){const f=free([6,92]),s=rn(.7,2.6),h=HF(f.x,f.z);rp.push({...f,s,h});COL.push({x:f.x,z:f.z,r:s*.95,t:s<1.5?h+s*.85:999})}
inst(new THREE.DodecahedronGeometry(1,0),new THREE.MeshLambertMaterial({color:0x55545c,flatShading:true}),70,(d,k)=>{const r=rp[k];d.position.set(r.x,r.h+r.s*.5,r.z);d.scale.set(r.s,r.s*.9,r.s);d.rotation.set(rn(3),rn(6),0)},1);
const nR=c.env=='ruins'?26:6,ru=new THREE.MeshLambertMaterial({color:0x6a665f});
for(let k=0;k<nR;k++){const f=free([12,85]),h=HF(f.x,f.z);if(k%2){const m=new THREE.Mesh(new THREE.CylinderGeometry(.8,.9,5.5,8),ru);m.position.set(f.x,h+2.7,f.z);m.castShadow=true;W.add(m);COL.push({x:f.x,z:f.z,r:.9,t:999})}else{const m=new THREE.Mesh(new THREE.BoxGeometry(6,3,.8),ru);m.position.set(f.x,h+1.4,f.z);m.castShadow=true;W.add(m);for(let j=-2;j<=2;j+=2)COL.push({x:f.x+j,z:f.z,r:1.15,t:999})}}
inst(new THREE.ConeGeometry(.09,.7,3),new THREE.MeshLambertMaterial({color:c.env=='swamp'?0x3a4a2a:0x2f4a26}),1400,(d,k)=>{const x=rn(-95,95),z=rn(-95,95);d.position.set(x,HF(x,z)+.3,z);d.scale.set(1,rn(.6,1.6),1);d.rotation.y=rn(6)});
inst(new THREE.IcosahedronGeometry(.13,0),new THREE.MeshLambertMaterial({color:0x66625c}),350,(d,k)=>{const x=rn(-95,95),z=rn(-95,95);d.position.set(x,HF(x,z)+.05,z);d.scale.set(1,.6,1);d.rotation.y=rn(6)});
for(let k=0;k<7;k++){const x=rn(-60,60),z=rn(-60,60),m=new THREE.Mesh(new THREE.CircleGeometry(rn(1.2,2.6),14),new THREE.MeshBasicMaterial({color:0x1a2a3a,transparent:true,opacity:.6}));m.rotation.x=-Math.PI/2;m.position.set(x,HF(x,z)+.04,z);W.add(m)}
const ah=HF(0,0),al=new THREE.Mesh(new THREE.CylinderGeometry(.9,1.2,1.2,8),ru),fl=new THREE.Mesh(new THREE.ConeGeometry(.4,1.2,6),new THREE.MeshBasicMaterial({color:0xffa04a}));al.position.set(0,ah+.6,0);fl.position.set(0,ah+1.8,0);al.castShadow=true;W.add(al,fl);COL.push({x:0,z:0,r:1.1,t:999});torch.position.set(0,ah+2.4,0);
NPC=null;if(!c.dg){const nx=12,nz=9,n=actor(art('n'),1);n.position.set(nx,HF(nx,nz),nz);W.add(n);NPC={x:nx,z:nz,g:n,st:0};SH=[];for(let k=0;k<3;k++){const f=free([20,60]),m=new THREE.Mesh(new THREE.OctahedronGeometry(.5),new THREE.MeshBasicMaterial({color:0x9ad0ff}));m.position.set(f.x,HF(f.x,f.z)+1,f.z);W.add(m);SH.push({x:f.x,z:f.z,m,got:0,vis:0})}}
const tt=[art('e','#5a2a3a'),art('e','#2a4a3a')],ne=c.dg?18:28;
for(let k=0;k<ne;k++){const f=free([16,88]);mkE(f.x,f.z,tt[k%2],c.mul,0)}
mkE(0,c.dg?-30:-78,art('b','#3a1030'),c.mul,1);
P.x=P.z=3;P.y=gy(3,3,99);P.vy=0;P.dest=null;P.tgt=null;P.inv=0;P.rc=0;P.f=0;P.stun=0;P.dg=0;P.imm=0;
S.hl.__q=0;Q={s:0,d:0};G.flash=0;G.sup=0;G.kills=0;G.total=E.length;msg(c.n);
}
function mkE(x,z,tex,mul,boss){const dg=CH[ci].dg?2.5:1,s=boss?1.9:1,o={x,z,y:gy(x,z,99),hp:(boss?4200*dg/(CH[ci].dg?1:1):130)*mul,dm:(boss?38:13)*mul,sp:boss?6:5+rn(2),st:0,sl:0,ac:rn(1),boss,rg:boss?3.4:2.2,rs:boss?.3:.15,g:actor(tex,s,1),ex:s};o.mx=o.hp;o.g.position.set(x,o.y,z);W.add(o.g);E.push(o)}
/* ---------- STATE ---------- */
const P={x:0,z:0,y:0,vy:0,h:'NYX',dest:null,tgt:null,inv:0,rc:0,f:0,at:0,emp:0,bon:0,shot:0,dg:0,imm:0,stun:0,ro:0},H={},G={flash:0,sup:0,kills:0,total:0,sel:'STUN'};let Q={s:0,d:0},play=false,cm=0,yaw=0,pitch=-.2,zoom=22,shk=0,ORB=[],orbT=0,rapid=0,fd=0;
const M={x:0,z:0};
function heroSt(n){if(!H[n]){const s=stat(n);H[n]={hp:s.hp,cd:[0,0,0,0],st:s}}return H[n]}
function refreshH(){for(const n of S.party){const s=stat(n),h=heroSt(n),r=h.hp/h.st.hp;h.st=s;h.hp=s.hp*r}}
let hl=null;const hit=(o,r)=>o.hp>0;
function msg(t){const m=$('msg');m.textContent=t;clearTimeout(m.t);m.t=setTimeout(()=>m.textContent='',2600)}
const cvs=new THREE.Raycaster(),mv=new THREE.Vector2();
function pick(e){mv.set(e.clientX/innerWidth*2-1,-(e.clientY/innerHeight)*2+1);cvs.setFromCamera(mv,cam);const r=cvs.intersectObject(TER)[0];return r?r.point:null}
/* ---------- ACTOR SETUP ---------- */
let PG=null;const SP=new THREE.Group();scene.add(SP);
function setHero(n){P.h=n;if(PG)scene.remove(PG);PG=actor(TX[n],1);scene.add(PG);const h=heroSt(n);if(h.hp<=0){return false}return true}
function ghost(x,z,y,n){const m=new THREE.Mesh(new THREE.PlaneGeometry(2.2,4.4),new THREE.MeshBasicMaterial({map:TX[n||P.h],transparent:true,opacity:.5,alphaTest:.05,side:2,color:HERO[n||P.h].c}));m.position.set(x,y+2.2,z);m.rotation.y=PG.rotation.y;scene.add(m);FX.push({m,t:.35,g:1})}
function ring(x,z,r,col,t=.45){const y=gy(x,z,99)+.2,m=new THREE.Mesh(new THREE.RingGeometry(.85,1,28),new THREE.MeshBasicMaterial({color:col,transparent:true,opacity:.8,side:2}));m.rotation.x=-Math.PI/2;m.position.set(x,y,z);scene.add(m);FX.push({m,t,T:t,r})}
function proj(o){const m=new THREE.Mesh(new THREE.SphereGeometry(.3,8,6),new THREE.MeshBasicMaterial({color:o.col}));m.scale.set(1,1,o.sc||1);m.position.set(o.x,o.y||P.y+1.4,o.z);m.rotation.y=Math.atan2(o.dx,o.dz);scene.add(m);o.m=m;o.life=o.life||1.2;PR.push(o)}
function dn(x,y,z,t,c){const v=new THREE.Vector3(x,y,z).project(cam);if(v.z>1)return;const d=document.createElement('div');d.className='dn';d.textContent=t;d.style.cssText+=`left:${(v.x*.5+.5)*innerWidth}px;top:${(-v.y*.5+.5)*innerHeight}px;color:${c}`;document.body.appendChild(d);setTimeout(()=>d.remove(),800)}
/* ---------- COMBAT ---------- */
function dmg(e,a,ty){const hr=H[P.h],s=hr.st;if(e&&e.remote){dn(e.x,e.y+3,e.z,Math.round(a),ty=='m'?'#c9a6ff':'#ffd28a');netDealDamage(e,a,ty);shk=Math.max(shk,.05);return}if(P.h=='SELENA'&&hr.hp<s.hp*.5)a*=1.15;if(P.bon&&P.h=='NYX'){a*=1.4;P.bon=0}a*=1+(e.boss&&ty=='p'?-.1:0);const res=(ty=='m'?(e.boss?.15:0):(e.boss?.2:.1));a*=1-res;e.hp-=a;dn(e.x,e.y+3,e.z,Math.round(a),ty=='m'?'#c9a6ff':'#ffd28a');if(s.ls){hr.hp=Math.min(s.hp,hr.hp+a*s.ls)}
shk=Math.max(shk,.05);if(e.hp<=0&&!e.dead)kill(e)}
function kill(e){e.dead=1;W.remove(e.g);G.kills++;S.kills++;S.gold+=e.boss?300:8;S.xp+=e.boss?200:10;if(S.xp>=S.lv*100){S.xp-=S.lv*100;S.lv++;msg('Lên cấp! '+S.lv)}
if(e.boss)clearMap();S.comp[ci]=Math.max(S.comp[ci]||0,Math.min(99,Math.round(G.kills/G.total*100)))}
function clearMap(){const c=CH[ci];if(!S.cleared.includes(ci)){S.cleared.push(ci);if(ci==S.maxCh&&ci<2)S.maxCh++}S.comp[ci]=100;if(c.dg){const it=mk('pmd'[rn(3)|0],1);S.inv.push(it);msg('Boss slain! Mythic: '+it.n)}else{S.tk+=5+ci;S.gold+=300;msg('Boss slain! +'+(5+ci)+' tickets')}save()}
function hurt(a){const hr=H[P.h];if(P.dg>0||P.imm>0||P.inv>0&&0)return;P.rc=0;hr.hp-=a*100/(100+hr.st.arm);shk=Math.max(shk,.25);if(hr.hp<=0){hr.hp=0;const nx=S.party.find(n=>H[n]&&H[n].hp>0);if(nx)sw(nx);else{msg('Đã gục… trở về tế đàn');S.gold=Math.floor(S.gold*.9);P.x=3;P.z=3;for(const n of S.party)H[n].hp=H[n].st.hp*.5}}}
function near(x,z,r){return combatTargets().filter(e=>!e.dead&&D(e.x-x,e.z-z)<r+(e.ex||1)*.5)}
function nearest(x,z,r){let b=null,bd=r;for(const e of combatTargets()){if(e.dead)continue;const d=D(e.x-x,e.z-z);if(d<bd){bd=d;b=e}}return b}
function aim(){let dx,dz;if(cm==0){dx=M.x-P.x;dz=M.z-P.z}else{dx=-Math.sin(yaw);dz=-Math.cos(yaw)}const l=D(dx,dz)||1;return{dx:dx/l,dz:dz/l,d:cm==0?l:12}}
function face(dx,dz){P.f=Math.atan2(dx,dz)}
function attack(){const b=HERO[P.h],hr=H[P.h],s=hr.st;if(P.at>0||P.stun>0)return;P.at=(b.as/(1+s.as));const a=aim();let t=P.tgt&&!P.tgt.dead?P.tgt:null;if(cm>0||!t){t=null;let bd=b.rng+2;for(const e of combatTargets()){if(e.dead)continue;const dx=e.x-P.x,dz=e.z-P.z,d=D(dx,dz);if(d<bd&&(dx*a.dx+dz*a.dz)/d>(cm>0?.8:-2)){bd=d;t=e}}}
let dx=a.dx,dz=a.dz;if(t&&cm==0){dx=t.x-P.x;dz=t.z-P.z;const l=D(dx,dz)||1;dx/=l;dz/=l}face(dx,dz);
if(b.rg){P.shot++;let d=b.bt=='m'?s.ap:s.ad;if(P.h=='RAVENNA'&&P.shot%4==0)d*=2;if(P.h=='CAELYN'&&t&&D(t.x-P.x,t.z-P.z)>9)d*=1.2;if(P.emp){d*=1.6;P.emp=0}proj({x:P.x+dx,z:P.z+dz,dx,dz,sp:46,dmg:d,ty:b.bt,col:parseInt(b.c.slice(1),16),sc:3,life:.7});P.ro=.12;ring(P.x+dx*1.2,P.z+dz*1.2,.6,parseInt(b.c.slice(1),16),.12)}
else if(t&&D(t.x-P.x,t.z-P.z)<b.rng+t.ex){let d=(b.bt=='m'?s.ap:s.ad)*.9+20;if(P.emp){d*=1.8;P.emp=0}dmg(t,d,b.bt);ring(t.x,t.z,1.2,HERO[P.h].c,.2);
if(P.h=='SELENA'&&orbT>0){const o=ORB.find(o=>o.d<=0);if(o){o.d=.3;o.t=t;dmg(t,40+s.ap*.2,'m');hr.hp=Math.min(s.hp,hr.hp+30)}}}}
function skill(i){if(!play)return;const n=P.h,b=HERO[n],hr=H[n],s=hr.st;if(hr.cd[i]>0||P.stun>0)return;const a=aim();let ap=s.ap,ad=s.ad,c=HERO[n].c,cds=b.cd[i]*(1-s.cdr),ok=1;face(a.dx,a.dz);
const tg=nearest(cm==0?M.x:P.x+a.dx*8,cm==0?M.z:P.z+a.dz*8,14)||nearest(P.x,P.z,14);
if(n=='NYX'){P.bon=1;
if(i==0)proj({x:P.x,z:P.z,dx:a.dx,dz:a.dz,sp:34,dmg:110+ap*.7,ty:'m',col:0xb48cff,st:1.3,life:1,sc:2});
if(i==1){if(!tg){ok=0}else{ghost(P.x,P.z,P.y);P.x=tg.x-a.dx*1.5;P.z=tg.z-a.dz*1.5;dmg(tg,140+ap*.6,'m');ring(tg.x,tg.z,3,0xb48cff)}}
if(i==2)dash(a.dx,a.dz,10,e=>dmg(e,120+ap*.5,'m'));
if(i==3){ring(P.x,P.z,8,0xb48cff,.6);for(const e of near(P.x,P.z,8))dmg(e,240+ap*.9,'m');hr.hp=Math.min(s.hp,hr.hp+s.hp*.2);dash(-a.dx,-a.dz,6)}}
if(n=='SELENA'){
if(i==0)proj({x:P.x,z:P.z,dx:a.dx,dz:a.dz,sp:28,dmg:100+ap*.7,ty:'m',col:0x7fe0ff,life:1,sc:1,cb:()=>{for(let k=1;k<4;k++)hr.cd[k]=Math.max(0,hr.cd[k]-2)}});
if(i==1){if(!tg)ok=0;else{ghost(P.x,P.z,P.y);const d=D(tg.x-P.x,tg.z-P.z),k=Math.max(0,d-2)/d;P.x+=(tg.x-P.x)*k;P.z+=(tg.z-P.z)*k;P.emp=1;ring(P.x,P.z,2,0x7fe0ff)}}
if(i==2){orbT=12;ORB.forEach(o=>o.m.visible=true);msg('Quỹ đạo linh hồn')}
if(i==3){P.inv=3;PG.visible=false;Cl=[0,1,2].map(k=>{const g=actor(TX.SELENA,1);g.userData.sp.material=g.userData.sp.material.clone();g.userData.sp.material.opacity=.7;g.userData.sp.material.color.set(0x9adfff);scene.add(g);return{g,x:P.x+Math.cos(k*2.1)*3,z:P.z+Math.sin(k*2.1)*3,a:0}});ring(P.x,P.z,5,0x7fe0ff,.6)}}
if(n=='VELORA'){
if(i==0)proj({x:P.x,z:P.z,dx:a.dx,dz:a.dz,sp:38,dmg:105+ap*.65,ty:'m',col:0xe8a6ff,life:1,sc:2});
if(i==1){dash(a.dx,a.dz,8);P.emp=1;P.dg=.22;ring(P.x,P.z,2,0xe8a6ff,.25)}
if(i==2){const d=Math.min(a.d,12),bx=P.x+a.dx*d,bz=P.z+a.dz*d;ring(bx,bz,5,0xc87cff,.5);for(const e of near(bx,bz,5)){dmg(e,120+ap*.45,'m');e.sl=2.5}}
if(i==3){for(let k=0;k<4;k++)TM.push({t:.18*k,f:()=>{const e=nearest(P.x,P.z,11);if(e){ghost(P.x,P.z,P.y);const dx=e.x-P.x,dz=e.z-P.z,l=D(dx,dz)||1;dash(dx/l,dz/l,4);dmg(e,95+ap*.28,'m');ring(e.x,e.z,2,0xe8a6ff,.2)}}})}}
if(n=='MYRIEL'){
if(i==0)proj({x:P.x,z:P.z,dx:a.dx,dz:a.dz,sp:36,dmg:115+ap*.7,ty:'m',col:0x8edcff,sl:2.5,life:1,sc:2});
if(i==1){ghost(P.x,P.z,P.y);dash(a.dx,a.dz,7);P.dg=.3;ring(P.x,P.z,2,0x8edcff,.25)}
if(i==2){ring(P.x,P.z,6,0x8edcff,.45);for(const e of near(P.x,P.z,6)){dmg(e,130+ap*.5,'m');e.sl=3;e.st=Math.max(e.st,.5)}}
if(i==3){for(let k=0;k<5;k++)TM.push({t:k*.35,f:()=>{ring(P.x,P.z,8,0x8edcff,.28);for(const e of near(P.x,P.z,8)){dmg(e,70+ap*.22,'m');e.sl=2}}})}}
if(n=='CAELYN'){
if(i==0)proj({x:P.x,z:P.z,dx:a.dx,dz:a.dz,sp:55,dmg:135+ad*.75,ty:'p',col:0xa8d66d,life:.9,sc:4});
if(i==1){dash(a.dx,a.dz,7);P.emp=1;P.dg=.25;ring(P.x,P.z,1.5,0xa8d66d,.2)}
if(i==2){const d=Math.min(a.d,14),bx=P.x+a.dx*d,bz=P.z+a.dz*d;ring(bx,bz,4,0x7fa84c,.7);TM.push({t:.45,f:()=>{for(const e of near(bx,bz,4)){dmg(e,80+ad*.35,'p');e.st=1.1;e.sl=3}}})}
if(i==3){for(const k of[-.3,-.2,-.1,0,.1,.2,.3]){const c2=Math.cos(k),s2=Math.sin(k);proj({x:P.x,z:P.z,dx:a.dx*c2-a.dz*s2,dz:a.dx*s2+a.dz*c2,sp:50,dmg:65+ad*.3,ty:'p',col:0xa8d66d,life:.8,sc:3})}}}
if(n=='RAVENNA'){
if(i==0)for(const k of[-.15,0,.15]){const c2=Math.cos(k),s2=Math.sin(k);proj({x:P.x,z:P.z,dx:a.dx*c2-a.dz*s2,dz:a.dx*s2+a.dz*c2,sp:48,dmg:70+ad*.5,ty:'p',col:0xffb060,st:.9,life:.6,sc:3})}
if(i==1){dash(a.dx,a.dz,7);P.emp=1;P.dg=.35}
if(i==2){const d=Math.min(a.d,14),bx=P.x+a.dx*d,bz=P.z+a.dz*d;ring(bx,bz,.8,0xff7a3a,.6);TM.push({t:.6,f:()=>{ring(bx,bz,5,0xff7a3a,.4);for(const e of near(bx,bz,5)){dmg(e,190+ad*.6,'p');e.sl=3}}})}
if(i==3){rapid=3}}
if(!ok){msg('Không có mục tiêu trong tầm');return}hr.cd[i]=cds}
function dash(dx,dz,len,fn){const hit=new Set();for(let k=0;k<10;k++){step(P,dx*len/10,dz*len/10);if(fn)for(const e of near(P.x,P.z,1.8))if(!hit.has(e)){hit.add(e);fn(e)}if(k%3==0)ghost(P.x,P.z,P.y)}}
function flash(){if(G.flash>0)return;const a=aim();dash(a.dx,a.dz,8);P.dg=.4;G.flash=58}
function support(){if(G.sup>0)return;const hr=H[P.h],t=G.sel;if(t=='STUN'){for(const e of near(P.x,P.z,9))e.st=2;ring(P.x,P.z,9,0xffe08a);G.sup=28}
if(t=='HEAL'){hr.hp+=(hr.st.hp-hr.hp)*.3;ring(P.x,P.z,3,0x6aff9a);G.sup=18}
if(t=='CLEANSE'){P.stun=0;P.imm=3;ring(P.x,P.z,3,0xffffff);G.sup=30}
if(t=='EXECUTE'){for(const e of E)if(!e.dead&&!e.boss&&e.hp<e.mx*.15){ring(e.x,e.z,2,0xfff06a);e.hp=0;kill(e)}G.sup=45}}
function sw(n){if(NET.active){msg('Không thể đổi tướng trong đấu 1v1');return}if(!S.party.includes(n)||n==P.h||!H[n]||H[n].hp<=0&&n!=P.h)return;const old=PG.position;setHero(n);PG.position.copy(old);P.inv=0;Cl=[];orbT=0;ORB.forEach(o=>o.m.visible=false);rapid=0;ring(P.x,P.z,2,parseInt(HERO[n].c.slice(1),16),.3)}
function recall(){if(!play||P.rc>0)return;P.rc=3;msg('Đang biến về…')}
/* ---------- INPUT ---------- */
const K={};addEventListener('keydown',e=>{if(!play)return;K[e.code]=1;const c=e.code;
if(c=='KeyQ')skill(0);if(c=='KeyW'&&cm==0)skill(1);if(c=='KeyE')skill(2);if(c=='KeyR')skill(3);if(c=='KeyT')flash();if(c=='KeyF')support();if(c=='KeyB')recall();
if(c=='Space'){e.preventDefault();if(P.y<=gy(P.x,P.z,P.y)+.15)P.vy=12}
if(c=='Digit1')sw(S.party[0]);if(c=='Digit2')sw(S.party[1]);if(c=='Digit3')sw(S.party[2]);
if(c=='Tab'){e.preventDefault();sw(S.party[(S.party.indexOf(P.h)+1)%3])}
if(c=='KeyV'){cm=(cm+1)%3;$('xh').style.display=cm==2?'block':'none';msg(['Góc nhìn hành động','Góc nhìn thứ ba','Góc nhìn FPS'][cm]);if(cm==0)document.exitPointerLock&&document.exitPointerLock()}if(c=='KeyM'){S.opt.minimap=S.opt.minimap?0:1;save();drawMiniMap()}
if(c=='KeyG')talk();if(c=='Escape')toLobby()});
addEventListener('keyup',e=>K[e.code]=0);
cv.addEventListener('pointermove',e=>{if(document.pointerLockElement==cv){yaw-=e.movementX*.003;pitch=Math.max(-1.2,Math.min(1.2,pitch-e.movementY*.003))}else if(play&&cm==0){const p=pick(e);if(p){M.x=p.x;M.z=p.z}}});
cv.addEventListener('pointerdown',e=>{if(!play)return;if(cm>0){if(document.pointerLockElement!=cv)try{cv.requestPointerLock()}catch(x){}else attack();return}
const p=pick(e);if(!p)return;M.x=p.x;M.z=p.z;const t=nearest(p.x,p.z,3);if(t){P.tgt=t;P.dest=null}else{P.tgt=null;P.dest={x:p.x,z:p.z};ring(p.x,p.z,.7,0xffffff,.3)}});
cv.addEventListener('wheel',e=>{zoom=Math.max(10,Math.min(38,zoom+e.deltaY*.02))});
cv.addEventListener('contextmenu',e=>e.preventDefault());
function talk(){if(!NPC||D(NPC.x-P.x,NPC.z-P.z)>5)return;if(Q.s==0){Q.s=1;msg('Isolde: Hãy tìm 3 Mảnh Trăng trong khu rừng.')}else if(Q.s==1&&SH.every(s=>s.got)){Q.s=2;S.gold+=200;S.tk+=1;msg('Hoàn thành nhiệm vụ: +200 vàng, +1 vé');save()}else if(Q.s==2)msg('Isolde: Con Ma Hươu đang chờ ở phía bắc.');else msg('Isolde: Vẫn còn thiếu Mảnh Trăng…')}
/* ---------- UPDATE ---------- */
function update(dt){const b=HERO[P.h],hr=H[P.h],s=hr.st,sp=b.spd*(gh(P.x,P.z)<-.5?.7:1);
for(const n of S.party){const h=H[n];for(let i=0;i<4;i++)h.cd[i]=Math.max(0,h.cd[i]-dt)}G.flash=Math.max(0,G.flash-dt);G.sup=Math.max(0,G.sup-dt);P.at=Math.max(0,P.at-dt);P.dg=Math.max(0,P.dg-dt);P.imm=Math.max(0,P.imm-dt);P.stun=Math.max(0,(Number.isFinite(P.stun)?P.stun:0)-dt);P.ro=Math.max(0,P.ro-dt);
let mx=0,mz=0;const fx=-Math.sin(yaw),fz=-Math.cos(yaw),rx=Math.cos(yaw),rz=-Math.sin(yaw);if(cm>0){if(K.KeyW){mx+=fx;mz+=fz}if(K.KeyS){mx-=fx;mz-=fz}if(K.KeyA){mx-=rx;mz-=rz}if(K.KeyD){mx+=rx;mz+=rz}}
if(!NET.dead&&P.stun<=0){if(mx||mz){P.dest=null;P.tgt=cm==0?P.tgt:null;const l=D(mx,mz);step(P,mx/l*sp*dt,mz/l*sp*dt);if(cm==0)face(mx,mz);P.rc=0}
else if(P.tgt&&!P.tgt.dead){const dx=P.tgt.x-P.x,dz=P.tgt.z-P.z,d=D(dx,dz);face(dx,dz);if(d>b.rng*.9+P.tgt.ex*.5){step(P,dx/d*sp*dt,dz/d*sp*dt);P.rc=0}else attack()}
else if(P.dest){const dx=P.dest.x-P.x,dz=P.dest.z-P.z,d=D(dx,dz);if(d<.4)P.dest=null;else{step(P,dx/d*sp*dt,dz/d*sp*dt);face(dx,dz);P.rc=0}}
if(cm>0&&K.Mouse)attack()}
if(rapid>0){rapid-=dt;fd-=dt;if(fd<=0){fd=.1;const a=aim(),t=nearest(P.x,P.z,16);let dx=a.dx,dz=a.dz;if(t&&cm==0){dx=t.x-P.x;dz=t.z-P.z;const l=D(dx,dz)||1;dx/=l;dz/=l}face(dx,dz);proj({x:P.x,z:P.z,dx:dx+rn(-.05,.05),dz,sp:50,dmg:40+s.ad*.35,ty:'p',col:0xffd27a,sc:3,life:.5});P.ro=.06}}
const g=gy(P.x,P.z,P.y+.5);P.vy-=32*dt;P.y+=P.vy*dt;if(P.y<=g){P.y=g;P.vy=0}
if(P.rc>0){P.rc-=dt;if(Math.random()<.3)ring(P.x,P.z,1.5,0x9ad0ff,.5);if(P.rc<=0){P.x=3;P.z=3;P.y=gy(3,3,99);hr.hp=s.hp;ring(P.x,P.z,4,0xffffff);msg('Đã trở về tế đàn');save()}}
if(D(P.x-altar.x,P.z-altar.z)<5)for(const n of S.party)H[n].hp=Math.min(H[n].st.hp,H[n].hp+H[n].st.hp*.05*dt);
if(P.inv>0){P.inv-=dt;if(Math.random()<.3)ghost(P.x,P.z,P.y);if(P.inv<=0){PG.visible=cm!=2;Cl.forEach(c=>scene.remove(c.g));Cl=[]}}
for(const c of Cl){c.a+=dt;const e=nearest(c.x,c.z,12);if(e){const dx=e.x-c.x,dz=e.z-c.z,d=D(dx,dz);if(d>2){c.x+=dx/d*9*dt;c.z+=dz/d*9*dt}else if(c.a%.5<dt){dmg(e,40+s.ap*.3,'m')}}c.g.position.set(c.x,gy(c.x,c.z,99),c.z);c.g.rotation.y=Math.atan2(cam.position.x-c.x,cam.position.z-c.z)}
if(orbT>0){orbT-=dt;ORB.forEach((o,i)=>{const an=performance.now()/350+i*1.256;let x=P.x+Math.cos(an)*1.7,z=P.z+Math.sin(an)*1.7,y=P.y+1.4;if(o.d>0){o.d-=dt;const f=Math.sin(Math.PI*(1-o.d/.3));if(o.t&&!o.t.dead){x+=(o.t.x-x)*f;z+=(o.t.z-z)*f}}o.m.position.set(x,y,z);if(orbT<=0)o.m.visible=false})}
for(let i=PR.length-1;i>=0;i--){const p=PR[i];p.life-=dt;p.x+=p.dx*p.sp*dt;p.z+=p.dz*p.sp*dt;p.m.position.set(p.x,P.y+1.4,p.z);let done=p.life<=0||!!solid(p.x,p.z,P.y+1.4);
if(!done)for(const e of combatTargets()){if(e.dead||D(e.x-p.x,e.z-p.z)>e.ex*.9+.5)continue;dmg(e,p.dmg,p.ty);if(p.st)e.st=p.st;if(p.sl)e.sl=p.sl;if(p.cb)p.cb();ring(p.x,p.z,1,p.col,.2);done=1;break}
if(done){scene.remove(p.m);PR.splice(i,1)}}
for(let i=TM.length-1;i>=0;i--){TM[i].t-=dt;if(TM[i].t<=0){TM[i].f();TM.splice(i,1)}}
for(const e of E){if(e.dead)continue;e.st-=dt;e.sl-=dt;e.ac-=dt;let tx=null;if(Cl.length){let bd=30;for(const c of Cl){const d=D(c.x-e.x,c.z-e.z);if(d<bd){bd=d;tx=c}}}else if(P.inv<=0&&D(P.x-e.x,P.z-e.z)<26)tx=P;
if(tx&&e.st<=0){const dx=tx.x-e.x,dz=tx.z-e.z,d=D(dx,dz);if(d>e.rg){const v=e.sp*(e.sl>0?.5:1)*dt;step(e,dx/d*v,dz/d*v)}else if(e.ac<=0){e.ac=1.3;if(tx===P)hurt(e.dm);else ring(tx.x,tx.z,1,0xff4040,.2)}}
e.y=gy(e.x,e.z,99);e.g.position.set(e.x,e.y,e.z);e.g.rotation.y=Math.atan2(cam.position.x-e.x,cam.position.z-e.z);e.g.userData.bar.scale.x=Math.max(.01,e.hp/e.mx);e.g.userData.bar.position.x=-(1-e.hp/e.mx)*.8*e.ex}
for(let i=FX.length-1;i>=0;i--){const f=FX[i];f.t-=dt;if(f.g)f.m.material.opacity=Math.max(0,f.t*1.4);else{const k=1-f.t/f.T;f.m.scale.setScalar(.3+f.r*k);f.m.material.opacity=.8*(1-k)}if(f.t<=0){scene.remove(f.m);FX.splice(i,1)}}
for(const q of SH){if(!q.got&&D(q.x-P.x,q.z-P.z)<2.2&&Q.s>=1){q.got=1;W.remove(q.m);msg('Moonshard '+SH.filter(z=>z.got).length+'/3')}q.m.rotation.y+=dt*2}
torch.intensity=1.2+Math.sin(performance.now()/90)*.2;
PG.position.set(P.x,P.y,P.z);PG.rotation.y=Math.atan2(cam.position.x-P.x,cam.position.z-P.z);PG.userData.sp.position.x=-Math.sin(P.f)*P.ro*3*0;PG.visible=P.inv<=0&&cm!=2;PG.userData.sp.material.opacity=1;
moon.position.set(P.x-40,P.y+70,P.z-30);moon.target.position.set(P.x,P.y,P.z);
cam.fov=S.opt.fov;shk=Math.max(0,shk-dt*.8);
const hy=P.y+1.7;
if(cm==0){cam.position.set(P.x,P.y+zoom*.9,P.z+zoom*.75);cam.lookAt(P.x,P.y+1,P.z)}
else if(cm==1){const cp=Math.cos(pitch),sx=-Math.sin(yaw)*cp,sz=-Math.cos(yaw)*cp,sy=Math.sin(pitch);let d=8;for(;d>1;d-=.5){const x=P.x-sx*d,z=P.z-sz*d,y=hy-sy*d;if(y>gy(x,z,99)+.6&&!solid(x,z,y))break}cam.position.set(P.x-sx*d,hy-sy*d,P.z-sz*d);cam.lookAt(P.x,hy,P.z)}
else{const cp=Math.cos(pitch),bob=S.opt.bob&&(mx||mz)?Math.sin(performance.now()/110)*.06:0;cam.position.set(P.x,hy+bob,P.z);cam.lookAt(P.x-Math.sin(yaw)*cp,hy+Math.sin(pitch),P.z-Math.cos(yaw)*cp)}
if(shk>0){const shakeAmt=S.opt.shk??S.opt.shake??1;cam.position.add(new THREE.Vector3(rn(-1,1),rn(-1,1),rn(-1,1)).multiplyScalar(shk*shakeAmt*.4))}
if(cm==0)P.f=P.f;if(!(mx||mz)&&cm>0)P.f=yaw+Math.PI;netTick(dt)}
document.addEventListener('mousedown',e=>{if(e.button==0)K.Mouse=1});document.addEventListener('mouseup',()=>K.Mouse=0);

/* ---------- MINI MAP + QUEST GUIDE ---------- */
function questInfo(){
 if(NET.active){const r=NET.remoteObj&&!NET.remoteObj.dead?NET.remoteObj:null;return{title:'ĐẤU TRƯỜNG 1v1',desc:r?'Đánh bại đối thủ':'Đang chờ đối thủ...',target:r?{x:r.x,z:r.z}:null,color:'#ff6b8a'}}
 if(CH[ci]&&CH[ci].dg){const b=E.find(e=>e.boss&&!e.dead);return{title:'PHÓ BẢN',desc:b?'Tiêu diệt '+CH[ci].boss:'Boss đã bị tiêu diệt',target:b?{x:b.x,z:b.z}:null,color:'#ff9b5c'}}
 if(Q.s==0&&NPC)return{title:'NHIỆM VỤ',desc:'Đến gặp Isolde và nhấn G',target:{x:NPC.x,z:NPC.z},color:'#ffd56a'};
 if(Q.s==1){const left=SH.filter(s=>!s.got);if(left.length){let q=left[0],bd=1e9;for(const s of left){const d=D(s.x-P.x,s.z-P.z);if(d<bd){bd=d;q=s}}return{title:'NHIỆM VỤ',desc:`Thu thập Mảnh Trăng ${SH.filter(s=>s.got).length}/3`,target:{x:q.x,z:q.z},color:'#8fdcff'}}if(NPC)return{title:'NHIỆM VỤ',desc:'Quay lại gặp Isolde',target:{x:NPC.x,z:NPC.z},color:'#ffd56a'}}
 const b=E.find(e=>e.boss&&!e.dead);return{title:'NHIỆM VỤ',desc:b?'Tiêu diệt boss: '+CH[ci].boss:'Khám phá khu vực',target:b?{x:b.x,z:b.z}:null,color:'#ff7f7f'}
}
function miniXY(x,z,w,h){return{x:(x+100)/200*w,y:(z+100)/200*h}}
function drawMiniMap(){const cv=$('minimap');if(!cv)return;const wrap=$('minimapWrap');if(wrap)wrap.style.display=S.opt.minimap?'block':'none';if(!S.opt.minimap)return;const x=cv.getContext('2d'),w=cv.width,h=cv.height;x.clearRect(0,0,w,h);x.save();x.beginPath();x.arc(w/2,h/2,w*.48,0,Math.PI*2);x.clip();x.fillStyle='#0b0a12';x.fillRect(0,0,w,h);x.strokeStyle='#272039';x.lineWidth=1;for(let i=20;i<180;i+=20){x.beginPath();x.moveTo(i,0);x.lineTo(i,h);x.stroke();x.beginPath();x.moveTo(0,i);x.lineTo(w,i);x.stroke()}
 const dot=(wx,wz,r,c)=>{const p=miniXY(wx,wz,w,h);x.fillStyle=c;x.beginPath();x.arc(p.x,p.y,r,0,Math.PI*2);x.fill()};
 dot(altar.x,altar.z,4,'#6dff91');if(NPC)dot(NPC.x,NPC.z,4,'#ffd56a');for(const s of SH)if(!s.got)dot(s.x,s.z,3,'#76dfff');for(const e of E){if(e.dead)continue;dot(e.x,e.z,e.boss?4:1.8,e.boss?'#ff9b5c':'#d55268')}if(NET.remoteObj&&!NET.remoteObj.dead)dot(NET.remoteObj.x,NET.remoteObj.z,4,'#ff61e6');
 const qi=questInfo();if(qi.target){const q=miniXY(qi.target.x,qi.target.z,w,h);x.strokeStyle=qi.color||'#fff';x.lineWidth=2;x.beginPath();x.arc(q.x,q.y,7,0,Math.PI*2);x.stroke()}
 const p=miniXY(P.x,P.z,w,h);x.save();x.translate(p.x,p.y);x.rotate(Math.PI-P.f);x.fillStyle='#ffffff';x.beginPath();x.moveTo(0,-7);x.lineTo(5,6);x.lineTo(-5,6);x.closePath();x.fill();x.restore();x.restore();x.strokeStyle='#6d5a8d';x.lineWidth=2;x.beginPath();x.arc(w/2,h/2,w*.48,0,Math.PI*2);x.stroke()}
function questHud(){const q=questInfo();let dist='',rot=0;if(q.target){const dx=q.target.x-P.x,dz=q.target.z-P.z;dist=` · ${Math.round(D(dx,dz))}m`;rot=(Math.atan2(dx,-dz)+(cm>0?yaw:0))*180/Math.PI}return`<b class="hd">${q.title}</b><br>${q.desc}${dist} <span id="questArrow" style="transform:rotate(${rot}deg)">↑</span>`}

/* ---------- HUD ---------- */
let ht=0;function hud(){const h=$('party');h.innerHTML=S.party.map((n,i)=>{const r=H[n],e=stat(n),ic=['p','m','d'].map(t=>{const it=item(S.eq[n]&&S.eq[n][t]);return it?`<span class="${it.m?'myth':''}" title="${it.n}">${TYPE[t][1]}</span>`:'<span class="dim">·</span>'}).join(' ');
return`<div class="pc ${n==P.h?'on':''}" onclick="sw('${n}')"><b class="hd" style="color:${HERO[n].c}">${i+1} ${n}</b> Lv ${S.hl[n]||1}<div class="bar"><i style="width:${Math.max(0,r.hp/r.st.hp*100)}%"></i></div><small>${Math.round(r.hp)}/${Math.round(r.st.hp)} ${ic}</small></div>`}).join('');
const b=HERO[P.h],c=H[P.h].cd;$('sk').innerHTML=['Q','W','E','R'].map((k,i)=>`<div class="sb"><b>${k}</b>${b.sk[i]}<u>${c[i]>0?c[i].toFixed(1):''}</u></div>`).join('')+`<div class="sb"><b>T</b>Flash<u>${G.flash>0?G.flash|0:''}</u></div><div class="sb"><b>F</b>${G.sel}<u>${G.sup>0?G.sup|0:''}</u></div><div class="sb" onclick="recall()"><b>B</b>Recall</div>`;
$('tr').innerHTML=`<b class="hd">${CH[ci].n}</b><br>Hạ gục ${G.kills}/${G.total} · Vàng ${S.gold} · Vé ${S.tk}<hr style="border:0;border-top:1px solid var(--ln)">${questHud()}<br><span class="dim">Click đất: di chuyển · Q/W/E/R: kỹ năng · Space: nhảy · 1/2/3: đổi tướng · V: đổi camera · M: bản đồ nhỏ · G: nói chuyện · B: biến về</span><br><button onclick="toLobby()">Về sảnh</button>`;drawMiniMap()}
/* ---------- LOOP ---------- */
let last=performance.now();function loop(t){requestAnimationFrame(loop);const dt=Math.min(.05,(t-last)/1000);last=t;if(play){update(dt);ht-=dt;if(ht<=0){ht=.2;hud()}}R.render(scene,cam)}
/* ---------- LOBBY + PANELS ---------- */
const MENU=[['PLAY','CHƠI'],['CHARACTERS','TƯỚNG'],['PARTY','ĐỘI HÌNH'],['INVENTORY','TÚI ĐỒ'],['GACHA','GACHA'],['EVENTS','SỰ KIỆN'],['MAIL','THƯ'],['FRIENDS','BẠN BÈ / PVP'],['SHOP','CỬA HÀNG'],['WORLD MAP','BẢN ĐỒ THẾ GIỚI'],['SETTINGS','CÀI ĐẶT'],['PROFILE','HỒ SƠ']];
function lobby(){$('lm').innerHTML='<h1>Ashen Vigil</h1>'+(play||H.__on?'<button class="p" onclick="resume()">TIẾP TỤC</button>':'')+MENU.map(([k,l])=>`<button onclick="openP('${k}')">${l}</button>`).join('');
const c=art(S.av,HERO[S.av].c).image;c.id='lcc';$('lc').replaceChildren(c);$('ln').textContent=S.name;$('ls').textContent=`${S.av} · Lv ${S.lv} · ID ${S.id}`}
function toLobby(){if(document.exitPointerLock)document.exitPointerLock();if(NET.active)netLeaveBattle();play=false;$('hud').style.display='none';$('lobby').style.display='flex';$('xh').style.display='none';save();lobby()}
function resume(){$('lobby').style.display='none';closeP();$('hud').style.display='block';play=true;last=performance.now()}
function closeP(){$('panel').style.display='none'}
function P_(t,b){$('pb').innerHTML=`<h2 class="hd">${t}</h2>${b}<div class="row"><span></span><button onclick="closeP()">Đóng</button></div>`;$('panel').style.display='flex'}
const it2=i=>`<span class="${i.m?'myth':''}">${TYPE[i.t][1]} ${i.n} +${i.v}</span>`;
function openP(k){const f={PLAY:pPlay,CHARACTERS:pChars,PARTY:pParty,INVENTORY:pInv,GACHA:pGacha,EVENTS:pEv,MAIL:pMail,FRIENDS:pFr,SHOP:pShop,'WORLD MAP':pMap,SETTINGS:pSet,PROFILE:pProf};f[k]()}
function pPlay(){P_('Chơi',`<div class="row"><span><b>Phiêu lưu</b><br><span class="dim">Cốt truyện thế giới mở — chọn chương trên bản đồ thế giới.</span></span><button class="p" onclick="openP('WORLD MAP')">Chọn bản đồ</button></div>
<div class="row"><span><b>Phó bản</b><br><span class="dim">Farm boss và vật phẩm; boss phó bản có thể rơi đồ Vô Song. Mở sau Chương 1.</span></span><button onclick="openP('WORLD MAP')">Vào</button></div>
<div class="row"><span><b>Chiến trường / PvP</b><br><span class="dim">Tìm người chơi bằng ID, gửi lời thách đấu rồi vào phòng thời gian thực.</span></span><button class="p" onclick="pFr()">Tìm đối thủ</button></div>
<div class="row"><span><b>Chơi cùng bạn</b><br><span class="dim">Dùng chung nền tảng mạng với PvP; Co-op PvE sẽ bổ sung sau.</span></span><button disabled>Sắp có</button></div>
<div class="row"><span><b>Chế độ sự kiện</b></span><button disabled>Sắp có</button></div>`)}
function pChars(){P_('Tướng',S.own.map(n=>{const s=stat(n),l=S.hl[n]||1,b=HERO[n];return`<div class="row"><span><b style="color:${b.c}">${n}</b> Lv ${l} <span class="dim">${b.bt=='m'?'Phép':'Vật lý'} · ${b.rg?'Đánh xa':'Đánh gần'}</span><br><span class="dim">${b.pas}</span><br>Máu ${Math.round(s.hp)} · Vật lý ${Math.round(s.ad)} · Phép ${Math.round(s.ap)} · Tốc đánh +${(s.as*100).toFixed(0)}% · Hồi chiêu ${(s.cdr*100).toFixed(0)}% · Giáp ${Math.round(s.arm)} · Hút máu ${(s.ls*100)|0}%</span></span><span><button onclick="S.av='${n}';lobby();pChars()">Chọn</button> <button onclick="upg('${n}')">Nâng cấp ${l*150}g</button></span></div>`}).join(''))}
function upg(n){const l=S.hl[n]||1;if(S.gold<l*150)return msg2('Không đủ vàng');S.gold-=l*150;S.hl[n]=l+1;save();pChars()}
function msg2(t){alert&&0;$('ls').textContent=t}
function pParty(){P_('Đội hình (chọn 3)',`<div class="dim">Đang dùng: ${S.party.join(', ')}</div>`+S.own.map(n=>`<div class="row"><b style="color:${HERO[n].c}">${n}</b><button onclick="tp('${n}')">${S.party.includes(n)?'Gỡ':'Thêm'}</button></div>`).join(''))}
function tp(n){if(S.party.includes(n)){if(S.party.length>1)S.party=S.party.filter(x=>x!=n)}else if(S.party.length<3)S.party.push(n);save();pParty()}
function pInv(){const sel=S.av;P_('Túi đồ — đang trang bị cho '+sel,`<div class="dim">Đổi tướng trong mục Tướng → Chọn.</div>`+(S.inv.length?S.inv.map(i=>{const on=S.eq[sel]&&S.eq[sel][i.t]==i.id;return`<div class="row"><span>${it2(i)} ${i.m?'<span class="dim">Vô Song: +8% hút máu</span>':''}</span><button onclick="eqp(${i.id})">${on?'Tháo':'Trang bị'}</button></div>`}).join(''):'<p>Túi trống. Hãy quay gacha hoặc mua trang bị trong cửa hàng.</p>'))}
function eqp(id){const i=item(id),n=S.av;S.eq[n]=S.eq[n]||{};S.eq[n][i.t]=S.eq[n][i.t]==id?0:id;save();pInv()}
function pGacha(){P_('Gacha',`<p>Vé ${S.tk}. Bảo hiểm ${S.pity}/20 — mỗi 20 lượt đảm bảo vật phẩm Vô Song hoặc tướng mới.</p><button class="p" onclick="pull(1)">Quay ×1</button> <button onclick="pull(10)">Quay ×10</button><div id="gr"></div>`)}
function pull(n){if(S.tk<n){$('gr').innerHTML='<p>Không đủ vé. Hãy vượt map, nhận thư hoặc mua trong cửa hàng.</p>';return}const out=[];for(let i=0;i<n;i++){S.tk--;S.pity++;const r=Math.random();let o;if(S.pity>=20||r<.03){S.pity=0;const it=mk('pmd'[rn(3)|0],1);S.inv.push(it);o=it2(it)+' (Mythic)'}else if(r<.6){const it=mk('pmd'[rn(3)|0],0);S.inv.push(it);o=it2(it)}else{const g=rn(50,150)|0;S.gold+=g;o=`<span class="dim">Nguyên liệu → ${g} vàng</span>`}out.push(o)}save();pGacha();$('gr').innerHTML=out.map(o=>`<div class="row">${o}</div>`).join('')}
function pEv(){const d=S.daily!=today(),w=S.kills>=30&&!S.wk;P_('Sự kiện',`<div class="row"><span><b>Đăng nhập hằng ngày</b><br><span class="dim">+2 tickets, 200 gold</span></span><button ${d?'':'disabled'} onclick="S.daily=today();S.tk+=2;S.gold+=200;save();pEv()">${d?'Claim':'Claimed'}</button></div>
<div class="row"><span><b>Nhiệm vụ tuần: hạ 30 quái</b><br><span class="dim">${Math.min(30,S.kills)}/30 · đặt lại hằng tuần</span></span><button ${w?'':'disabled'} onclick="S.wk=1;S.tk+=5;save();pEv()">${S.wk?'Claimed':'Claim 5 tickets'}</button></div>
<div class="row"><span><b>Sự kiện giới hạn / Chiến đấu / Thử thách đặc biệt</b><br><span class="dim">Cần máy chủ sự kiện trực tuyến.</span></span><button disabled>Sắp có</button></div>`)}
function claim(i){const m=S.mail[i];if(m.done)return;const a=m.a;if(a.tk)S.tk+=a.tk;if(a.gold)S.gold+=a.gold;if(a.trial)S.trial[a.trial]=Date.now()+6048e5;if(a.skin)S.skins[a.skin]=Date.now()+6048e5;m.done=1;save()}
function pMail(){P_('Thư',`<button onclick="S.mail.forEach((m,i)=>claim(i));pMail()">Nhận tất cả</button>`+S.mail.map((m,i)=>`<div class="row"><span><b>${m.t}</b> <span class="dim">từ ${m.f}</span><br>${m.m}<br><span class="tag">${a2(m.a)}</span></span><button ${m.done?'disabled':''} onclick="claim(${i});pMail()">${m.done?'Claimed':'Claim'}</button></div>`).join(''))}
const a2=a=>[a.tk&&a.tk+' tickets',a.gold&&a.gold+' gold',a.trial&&a.trial+' trial (7d)',a.skin&&a.skin+' EPIC skin trial (7d)'].filter(Boolean).join(', ');
async function pFr(){
 const req=NET.ready?await netLoadRequests():[];const incoming=NET.incoming.map(c=>`<div class="row"><span><b>${c.fromName||c.fromId}</b><br><span class="dim">Duel invitation · room ${c.room}</span></span><button class="p" onclick="netAcceptChallenge('${c.key}')">Chấp nhận đấu</button></div>`).join('');
 const requests=req.map(r=>`<div class="row"><span>Lời mời kết bạn từ <b>${r.name||r.from}</b></span><button onclick="netAcceptFriend('${r.from}')">Chấp nhận</button></div>`).join('');
 const fl=Object.keys(NET.friends||{}).map(id=>`<div class="row"><span>Bạn <b>${id}</b></span><button onclick="netChallenge('${id}')">Đấu 1v1</button></div>`).join('');
 const sr=NET.search?(NET.search.missing?`<div class="row"><span>Không tìm thấy người chơi có ID <b>${NET.search.id}</b>.</span></div>`:`<div class="row"><span><b>${NET.search.name||'Player'}</b> · ID ${NET.search.id}<br><span class="dim">${NET.search.online?'<span class="online">Online</span>':'<span class="offline">Offline</span>'} · ${NET.search.hero||''}</span></span><span><button onclick="netAddFriend('${NET.search.id}')">Kết bạn</button> <button class="p" onclick="netChallenge('${NET.search.id}')">Đấu 1v1</button></span></div>`):'';
 P_('Bạn bè / PvP',`<p>Mạng: <b class="${NET.ready?'online':'offline'}">${NET.status}</b><br>Your ID người chơi: <b>${S.id}</b></p>${NET.ready?'':`<p class="dim">GitHub Pages không tự chạy phòng thời gian thực. Hãy điền cấu hình Firebase vào FIREBASE_CONFIG, bật Đăng nhập ẩn danh và Realtime Database rồi đăng lại.</p>`}<div class="row"><span><input id="fid" placeholder="Nhập chính xác ID người chơi"></span><button ${NET.ready?'':'disabled'} onclick="netSearch()">Tìm</button></div>${sr}${incoming?'<h3>Lời mời đấu</h3>'+incoming:''}${requests?'<h3>Lời mời kết bạn</h3>'+requests:''}${fl?'<h3>Bạn bè</h3>'+fl:'<p class="dim">Chưa có bạn bè.</p>'}`);$('pb').dataset.page='friends'
}
function pShop(){P_('Cửa hàng',`<div class="row"><span>Vé gacha</span><button onclick="buy('tk',300)">300g</button></div>`+['p','m','d'].map(t=>`<div class="row"><span>${TYPE[t][0]} gear</span><button onclick="buy('${t}',180)">180g</button></div>`).join('')+`<p class="dim">Vàng ${S.gold}</p>`)}
function buy(t,c){if(S.gold<c)return;S.gold-=c;if(t=='tk')S.tk++;else S.inv.push(mk(t,0));save();pShop()}
function pMap(){P_('Bản đồ thế giới',`<div class="row"><span>Phép bổ trợ cho lượt chơi này: </span>${[['STUN','CHOÁNG'],['HEAL','HỒI MÁU'],['CLEANSE','THANH TẨY'],['EXECUTE','KẾT LIỄU']].map(([s,l])=>`<label><input type="radio" name="sup" value="${s}" ${G.sel==s?'checked':''}>${l}</label>`).join(' ')}</div>`+CH.map((c,i)=>{const un=c.dg?S.cleared.includes(0):i<=S.maxCh;return`<div class="row"><span><b>${c.n}</b> ${S.cleared.includes(i)?'<span class="tag">Đã vượt</span>':''}<br><span class="dim">Cấp đề nghị ${c.lv} · Quái: ${c.en} · Boss: ${c.boss} · Hoàn thành ${S.comp[i]||0}% · Thưởng: ${c.rw}</span></span><button ${un?'':'disabled'} class="p" onclick="start(${i})">${un?'Đi tới':'Khóa'}</button></div>`}).join(''))}
function start(i){const q=document.querySelector('input[name=sup]:checked');G.sel=q?q.value:'STUN';refreshH();if(!ORB.length)for(let k=0;k<5;k++){const m=new THREE.Mesh(new THREE.SphereGeometry(.22,8,6),new THREE.MeshBasicMaterial({color:0x7fe0ff}));m.visible=false;scene.add(m);ORB.push({m,d:0})}
const first=S.party.includes(S.av)?S.av:S.party[0];build(i);for(const n of S.party){const h=heroSt(n);h.hp=h.st.hp;h.cd=[0,0,0,0]}setHero(first);H.__on=1;cm=0;resume()}
function pSet(){const o=S.opt;P_('Cài đặt',`<div class="row"><span>FOV ${o.fov}</span><input type="range" min="70" max="110" value="${o.fov}" oninput="S.opt.fov=+this.value;resize();save()"></div>
<div class="row"><span>Rung camera</span><input type="range" min="0" max="1" step=".1" value="${o.shk??o.shake??1}" oninput="S.opt.shk=+this.value;save()"></div>
<div class="row"><span>Tỉ lệ render</span><input type="range" min=".5" max="1" step=".1" value="${o.rs}" oninput="S.opt.rs=+this.value;resize();save()"></div>
<div class="row"><span>Bóng đổ</span><button onclick="S.opt.sh=S.opt.sh?0:1;resize();save();pSet()">${o.sh?'Bật':'Tắt'}</button></div>
<div class="row"><span>Lắc đầu (FPS)</span><button onclick="S.opt.bob=S.opt.bob?0:1;save();pSet()">${o.bob?'Bật':'Tắt'}</button></div>
<div class="row"><span>Bản đồ nhỏ (M)</span><button onclick="S.opt.minimap=S.opt.minimap?0:1;save();pSet()">${S.opt.minimap?'Bật':'Tắt'}</button></div>
<div class="row"><span class="dim">Âm thanh nâng cao, AA, AO, bloom và cấp texture sẽ bổ sung sau.</span></div>
<div class="row"><span><b>Chơi lại từ đầu</b><br><span class="dim">Xóa toàn bộ tiến trình.</span></span><button onclick="rst1()">Đặt lại…</button></div>`)}
function rst1(){P_('Chơi lại từ đầu?','<p>Thao tác này sẽ xóa cốt truyện, tướng, trang bị, tiền, nhiệm vụ và bảo hiểm gacha.</p><button onclick="rst2()">Tiếp tục</button>')}
function rst2(){P_('Xác nhận cuối cùng','<p><b>Bạn có chắc muốn xóa toàn bộ tiến trình?</b> Không thể hoàn tác.</p><button class="p" onclick="try{localStorage.removeItem(\'av1\')}catch(e){};location.reload()">Xóa toàn bộ</button>')}
function pProf(){const sk=Object.keys(S.skins).map(k=>k+' EPIC (trial)').join(', ')||'none';P_('Hồ sơ',`<div class="row"><span>Tên <input id="nm" value="${S.name}" maxlength="16"></span><button onclick="S.name=$('nm').value||'Wanderer';save();netRefreshProfile();lobby();pProf()">Lưu</button></div><div class="row"><span>Ảnh đại diện</span><span>${S.own.map(n=>`<button onclick="S.av='${n}';save();netRefreshProfile();lobby();pProf()">${n}${S.av==n?' ✓':''}</button>`).join(' ')}</span></div>
<p>ID người chơi <b>${S.id}</b> · Level ${S.lv} · EXP ${S.xp}/${S.lv*100}<br>Monsters slain ${S.kills} · Maps cleared ${S.cleared.length} · Vàng ${S.gold} · Skins: ${sk}</p>`)}
resize();lobby();netInit();requestAnimationFrame(loop);
</script></body></html>