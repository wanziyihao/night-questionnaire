[index.html](https://github.com/user-attachments/files/28174344/index.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>夜间情绪与陪伴需求调研</title>
<style>
/* ====== Reset & Variables ====== */
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#1a1625; --bg-card:#241e33; --bg-input:#2d2640;
  --text:#e8e0f0; --text-muted:#9a8fb8; --text-dim:#6b6085;
  --accent:#e8b85e; --accent-glow:#f0d080; --accent-dim:#8a6d35;
  --danger:#c06060; --border:#3a3250; --radius:12px; --radius-sm:8px;
  --font:"PingFang SC","Noto Sans SC","Microsoft YaHei",sans-serif;
}
html{font-size:16px}
body{
  font-family:var(--font); background:var(--bg); color:var(--text);
  min-height:100vh; line-height:1.7; -webkit-font-smoothing:antialiased;
  background-image:radial-gradient(ellipse at 50% 0%, #2a2240 0%, #1a1625 60%);
}

/* ====== Layout ====== */
.container{max-width:640px;margin:0 auto;padding:24px 20px 80px}

/* ====== Header ====== */
.header{text-align:center;padding:32px 0 20px}
.header .moon{font-size:40px;display:block;margin-bottom:8px}
.header h1{font-size:1.5rem;font-weight:600;color:var(--accent);letter-spacing:.02em;margin-bottom:4px}
.header .sub{font-size:.85rem;color:var(--text-muted)}

/* ====== Progress ====== */
.progress-wrap{padding:0 0 28px}
.progress-bar{
  height:3px;background:var(--border);border-radius:2px;overflow:hidden;margin-bottom:6px
}
.progress-fill{height:100%;background:var(--accent);border-radius:2px;transition:width .4s ease}
.progress-text{font-size:.75rem;color:var(--text-dim);text-align:right}

/* ====== Card ====== */
.card{background:var(--bg-card);border:1px solid var(--border);border-radius:var(--radius);padding:28px 24px}
@media(min-width:480px){.card{padding:32px 28px}}

/* ====== Part Title ====== */
.part-label{font-size:.7rem;text-transform:uppercase;letter-spacing:.12em;color:var(--accent-dim);margin-bottom:6px}
.part-title{font-size:1.15rem;font-weight:600;margin-bottom:6px}
.part-desc{font-size:.82rem;color:var(--text-muted);margin-bottom:24px;font-style:italic}

/* ====== Question Block ====== */
.q-block{margin-bottom:24px;padding-bottom:0}
.q-block:last-child{margin-bottom:0}
.q-label{display:block;font-size:.92rem;font-weight:500;margin-bottom:10px;line-height:1.6}
.q-num{color:var(--accent-dim);font-size:.78rem;margin-right:4px}
.req-mark{color:var(--danger);font-size:.72rem;font-weight:400;margin-left:2px}

/* ====== Inputs ====== */
textarea{
  width:100%;background:var(--bg-input);border:1px solid var(--border);border-radius:var(--radius-sm);
  color:var(--text);font-family:var(--font);font-size:.9rem;line-height:1.7;padding:12px 14px;
  resize:vertical;min-height:80px;transition:border-color .2s;outline:none
}
textarea:focus{border-color:var(--accent-dim)}
textarea::placeholder{color:var(--text-dim)}

input[type=text]{
  width:100%;background:var(--bg-input);border:1px solid var(--border);border-radius:var(--radius-sm);
  color:var(--text);font-family:var(--font);font-size:.9rem;padding:12px 14px;
  outline:none;transition:border-color .2s
}
input[type=text]:focus{border-color:var(--accent-dim)}
input[type=text]::placeholder{color:var(--text-dim)}

/* ====== Radio / Checkbox ====== */
.option-list{display:flex;flex-direction:column;gap:2px}
.option{
  display:flex;align-items:flex-start;gap:10px;padding:10px 12px;
  border-radius:var(--radius-sm);cursor:pointer;transition:background .15s;
  -webkit-tap-highlight-color:transparent;user-select:none
}
.option:hover,.option:active{background:rgba(255,255,255,.03)}
.option input[type=radio],.option input[type=checkbox]{
  appearance:none;-webkit-appearance:none;width:20px;height:20px;min-width:20px;
  border:2px solid var(--border);border-radius:50%;margin-top:1px;
  display:grid;place-items:center;cursor:pointer;transition:border-color .2s,background .2s
}
.option input[type=checkbox]{border-radius:4px}
.option input:checked{border-color:var(--accent);background:var(--accent)}
.option input[type=radio]::after{
  content:"";width:6px;height:6px;border-radius:50%;background:var(--bg);
  transform:scale(0);transition:transform .15s
}
.option input[type=radio]:checked::after{transform:scale(1)}
.option input[type=checkbox]::after{
  content:"";width:10px;height:6px;border-left:2px solid var(--bg);border-bottom:2px solid var(--bg);
  transform:rotate(-45deg) translateY(-1px);opacity:0;transition:opacity .15s
}
.option input[type=checkbox]:checked::after{opacity:1}
.option-text{font-size:.88rem}

/* Other input inline */
.option-inline{display:flex;align-items:center;gap:8px;padding:6px 12px 6px 42px}
.option-inline input[type=text]{
  flex:1;padding:8px 10px;font-size:.85rem;min-height:auto
}

/* ====== Conditional block ====== */
.conditional{margin-top:12px;margin-left:0;padding-left:0;display:none}
.conditional.open{display:block}

/* ====== Buttons ====== */
.btn-row{display:flex;gap:12px;margin-top:28px;justify-content:space-between}
.btn-row.no-prev{justify-content:flex-end}
.btn{
  display:inline-flex;align-items:center;justify-content:center;gap:6px;
  padding:12px 28px;border-radius:24px;font-size:.9rem;font-weight:500;
  cursor:pointer;border:none;transition:all .2s;font-family:var(--font);
  min-height:48px;-webkit-tap-highlight-color:transparent
}
.btn-primary{background:var(--accent);color:#1a1625}
.btn-primary:hover,.btn-primary:active{background:var(--accent-glow)}
.btn-secondary{background:transparent;color:var(--text-muted);border:1px solid var(--border)}
.btn-secondary:hover,.btn-secondary:active{color:var(--text);border-color:var(--text-dim)}
.btn:disabled{opacity:.4;pointer-events:none}

/* ====== Error hint ====== */
.error-hint{color:var(--danger);font-size:.78rem;margin-top:6px;display:none}

/* ====== Thank-you page ====== */
.thankyou{text-align:center;padding:48px 20px}
.thankyou .icon{font-size:48px;display:block;margin-bottom:16px}
.thankyou h2{font-size:1.3rem;color:var(--accent);margin-bottom:12px}
.thankyou p{color:var(--text-muted);font-size:.9rem;margin-bottom:8px;line-height:1.8}
.thankyou .summary{
  text-align:left;background:var(--bg-input);border-radius:var(--radius);
  padding:16px 18px;margin-top:20px;font-size:.82rem;color:var(--text-muted);
  max-height:300px;overflow-y:auto;line-height:1.8
}
.thankyou .summary span{color:var(--accent-dim)}
.thankyou .actions{margin-top:24px;display:flex;flex-direction:column;gap:10px;align-items:center}

/* ====== Admin panel ====== */
.admin-trigger{
  position:fixed;bottom:16px;right:16px;width:40px;height:40px;
  background:var(--bg-input);border:1px solid var(--border);border-radius:50%;
  display:flex;align-items:center;justify-content:center;cursor:pointer;
  font-size:16px;opacity:.3;transition:opacity .2s;z-index:100;
  -webkit-tap-highlight-color:transparent;
  padding:0;line-height:1
}
.admin-trigger:hover,.admin-trigger:active{opacity:.8}
.admin-panel{
  position:fixed;inset:0;background:rgba(0,0,0,.85);z-index:999;
  display:none;flex-direction:column;padding:20px;overflow-y:auto
}
.admin-panel.open{display:flex}
.admin-inner{max-width:600px;width:100%;margin:auto}
.admin-inner h3{color:var(--accent);margin-bottom:8px}
.admin-inner p{color:var(--text-muted);font-size:.8rem;margin-bottom:16px}
.admin-table-wrap{overflow-x:auto;margin-bottom:16px}
.admin-table{width:100%;border-collapse:collapse;font-size:.7rem}
.admin-table th,.admin-table td{
  border:1px solid var(--border);padding:6px 8px;text-align:left;
  white-space:nowrap;max-width:200px;overflow:hidden;text-overflow:ellipsis
}
.admin-table th{background:var(--bg-input);color:var(--accent-dim);position:sticky;top:0}
.admin-table td{color:var(--text-muted)}
.admin-actions{display:flex;gap:8px;flex-wrap:wrap}
.admin-close{
  position:absolute;top:16px;right:20px;font-size:24px;color:var(--text-muted);
  cursor:pointer;background:none;border:none;width:44px;height:44px
}

/* ====== Toast ====== */
.toast{
  position:fixed;bottom:24px;left:50%;transform:translateX(-50%) translateY(100px);
  background:var(--accent);color:#1a1625;padding:10px 20px;border-radius:20px;
  font-size:.82rem;font-weight:500;z-index:9999;transition:transform .3s ease;
  pointer-events:none
}
.toast.show{transform:translateX(-50%) translateY(0)}

/* ====== Section divider ====== */
.section-hint{
  text-align:center;padding:8px 0;color:var(--text-dim);font-size:.75rem;
  letter-spacing:.06em
}

/* ====== Responsive ====== */
@media(max-width:480px){
  .container{padding:16px 14px 48px}
  .header{padding:20px 0 14px}
  .header h1{font-size:1.25rem}
  .card{padding:20px 16px}
  .part-title{font-size:1.05rem}
  .q-label{font-size:.85rem}
  textarea{font-size:.85rem;min-height:72px;padding:10px 12px}
  .btn{padding:10px 20px;font-size:.85rem;min-height:44px}
  .option{padding:8px 10px}
  .option-text{font-size:.82rem}
}

@media(min-width:768px){
  .container{padding:32px 0 80px}
}

/* ====== Print ====== */
@media print{
  .btn-row,.progress-wrap,.admin-trigger,.toast{display:none!important}
  .card{border:none;break-inside:avoid}
  body{background:#fff;color:#000}
}
</style>
</head>
<body>

<div class="container" id="app">
  <!-- Header -->
  <div class="header">
    <span class="moon">🌙</span>
    <h1>夜间情绪与陪伴需求调研</h1>
    <p class="sub">一份关于夜晚独处真实体验的问卷</p>
  </div>

  <!-- Progress -->
  <div class="progress-wrap">
    <div class="progress-bar"><div class="progress-fill" id="progressFill"></div></div>
    <div class="progress-text" id="progressText">第 1 / 6 部分</div>
  </div>

  <!-- Form card -->
  <div class="card" id="formCard"></div>
</div>

<!-- Admin -->
<div class="admin-trigger" id="adminTrigger" title="数据管理">⚙</div>
<div class="admin-panel" id="adminPanel">
  <button class="admin-close" id="adminClose">&times;</button>
  <div class="admin-inner">
    <h3>答卷数据管理</h3>
    <p id="adminInfo">共 0 份答卷（数据仅保存在本浏览器中）</p>
    <div class="admin-table-wrap"><table class="admin-table" id="adminTable"></table></div>
    <div class="admin-actions">
      <button class="btn btn-primary" id="btnExportCSV">导出 CSV</button>
      <button class="btn btn-secondary" id="btnExportJSON">导出 JSON</button>
      <button class="btn btn-secondary" id="btnExportPrint">打印所有答卷</button>
      <button class="btn btn-secondary" id="btnClearData" style="color:var(--danger);border-color:var(--danger)">清空数据</button>
    </div>
  </div>
</div>

<!-- Toast -->
<div class="toast" id="toast"></div>

<script>
// ==================== QUESTIONNAIRE ENGINE ====================
const FORM = {
  parts: [
    {
      id:'p1', title:'第一部分：关于你', desc:'先认识一下你。几个简单的问题。',
      questions:[
        {id:'q1',type:'radio',label:'1. 你的年龄段是？',required:true,
         options:['18-22岁','23-26岁','27-30岁','30岁以上']},
        {id:'q2',type:'radio',label:'2. 你目前的居住状态是？',required:true,
         options:['一个人住','合租，但和室友不算很熟','合租，和室友关系亲近','和家人住在一起','和伴侣住在一起'],
         other:true},
        {id:'q3',type:'textarea',label:'3. 工作日的一天，你大概是怎么过的？用几句话描述一下就好。',required:false,
         placeholder:'比如：早上几点起、做什么工作/学什么、晚上一般几点回到家、睡前通常会干点什么。'},
        {id:'q4',type:'textarea',label:'4. 一天之中，哪个时段是你感觉最放松、最属于自己的时间？',required:false,
         placeholder:''}
      ]
    },
    {
      id:'p2', title:'第二部分：夜晚的你', desc:'这部分想了解你睡前那段独处时间的真实感受。没有标准答案，你的体验就是最重要的数据。',
      questions:[
        {id:'q5',type:'radio',label:'5. 在你一个人待着的时候——尤其是晚上——有没有过那种"特别想说点什么"或者"特别希望身边有个人"的时刻？',required:true,
         options:['经常有','偶尔有','很少有','几乎没有']},
        {id:'q6',type:'textarea',label:'6. 如果有的话，请回忆最近一次让你印象比较深的场景。那是怎样的一个晚上？几点钟？你在做什么？当时发生了什么？',required:false,
         placeholder:''},
        {id:'q7',type:'textarea',label:'7. 那个时刻，你心里是什么感觉？如果让你用自己的话来形容，它像什么？那一刻你最想做什么？',required:false,
         placeholder:''},
        {id:'q8',type:'textarea',label:'8. 准备睡觉那段时间，你脑子里通常会想些什么？有没有哪些念头会来回转，让你不容易静下来？',required:false,
         placeholder:''},
        {id:'q9',type:'checkbox',label:'9. 以下哪些描述比较接近你睡前的感觉？（可多选）',required:false,
         options:['脑子里很多事，停不下来','身体累了但脑子醒着','觉得心里空空的','莫名其妙有点难过','对第二天要做的事感到压力','翻来覆去就是睡不着','想找人说说话','刷手机刷到很晚，其实也不知道在看什么'],
         other:true}
      ]
    },
    {
      id:'p3', title:'第三部分：你通常会怎么做', desc:'面对那些不好受的时刻，每个人都有自己的习惯。我们希望了解你真实的做法，无论大小。',
      questions:[
        {id:'q10',type:'textarea',label:'10. 当上面说的那种感受出现时，你一般会做点什么？请把你通常会做的事都写下来，哪怕是很小的动作。',required:false,
         placeholder:'比如翻个身、拿起手机、点开某个App……'},
        {id:'q11',type:'textarea',label:'11. 如果你会尝试找人聊天——从拿起手机，到真正跟人说上话，这个过程通常是怎样的？中间都发生了什么？',required:false,
         placeholder:''},
        {id:'q12',type:'radio',label:'12. 有没有翻过通讯录、打了字、然后又删掉、最后没发出去的情况？',required:false,
         options:['经常这样','偶尔有过','几乎没有']},
        {id:'q13',type:'textarea',label:'13. 如果上一题你选了"经常"或"偶尔"——那时候，是什么让你决定"算了"？你心里闪过什么念头？',required:false,
         placeholder:''},
        {id:'q14',type:'textarea',label:'14. 除了找人聊天，你在睡前用过手机上的什么东西来帮自己度过那段时间吗？听歌、看视频、某个App、直播……都可以写下来。',required:false,
         placeholder:''},
        {id:'q15',type:'textarea',label:'15. 在这些方式里，有没有那么一个瞬间，让你觉得"嗯，这一刻其实还不错"？请描述一下那个瞬间——当时你在做什么？它在做什么？',required:false,
         placeholder:''},
        {id:'q16',type:'textarea',label:'16. 反过来，有没有让你觉得"用了之后反而更糟了"的经历？发生了什么？',required:false,
         placeholder:''},
        {id:'q17',type:'textarea',label:'17. 在深夜真的不太好受的时候——抛开所有现实限制，你心里最深处的渴望是什么？那个你可能平时不太跟人说的愿望。',required:false,
         placeholder:''},
        {id:'q18',type:'textarea',label:'18. 如果没有任何限制，你来设计一个能在那个时候陪着你的东西——你觉得它会是什么样子的？（它会做什么？一定不会做什么？）',required:false,
         placeholder:''}
      ]
    },
    {
      id:'p4', title:'第四部分：你心中理想的陪伴', desc:'接下来，请你发挥想象。不需要考虑技术能不能实现——只管你想要什么。',
      questions:[
        {id:'q19',type:'textarea',label:'19. 如果在你需要的时刻，有一个可以陪你说话的存在——你心里浮现出来的那个形象或者感觉，是什么样的？请描述一下。',required:false,
         placeholder:''},
        {id:'q20',type:'checkbox',label:'20. 你更喜欢用什么方式和它交流？（可多选）',required:false,
         options:['打字聊天','能听到它的声音，我用语音跟它说话','只能听到它的声音，我打字回应','能看到一个虚拟形象'],
         other:true},
        {id:'q21',type:'textarea',label:'21. 你觉得它什么时候出现会刚刚好，什么时候会让你觉得被打扰了？请举一个具体的例子。',required:false,
         placeholder:''},
        {id:'q22',type:'textarea',label:'22. 除了聊天本身，你还需要它为你做什么？有没有聊天之外的、能让你在睡前感觉更好的事情？',required:false,
         placeholder:''},
        {id:'q23',type:'textarea',label:'23. 你最怕这个东西做什么？它做了什么事，会让你觉得"算了，我不要了"？',required:false,
         placeholder:''}
      ]
    },
    {
      id:'p5', title:'第五部分：信任与选择', desc:'最后几个关于你如何看待这类服务的问题。',
      questions:[
        {id:'q24',type:'textarea',label:'24. 如果现在真的有这样一个东西——能做到你刚才说的那些——你会把它放在你生活中的什么位置？它对你来说更像一个什么？',required:false,
         placeholder:'比如：一个深夜可以说话的朋友、一个日记本、一个背景音、一个心理工具，或者其他任何你觉得像的东西。'},
        {id:'q25',type:'radio',label:'25. 关于这个陪伴服务背后——是谁在跟你互动，你会在意吗？',required:false,
         options:['很在意，我希望知道它背后是真人还是技术','有点在意，但体验好更重要','不太在意，只要它能帮到我','完全不在意']},
        {id:'q26',type:'textarea',label:'26. 如果它是AI而不是真人——你觉得这对你来说意味着什么？会让你的感受有什么不同吗？',required:false,
         placeholder:''},
        {id:'q27',type:'textarea',label:'27. 对于这样一个会知道你很多情绪和心事的东西，你最不放心的是什么？',required:false,
         placeholder:''}
      ]
    },
    {
      id:'p6', title:'第六部分：你用过这些吗', desc:'下面是一些市面上已有的产品类型。根据你的实际使用情况选填即可。没听过或没用过就跳过，完全没关系。',
      questions:[
        // A: 角色扮演
        {id:'q28',type:'radio',label:'28.【角色扮演类AI】你用过这类App吗？（如Character.AI、Glow、星野等——可以和角色聊天、编故事的那种）',required:false,
         options:['用过，现在还在用','用过，但是已经不用了','没用过，但听说过','完全没听过']},
        {id:'q29',type:'textarea',label:'29. 当你从故事或者对话里退出来，回到自己安静的房间里——退出那一刻，你心里是什么感觉？',required:false,
         placeholder:'', dependsOn:{q:'q28',not:['完全没听过']}},
        {id:'q30',type:'textarea',label:'30. 如果一个AI不扮演任何角色——就是一个普通的、愿意听你说话的存在——你觉得这种方式吸引你吗？和你用过的角色扮演相比，在哪种关系里你更可能说出你真正想说的话？为什么？',required:false,
         placeholder:'', dependsOn:{q:'q28',not:['完全没听过']}},
        // B: 疗愈
        {id:'q31',type:'radio',label:'31.【心理疗愈类App】你用过这类App吗？（如Woebot、林间聊愈室、简单心理等）',required:false,
         options:['用过，现在还在用','用过，但是已经不用了','没用过，但听说过','完全没听过']},
        {id:'q32',type:'textarea',label:'32. 当你带着一些情绪打开它时，你希望它最开始对你说什么？你希望那个互动的第一分钟是什么感觉？',required:false,
         placeholder:'', dependsOn:{q:'q31',not:['完全没听过']}},
        {id:'q33',type:'textarea',label:'33. 在你看来，"被治愈"或者"心情好起来"——那个转折点通常是怎么发生的？是某件事想通了，还是某种感觉变了，还是别的什么？',required:false,
         placeholder:'', dependsOn:{q:'q31',not:['完全没听过']}},
        // C: 伴侣
        {id:'q34',type:'radio',label:'34.【AI伴侣类】你用过这类App吗？（如Replika——可以建立亲密关系的AI）',required:false,
         options:['用过，现在还在用','用过，但是已经不用了','没用过，但听说过','完全没听过']},
        {id:'q35',type:'textarea',label:'35. 有些人跟AI聊着聊着，关系会变得有点像恋爱。你怎么看这个现象？如果放在你自己身上——你觉得那种关系对你晚上的状态会产生什么影响？',required:false,
         placeholder:'', dependsOn:{q:'q34',not:['完全没听过']}},
        {id:'q36',type:'textarea',label:'36. 如果一个陪伴服务从一开始就跟你把话说清楚——"我们就是朋友关系，不会往别的方向发展"——听到这个，你的第一反应是什么？',required:false,
         placeholder:''},
        // D: 声音
        {id:'q37',type:'radio',label:'37.【声音陪伴类】你在睡前听过这类内容吗？（如助眠白噪音、ASMR、冥想音频等）',required:false,
         options:['经常听','偶尔听','没听过']},
        {id:'q38',type:'textarea',label:'38. 那个声音对你来说，更像是一个"陪伴"，还是更像一个"背景"？如果它突然叫了你的名字，你会是什么反应？',required:false,
         placeholder:'', dependsOn:{q:'q37',not:['没听过']}},
        {id:'q39',type:'textarea',label:'39. 如果那个声音不只是自己在那说，而是真的能听到你说话、回应你——你觉得那会是什么感觉？你会想跟它说什么吗？',required:false,
         placeholder:''},
        // E: 总结
        {id:'q40',type:'textarea',label:'40. 聊了这么多不同的体验——回头想想，在你感觉最被安慰到的那些时刻里，让你真的变好了一点的，到底是什么？',required:false,
         placeholder:''}
      ]
    }
  ],
  totalParts:6
};

// ==================== STORAGE ENGINE ====================
const STORAGE_KEY_DRAFT = 'ntq_draft';
const STORAGE_KEY_SUBMISSIONS = 'ntq_submissions';
const SESSION_KEY_SUBMITTED = 'ntq_submitted';
const EMAILJS_SERVICE = 'service_qjlqb5l';
const EMAILJS_TEMPLATE = 'template_jmkj6ht';
const EMAILJS_PUBLIC = '36Am8Bmx2V9rdwi8a';
const TOAST_DURATION = 2000;

function saveDraft(data){localStorage.setItem(STORAGE_KEY_DRAFT,JSON.stringify(data))}
function loadDraft(){try{const d=localStorage.getItem(STORAGE_KEY_DRAFT);return d?JSON.parse(d):null}catch(e){return null}}
function clearDraft(){localStorage.removeItem(STORAGE_KEY_DRAFT)}

function saveSubmission(data){
  const subs=loadSubmissions(); subs.push({...data,submittedAt:new Date().toISOString(),id:Date.now().toString(36)+Math.random().toString(36).slice(2,6)});
  localStorage.setItem(STORAGE_KEY_SUBMISSIONS,JSON.stringify(subs)); return subs.length;
}
function loadSubmissions(){try{const d=localStorage.getItem(STORAGE_KEY_SUBMISSIONS);return d?JSON.parse(d):[]}catch(e){return []}}
function clearSubmissions(){localStorage.removeItem(STORAGE_KEY_SUBMISSIONS)}

// ==================== STATE ====================
let state={
  currentPart:0,
  answers:{},
  submitted:false
};

const draft=loadDraft();
if(draft){state.answers=draft.answers||{};state.currentPart=Math.min(draft.currentPart||0,FORM.totalParts-1)}
if(sessionStorage.getItem(SESSION_KEY_SUBMITTED)){state.submitted=true}

// ==================== RENDER ====================
const $card=document.getElementById('formCard');
const $progressFill=document.getElementById('progressFill');
const $progressText=document.getElementById('progressText');
const $toast=document.getElementById('toast');

if(draft&&!state.submitted){
  setTimeout(()=>showToast('已恢复上次的填写进度'),500);
}

function showToast(msg){
  $toast.textContent=msg; $toast.classList.add('show');
  clearTimeout($toast._t); $toast._t=setTimeout(()=>$toast.classList.remove('show'),TOAST_DURATION);
}

function updateProgress(){
  const pct=Math.round(((state.currentPart+1)/FORM.totalParts)*100);
  $progressFill.style.width=pct+'%';
  $progressText.textContent=`第 ${state.currentPart+1} / ${FORM.totalParts} 部分`;
}

function getAnswer(qid){
  return state.answers[qid]!==undefined?state.answers[qid]:null;
}

function setAnswer(qid,val){
  if(val===null||val===undefined||val===''||(Array.isArray(val)&&val.length===0)){delete state.answers[qid]}
  else{state.answers[qid]=val}
}

function isAnswered(val){
  return val!==null&&val!==undefined&&val!==''&&!(Array.isArray(val)&&val.length===0);
}

function getAllQuestionKeys(){
  const keys=['id','submittedAt'];
  FORM.parts.forEach(p=>p.questions.forEach(q=>{if(!keys.includes(q.id))keys.push(q.id)}));
  return keys;
}

function isQuestionVisible(q){
  if(!q.dependsOn)return true;
  const dv=getAnswer(q.dependsOn.q);
  if(dv===null)return false;
  if(q.dependsOn.not&&q.dependsOn.not.includes(dv))return false;
  return true;
}

function renderPart(idx,keepScroll){
  const part=FORM.parts[idx];
  let html='';
  html+=`<div class="part-label">第 ${idx+1} 部分</div>`;
  html+=`<div class="part-title">${part.title}</div>`;
  html+=`<div class="part-desc">${part.desc}</div>`;

  part.questions.forEach(q=>{
    if(!isQuestionVisible(q))return;
    const reqMark=q.required?' <span class="req-mark">(必填)</span>':'';
    html+=`<div class="q-block" data-qid="${q.id}">`;
    html+=`<label class="q-label"><span class="q-num">Q</span>${q.label}${reqMark}</label>`;

    const val=getAnswer(q.id);

    if(q.type==='radio'){
      html+=`<div class="option-list">`;
      q.options.forEach((opt,i)=>{
        const checked=(val===opt)?' checked':'';
        html+=`<label class="option"><input type="radio" name="${q.id}" value="${escapeHtml(opt)}"${checked} data-qid="${q.id}"><span class="option-text">${opt}</span></label>`;
      });
      if(q.other){
        const otherVal=(val&&!q.options.includes(val))?val:'';
        html+=`<div class="option-inline"><input type="text" name="${q.id}_other" value="${escapeHtml(otherVal)}" placeholder="其他，请填写…" data-qid="${q.id}" data-other="true"></div>`;
      }
      html+=`</div>`;
      html+=`<div class="error-hint" id="err-${q.id}">请选择一个选项</div>`;
    }

    if(q.type==='checkbox'){
      const selected=Array.isArray(val)?val:[];
      html+=`<div class="option-list">`;
      q.options.forEach(opt=>{
        const checked=selected.includes(opt)?' checked':'';
        html+=`<label class="option"><input type="checkbox" name="${q.id}" value="${escapeHtml(opt)}"${checked} data-qid="${q.id}"><span class="option-text">${opt}</span></label>`;
      });
      if(q.other){
        const otherVal=selected.find(v=>!q.options.includes(v))||'';
        html+=`<div class="option-inline"><input type="text" name="${q.id}_other" value="${escapeHtml(otherVal)}" placeholder="其他，请填写…" data-qid="${q.id}" data-other="true"></div>`;
      }
      html+=`</div>`;
    }

    if(q.type==='textarea'){
      html+=`<textarea name="${q.id}" placeholder="${q.placeholder||''}" data-qid="${q.id}">${val||''}</textarea>`;
    }

    html+=`</div>`;
  });

  // Nav buttons
  html+=`<div class="btn-row${idx===0?' no-prev':''}">`;
  if(idx>0){html+=`<button class="btn btn-secondary" id="btnPrev">← 上一部分</button>`}
  if(idx<FORM.totalParts-1){
    html+=`<button class="btn btn-primary" id="btnNext">下一部分 →</button>`;
  }else{
    html+=`<button class="btn btn-primary" id="btnSubmit">提交问卷 ✨</button>`;
  }
  html+=`</div>`;

  $card.innerHTML=html;
  updateProgress();

  // Bind radio/checkbox change
  $card.querySelectorAll('input[type=radio]').forEach(el=>{
    el.addEventListener('change',function(){
      setAnswer(this.dataset.qid,this.value);
      // Clear other input for this question when radio changes
      const otherInput=$card.querySelector(`input[name="${this.dataset.qid}_other"]`);
      if(otherInput)otherInput.value='';
      saveCurrentDraft();
      refreshConditional();
    });
  });

  $card.querySelectorAll('input[type=checkbox]').forEach(el=>{
    el.addEventListener('change',function(){
      const qid=this.dataset.qid;
      const checked=$card.querySelectorAll(`input[type=checkbox][data-qid="${qid}"]:checked`);
      const vals=Array.from(checked).map(c=>c.value);
      // Also include the "other" text if present
      const otherInput=$card.querySelector(`input[name="${qid}_other"]`);
      if(otherInput&&otherInput.value.trim()){
        vals.push(otherInput.value.trim());
      }
      setAnswer(qid,vals);
      saveCurrentDraft();
      refreshConditional();
    });
  });

  // Bind "other" text inputs
  $card.querySelectorAll('input[type=text][data-other="true"]').forEach(el=>{
    el.addEventListener('input',function(){
      const qid=this.dataset.qid;
      const q=part.questions.find(qq=>qq.id===qid);
      if(q&&q.type==='radio'){
        // Uncheck any selected radio — "other" is mutually exclusive
        const checkedRadio=$card.querySelector(`input[type=radio][name="${qid}"]:checked`);
        if(checkedRadio)checkedRadio.checked=false;
        setAnswer(qid,this.value.trim()||null);
      }
      if(q&&q.type==='checkbox'){
        const checked=$card.querySelectorAll(`input[type=checkbox][data-qid="${qid}"]:checked`);
        const vals=Array.from(checked).map(c=>c.value);
        if(this.value.trim())vals.push(this.value.trim());
        setAnswer(qid,vals.length?vals:null);
      }
      saveCurrentDraft();
    });
    // Also handle focus — uncheck radio when user focuses the "other" field
    el.addEventListener('focus',function(){
      const qid=this.dataset.qid;
      const q=part.questions.find(qq=>qq.id===qid);
      if(q&&q.type==='radio'){
        const checkedRadio=$card.querySelector(`input[type=radio][name="${qid}"]:checked`);
        if(checkedRadio)checkedRadio.checked=false;
      }
    });
  });

  // Bind textarea (debounced save to localStorage)
  let _debounceTimer=null;
  $card.querySelectorAll('textarea').forEach(el=>{
    el.addEventListener('input',function(){
      setAnswer(this.dataset.qid,this.value||null);
      clearTimeout(_debounceTimer);
      _debounceTimer=setTimeout(saveCurrentDraft,500);
    });
  });

  // Bind buttons
  const btnPrev=$card.querySelector('#btnPrev');
  const btnNext=$card.querySelector('#btnNext');
  const btnSubmit=$card.querySelector('#btnSubmit');

  if(btnPrev)btnPrev.addEventListener('click',()=>{navigatePart(idx-1)});
  if(btnNext)btnNext.addEventListener('click',()=>{
    if(validatePart(idx)){navigatePart(idx+1)}
  });
  if(btnSubmit)btnSubmit.addEventListener('click',function(){
    if(this.disabled)return;
    this.disabled=true;
    this.textContent='提交中…';
    if(validateAll()&&validatePart(idx)){submitForm()}
    else{this.disabled=false;this.textContent='提交问卷 ✨';}
  });

  // Scroll to top (skip when refreshing conditionals to avoid jarring jumps)
  if(!keepScroll)window.scrollTo({top:0,behavior:'smooth'});
}

function refreshConditional(){
  const part=FORM.parts[state.currentPart];
  const hasConditional=part.questions.some(q=>q.dependsOn);
  if(!hasConditional)return;
  // Clear answers for questions that are now hidden
  part.questions.forEach(q=>{
    if(!isQuestionVisible(q)&&getAnswer(q.id)!==null){
      setAnswer(q.id,null);
    }
  });
  renderPart(state.currentPart,true);
}

function validatePart(idx){
  const part=FORM.parts[idx];
  let valid=true;
  part.questions.forEach(q=>{
    if(!q.required||!isQuestionVisible(q))return;
    if(!isAnswered(getAnswer(q.id))){
      valid=false;
      const errEl=document.getElementById('err-'+q.id);
      if(errEl)errEl.style.display='block';
    }
  });
  if(!valid){showToast('请先完成必填问题（已标注"必填"）')}
  return valid;
}

function validateAll(){
  let firstMissing=null;
  FORM.parts.forEach((part,pi)=>{
    part.questions.forEach(q=>{
      if(!q.required||!isQuestionVisible(q))return;
      if(!isAnswered(getAnswer(q.id))&&!firstMissing){firstMissing=pi}
    });
  });
  if(firstMissing!==null){
    if(state.currentPart!==firstMissing){navigatePart(firstMissing)}
    showToast('请先完成所有必填问题（已标注"必填"）');
    return false;
  }
  return true;
}

function navigatePart(idx){
  state.currentPart=idx;
  saveCurrentDraft();
  renderPart(idx);
  window.scrollTo({top:0,behavior:'smooth'});
}

function saveCurrentDraft(){
  saveDraft({answers:state.answers,currentPart:state.currentPart});
}

function submitForm(){
  // Final DOM scan as safety net for last-focused input
  $card.querySelectorAll('textarea').forEach(el=>{setAnswer(el.dataset.qid,el.value||null)});
  const count=saveSubmission(state.answers);
  clearDraft();
  state.submitted=true;
  sessionStorage.setItem(SESSION_KEY_SUBMITTED,'1');
  sendEmail(state.answers,count);
  renderThankYou();
  window.scrollTo({top:0,behavior:'smooth'});
  showToast(`已收到第 ${count} 份答卷，谢谢你`);
}

function renderThankYou(){
  updateProgress();
  $progressFill.style.width='100%';
  $progressText.textContent='已完成';

  // Build summary
  let summaryHtml='';
  FORM.parts.forEach(part=>{
    summaryHtml+=`<p><span>—— ${part.title} ——</span></p>`;
    part.questions.forEach(q=>{
      const val=state.answers[q.id];
      if(val===null||val===undefined)return;
      const displayVal=Array.isArray(val)?val.join('、'):val;
      summaryHtml+=`<p><span>${q.label.split('. ')[0]}.</span> ${escapeHtml(displayVal)}</p>`;
    });
  });

  $card.innerHTML=`
    <div class="thankyou">
      <span class="icon">🕯️</span>
      <h2>问卷已完成</h2>
      <p>谢谢你花了这么多时间，把心里的话写下来。<br>这对我非常有帮助。</p>
      <p style="font-size:.82rem;color:var(--text-dim)">你的回答已保存在本浏览器中，不会上传到任何服务器。</p>
      <div class="summary">${summaryHtml}</div>
      <p style="font-size:.82rem;color:var(--text-dim);margin-top:16px">如果身边有朋友晚上也有类似感受，欢迎转发这份问卷。</p>
      <div class="actions">
        <button class="btn btn-secondary" id="btnRetake">再填一份</button>
      </div>
    </div>`;

  document.getElementById('btnRetake').addEventListener('click',()=>{
    sessionStorage.removeItem(SESSION_KEY_SUBMITTED);
    clearDraft();
    state={currentPart:0,answers:{},submitted:false};
    renderPart(0);
    window.scrollTo({top:0,behavior:'smooth'});
    showToast('可以重新填写了');
  });
}

// ==================== EMAILJS ====================
function buildEmailBody(answers,count){
  const time=new Date().toLocaleString('zh-CN',{timeZone:'Asia/Shanghai'});
  let text=`🌙 新答卷 #${count}  |  ${time}\n`;
  text+=`━━━━━━━━━━━━━━━━\n`;
  FORM.parts.forEach(part=>{
    text+=`\n📌 ${part.title}\n`;
    part.questions.forEach(q=>{
      const val=answers[q.id];
      if(val===null||val===undefined||val==='')return;
      const display=Array.isArray(val)?val.join('、'):val;
      const label=q.label.replace(/^\d+\.\s*/,'');
      text+=`  · ${label}：${display}\n`;
    });
  });
  text+=`\n━━━━━━━━━━━━━━━━`;
  return text;
}

async function sendEmail(answers,count){
  try{
    const resp=await fetch('https://api.emailjs.com/api/v1.0/email/send',{
      method:'POST',
      headers:{'Content-Type':'application/json'},
      body:JSON.stringify({
        service_id:EMAILJS_SERVICE,
        template_id:EMAILJS_TEMPLATE,
        user_id:EMAILJS_PUBLIC,
        template_params:{message:buildEmailBody(answers,count)}
      })
    });
    if(!resp.ok){console.error('EmailJS failed:',resp.status)}
  }catch(e){
    console.error('EmailJS error:',e);
    showToast('⚠ 邮件发送失败，但数据已保存在本地管理面板中');
  }
}

// ==================== ADMIN PANEL ====================
function renderAdminPanel(){
  const subs=loadSubmissions();
  document.getElementById('adminInfo').textContent=`共 ${subs.length} 份答卷（数据仅保存在本浏览器中）`;

  if(subs.length===0){
    document.getElementById('adminTable').innerHTML='<tr><td style="text-align:center;padding:20px;color:var(--text-dim)">暂无答卷</td></tr>';
    return;
  }

  const allKeys=getAllQuestionKeys();

  let thead='<tr><th>#</th>';
  allKeys.forEach(k=>{thead+=`<th>${k}</th>`});
  thead+='</tr>';

  let tbody='';
  subs.forEach((sub,i)=>{
    tbody+=`<tr><td>${i+1}</td>`;
    allKeys.forEach(k=>{
      let v=sub[k]||'';
      if(Array.isArray(v))v=v.join('、');
      v=String(v).slice(0,150);
      tbody+=`<td>${escapeHtml(v)}</td>`;
    });
    tbody+='</tr>';
  });

  document.getElementById('adminTable').innerHTML=thead+tbody;
}

function exportCSV(){
  const subs=loadSubmissions();
  if(subs.length===0){showToast('暂无数据可导出');return}

  const allKeys=getAllQuestionKeys();

  const header=allKeys.join(',');
  const rows=subs.map(sub=>{
    return allKeys.map(k=>{
      let v=sub[k]||'';
      if(Array.isArray(v))v=v.join('、');
      v=String(v).replace(/"/g,'""');
      return `"${v}"`;
    }).join(',');
  });

  const csv='﻿'+header+'\n'+rows.join('\n');
  downloadFile(csv,'夜间情绪调研_答卷.csv','text/csv;charset=utf-8');
}

function exportJSON(){
  const subs=loadSubmissions();
  if(subs.length===0){showToast('暂无数据可导出');return}
  const json=JSON.stringify(subs,null,2);
  downloadFile(json,'夜间情绪调研_答卷.json','application/json');
}

function exportPrint(){
  const subs=loadSubmissions();
  if(subs.length===0){showToast('暂无数据可打印');return}
  let html='<!DOCTYPE html><html><head><meta charset="UTF-8"><title>答卷打印</title><style>body{font-family:sans-serif;line-height:1.8;max-width:800px;margin:auto;padding:20px}h2{page-break-before:always;color:#333}h3{color:#555}td{padding:4px 8px;vertical-align:top}</style></head><body>';
  subs.forEach((sub,i)=>{
    html+=`<h2>答卷 #${i+1}</h2><p>提交时间：${sub.submittedAt||''}</p>`;
    FORM.parts.forEach(part=>{
      html+=`<h3>${part.title}</h3><table>`;
      part.questions.forEach(q=>{
        const v=sub[q.id];
        if(v===undefined||v===null||v==='')return;
        html+=`<tr><td><strong>${q.label}</strong></td><td>${escapeHtml(Array.isArray(v)?v.join('、'):v)}</td></tr>`;
      });
      html+=`</table>`;
    });
  });
  html+='</body></html>';
  const w=window.open('','_blank','width=800,height=600');
  w.document.write(html); w.document.close();
}

function downloadFile(content,filename,mime){
  const blob=new Blob([content],{type:mime});
  const url=URL.createObjectURL(blob);
  const a=document.createElement('a'); a.href=url;a.download=filename;
  document.body.appendChild(a);a.click();
  document.body.removeChild(a);URL.revokeObjectURL(url);
}

// Admin panel bindings
document.getElementById('adminTrigger').addEventListener('click',()=>{
  renderAdminPanel();
  document.getElementById('adminPanel').classList.add('open');
});
document.getElementById('adminClose').addEventListener('click',()=>{
  document.getElementById('adminPanel').classList.remove('open');
});
document.getElementById('adminPanel').addEventListener('click',function(e){
  if(e.target===this)this.classList.remove('open');
});
document.getElementById('btnExportCSV').addEventListener('click',exportCSV);
document.getElementById('btnExportJSON').addEventListener('click',exportJSON);
document.getElementById('btnExportPrint').addEventListener('click',exportPrint);
document.getElementById('btnClearData').addEventListener('click',()=>{
  if(confirm('确定要清空所有答卷数据吗？此操作不可恢复。')){
    clearSubmissions();
    renderAdminPanel();
    showToast('数据已清空');
  }
});

// ==================== UTILS ====================
const _escDiv=document.createElement('div');
function escapeHtml(str){_escDiv.textContent=str;return _escDiv.innerHTML}

// ==================== INIT ====================
function init(){
  if(state.submitted){
    renderThankYou();
  }else{
    renderPart(state.currentPart);
  }
}

init();
</script>
</body>
</html>
