<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rizq Tasbih</title>
<link rel="manifest" href="manifest.json">
<style>
  body {
    margin: 0;
    padding: 20px;
    font-family: system-ui, Arial, sans-serif;
    background: linear-gradient(135deg, #0f766e, #022c22);
    color: #ecfeff;
    text-align: center;
  }
  h1 { color: #a7f3d0; margin-bottom: 25px;}
  .card {
    background: rgba(255,255,255,0.08);
    border-radius: 20px;
    padding: 20px;
    margin-bottom: 25px;
  }
  .ar { font-size: 20px; margin-bottom:5px;}
  .tr { font-size: 14px; font-style: italic; color: #ccfbf1; margin-bottom:5px;}
  .en { font-size: 14px; color: #99f6e4; margin-bottom:10px;}
  .count { font-size: 26px; margin: 10px;}
  .bead {
    width: 140px;
    height: 140px;
    border-radius: 50%;
    background: radial-gradient(circle at top, #5eead4, #0f766e);
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 15px auto;
    font-size: 22px;
    color: #022c22;
    cursor: pointer;
    user-select: none;
  }
  button {
    margin-top: 10px;
    border: none;
    border-radius: 20px;
    padding: 8px 18px;
    background: #134e4a;
    color: #ccfbf1;
    cursor: pointer;
  }
  input {
    width: 80px;
    padding: 6px;
    border-radius: 6px;
    border: none;
    text-align: center;
  }
</style>
</head>
<body>
<h1>Rizq Tasbih 📿</h1>
<div id="app"></div>

<script>
const duas=[
  {id:"d1",ar:"اللهم اكفني بحلالك عن حرامك واغنني برحمتك عمن سواك",
   tr:"Allahumma-kfini bihalalika ‘an haramika wa aghnini birahmatika ‘amman siwaka",
   en:"O Allah, suffice me with what You made lawful and make me independent of others."},
  {id:"d2",ar:"حسبنا الله سيؤتينا الله من فضله إنا إلى الله راغبون",
   tr:"Hasbunallahu sayu’tinallahu min fadlihi inna ilallahi raghibun",
   en:"Allah is sufficient for us. Allah will give us from His bounty."},
  {id:"d3",ar:"ربنا إني لما أنزلت إليّ من خير فقير",
   tr:"Rabbani inni lima anzalta ilayya min khayrin faqir",
   en:"My Lord, I am in need of whatever good You send to me."}
];

const app=document.getElementById("app");

duas.forEach(d=>{
  let c=localStorage.getItem(d.id)||0;
  let card=document.createElement("div");
  card.className="card";
  card.innerHTML=`
    <div class="ar">${d.ar}</div>
    <div class="tr">${d.tr}</div>
    <div class="en">${d.en}</div>
    <div class="count">Count: <span id="${d.id}">${c}</span></div>
    <div>Target: <input type="number" id="${d.id}t" value="100"></div>
    <div class="bead" id="${d.id}b">Tap</div>
    <button id="${d.id}r">Reset</button>`;
  app.appendChild(card);

  document.getElementById(d.id+"b").onclick=()=>{
    c++;document.getElementById(d.id).innerText=c;
    localStorage.setItem(d.id,c);
    navigator.vibrate && navigator.vibrate(40);
  };
  document.getElementById(d.id+"r").onclick=()=>{
    if(confirm("Reset count?")){
      c=0;document.getElementById(d.id).innerText=0;
      localStorage.setItem(d.id,0);
    }
  };
});

// Service Worker registration (optional PWA)
if("serviceWorker" in navigator){
  navigator.serviceWorker.register("service-worker.js");
}
</script>
</body>
</html>
