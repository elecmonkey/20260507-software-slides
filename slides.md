---
theme: seriph
title: 电商订单故障排查知识图谱设计
highlighter: shiki
lineNumbers: false
transition: slide-left
aspectRatio: 16/9
canvasWidth: 980
fonts:
  sans: Noto Sans SC, sans-serif
  mono: Fira Code
drawings:
  enabled: false
mermaid:
  theme: base
  themeVariables:
    primaryColor: '#f8fafc'
    primaryTextColor: '#0f172a'
    primaryBorderColor: '#94a3b8'
    lineColor: '#64748b'
    secondaryColor: '#eef6ff'
    tertiaryColor: '#ffffff'
    clusterBkg: '#f8fafc'
    clusterBorder: '#cbd5e1'
    edgeLabelBackground: '#ffffff'
background: https://cover.sli.dev
---

<style>
:root {
  --kg-ink: #0f172a;
  --kg-muted: #64748b;
  --kg-line: #bcccdc;
  --kg-card: rgba(226, 235, 247, 0.94);
  --kg-soft: rgba(214, 226, 242, 0.9);
  --kg-primary: #2563eb;
  --kg-primary-dark: #1e3a8a;
  --kg-cyan: #0891b2;
}

.slidev-layout {
  background:
    linear-gradient(135deg, rgba(248, 250, 252, 0.97), rgba(236, 246, 255, 0.98)),
    radial-gradient(circle at 85% 12%, rgba(37, 99, 235, 0.12), transparent 30%);
  color: var(--kg-ink);
}

.slidev-layout h1 {
  color: var(--kg-ink);
  font-weight: 800;
  letter-spacing: 0;
}

.slidev-layout h2 {
  color: var(--kg-ink) !important;
  font-weight: 800;
  letter-spacing: 0;
  position: relative;
  padding-bottom: 0.35rem;
}

.slidev-layout h2::after {
  content: "";
  position: absolute;
  left: 0;
  bottom: 0;
  width: 4.8rem;
  height: 3px;
  border-radius: 999px;
  background: linear-gradient(90deg, var(--kg-primary), var(--kg-cyan));
}

.slidev-layout p,
.slidev-layout .text-slate-500,
.slidev-layout .text-slate-400 {
  color: var(--kg-muted) !important;
}

.slidev-layout .rounded-xl,
.slidev-layout .rounded-lg,
.slidev-layout .rounded-md {
  border-radius: 10px !important;
}

.slidev-layout .rounded-full {
  box-shadow: none;
}

.slidev-layout [class*="bg-orange-50"],
.slidev-layout [class*="bg-red-50"],
.slidev-layout [class*="bg-yellow-50"],
.slidev-layout [class*="bg-green-50"],
.slidev-layout [class*="bg-emerald-50"],
.slidev-layout [class*="bg-violet-50"],
.slidev-layout [class*="bg-blue-50"],
.slidev-layout .bg-slate-50,
.slidev-layout .bg-slate-100 {
  background-color: var(--kg-soft) !important;
}

.slidev-layout [class*="border-orange-"],
.slidev-layout [class*="border-red-"],
.slidev-layout [class*="border-yellow-"],
.slidev-layout [class*="border-green-"],
.slidev-layout [class*="border-emerald-"],
.slidev-layout [class*="border-violet-"],
.slidev-layout [class*="border-blue-"],
.slidev-layout .border-slate-100,
.slidev-layout .border-slate-200 {
  border-color: var(--kg-line) !important;
}

.slidev-layout [class*="text-orange-"],
.slidev-layout [class*="text-red-"],
.slidev-layout [class*="text-yellow-"],
.slidev-layout [class*="text-green-"],
.slidev-layout [class*="text-emerald-"],
.slidev-layout [class*="text-violet-"],
.slidev-layout [class*="text-blue-"] {
  color: var(--kg-primary-dark) !important;
}

.slidev-layout [class*="bg-orange-500"],
.slidev-layout [class*="bg-red-500"],
.slidev-layout [class*="bg-yellow-500"],
.slidev-layout [class*="bg-green-500"],
.slidev-layout [class*="bg-blue-500"],
.slidev-layout .bg-blue-600,
.slidev-layout .bg-cyan-500 {
  background: linear-gradient(135deg, var(--kg-primary), var(--kg-cyan)) !important;
}

.slidev-layout .bg-white,
.slidev-layout [class*="bg-white/"] {
  background-color: var(--kg-card) !important;
}

.slidev-layout .bg-slate-50,
.slidev-layout .bg-slate-100,
.slidev-layout [class*="bg-slate-50/"],
.slidev-layout [class*="bg-slate-100/"] {
  background-color: #d8e3f0 !important;
}

.slidev-layout .shadow-lg,
.slidev-layout img,
.slidev-layout .mermaid {
  box-shadow: 0 12px 32px rgba(15, 23, 42, 0.08) !important;
}

.slidev-layout .mermaid {
  background: rgba(226, 235, 247, 0.9);
  border: 1px solid var(--kg-line);
  border-radius: 12px;
  padding: 0.45rem;
}

.slidev-layout .mermaid svg [fill="#ECECFF"],
.slidev-layout .mermaid svg [fill="#ffffde"],
.slidev-layout .mermaid svg [fill="#f9f"],
.slidev-layout .mermaid svg [fill="#ccf"],
.slidev-layout .mermaid svg [fill="#ccffcc"] {
  fill: #e2ebf7 !important;
}

.slidev-layout .mermaid svg .node rect,
.slidev-layout .mermaid svg .node circle,
.slidev-layout .mermaid svg .node ellipse,
.slidev-layout .mermaid svg .node polygon,
.slidev-layout .mermaid svg .mindmap-node rect,
.slidev-layout .mermaid svg .mindmap-node circle {
  fill: #e2ebf7 !important;
  stroke: #94a3b8 !important;
}

.slidev-layout .mermaid svg .edgePath path,
.slidev-layout .mermaid svg .flowchart-link,
.slidev-layout .mermaid svg .edge-thickness-normal {
  stroke: #64748b !important;
}

.slidev-layout .mermaid svg text {
  fill: #0f172a !important;
}

.slidev-layout img {
  border: 1px solid var(--kg-line);
  background: white;
}

code {
  color: var(--kg-primary-dark);
  background: rgba(219, 234, 254, 0.8) !important;
}
</style>

<!-- ===== Page 1: Cover ===== -->

<div class="text-center">

<div class="text-white-500 text-xs tracking-widest uppercase mb-2">Knowledge Graph for E-Commerce Troubleshooting</div>

# 电商订单故障排查知识图谱

---
layout: default
background: false
---

<!-- ===== Page 2: 项目背景与痛点 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">项目背景：电商订单排障为什么困难？</h2>
<p class="text-slate-500 text-sm mb-4">订单故障往往跨越业务链路、系统模块和维护数据，单靠日志或经验很难快速定位。</p>

<div class="grid grid-cols-[1.05fr_0.95fr] gap-4 h-[70%]">

<div class="rounded-xl border border-slate-200 bg-white/85 p-4 flex flex-col">
  <div class="text-sm font-bold text-slate-800 mb-3">电商系统的复杂性</div>
  <div class="grid grid-cols-2 gap-2 text-xs">
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-3 py-2">
      <div class="font-bold text-slate-800 mb-1">链路长</div>
      <div class="text-slate-500 leading-snug">下单、支付、库存、物流、售后连续协作。</div>
    </div>
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-3 py-2">
      <div class="font-bold text-slate-800 mb-1">模块多</div>
      <div class="text-slate-500 leading-snug">订单模块与支付、库存、优惠等模块强耦合。</div>
    </div>
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-3 py-2">
      <div class="font-bold text-slate-800 mb-1">数据散</div>
      <div class="text-slate-500 leading-snug">Git、Issue、日志、API 文档分散存放。</div>
    </div>
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-3 py-2">
      <div class="font-bold text-slate-800 mb-1">变更多</div>
      <div class="text-slate-500 leading-snug">接口、代码文件和日志格式随版本持续变化。</div>
    </div>
  </div>

  <div class="mt-4 rounded-lg border border-slate-200 bg-slate-50 px-3 py-2 text-xs text-slate-600">
    典型问题：支付单已支付但订单仍未支付、库存扣减失败、订单与物流或售后状态不同步。
  </div>
</div>

<div class="rounded-xl border border-slate-200 bg-white/85 p-4 flex flex-col">
  <div class="text-sm font-bold text-slate-800 mb-3">知识图谱解决的痛点</div>
  <div class="flex flex-col gap-2 text-xs">
    <div class="flex gap-2 rounded-lg border border-slate-200 bg-slate-50 px-3 py-2">
      <div class="w-6 h-6 rounded-full bg-slate-700 text-white flex items-center justify-center shrink-0">1</div>
      <div><b class="text-slate-800">把分散信息关联起来</b><br/><span class="text-slate-500">Commit、Bug、LogEvent、TraceId、API 和测试用例进入同一张图。</span></div>
    </div>
    <div class="flex gap-2 rounded-lg border border-slate-200 bg-slate-50 px-3 py-2">
      <div class="w-6 h-6 rounded-full bg-slate-700 text-white flex items-center justify-center shrink-0">2</div>
      <div><b class="text-slate-800">把排查过程路径化</b><br/><span class="text-slate-500">从异常日志、订单、模块或 Commit 出发，沿关系路径定位影响范围。</span></div>
    </div>
    <div class="flex gap-2 rounded-lg border border-slate-200 bg-slate-50 px-3 py-2">
      <div class="w-6 h-6 rounded-full bg-slate-700 text-white flex items-center justify-center shrink-0">3</div>
      <div><b class="text-slate-800">把维护决策自动化</b><br/><span class="text-slate-500">支持故障定位、影响分析、Bug 统计和回归测试范围判断。</span></div>
    </div>
  </div>
</div>

</div>

---
layout: default
background: false
---

<!-- ===== Page 2: 多源数据汇入全景 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">多源数据汇入知识图谱</h2>
<p class="text-slate-500 text-sm mb-4">Git · Issue · 日志 · API 文档 —— 四种数据源融合为统一故障排查视图</p>

```mermaid {scale: 0.75}
flowchart LR
    Git[Git 提交记录] --> GitExtract[Commit / 文件修改 / 模块变更]
    Issue[Issue / Bug] --> IssueExtract[Bug 描述 / 影响模块 / 修复人员]
    Log[运行日志] --> LogExtract[LogEvent / 异常类型 / TraceId]
    API[API 文档] --> APIExtract[接口 / 模块映射 / 测试用例]

    GitExtract --> KG[电商订单故障排查知识图谱]
    IssueExtract --> KG
    LogExtract --> KG
    APIExtract --> KG

    KG --> Q1[影响分析]
    KG --> Q2[故障定位]
    KG --> Q3[Bug 统计]
    KG --> Q4[回归测试范围]
```

<div class="grid grid-cols-4 gap-2 mt-2 text-xs">
  <div class="rounded-lg border border-slate-200 bg-white/80 p-2"><b class="text-slate-700">Git</b><br/>追踪提交、文件与模块影响</div>
  <div class="rounded-lg border border-slate-200 bg-white/80 p-2"><b class="text-slate-700">Issue</b><br/>抽取 Bug 描述与修复信息</div>
  <div class="rounded-lg border border-slate-200 bg-white/80 p-2"><b class="text-slate-700">日志</b><br/>通过 TraceId 连接异常与订单</div>
  <div class="rounded-lg border border-slate-200 bg-white/80 p-2"><b class="text-slate-700">API</b><br/>建立接口、模块和测试映射</div>
</div>

<div class="mt-2 rounded-lg border border-slate-200 bg-slate-50 px-3 py-1.5 text-xs text-slate-500">
  统一查询入口：围绕一个模块、订单、Bug 或 Commit，快速追踪相关业务、代码、日志和测试范围。
</div>

---
layout: default
background: false
---

<!-- ===== Page 3: 实体分类卡片 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">实体分类设计</h2>
<p class="text-slate-500 text-sm mb-5">5 大类 · 20+ 实体 · 覆盖业务链路与维护链路</p>

<div class="flex gap-3 h-[62%]">

<div class="flex-1 rounded-xl p-3 bg-white/80 border border-slate-200 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-slate-100 flex items-center justify-center text-sm">📦</div>
    <div>
      <div class="font-bold text-sm text-slate-800">业务实体</div>
      <div class="text-xs text-slate-400">8 个</div>
    </div>
  </div>
  <div class="flex flex-wrap gap-1">
    <span v-for="e in ['用户','订单','商品','SKU','支付单','物流单','库存记录','售后单']" class="px-1.5 py-0.5 rounded-md text-xs bg-white border border-slate-200 text-slate-700">{{ e }}</span>
  </div>
</div>

<div class="flex-1 rounded-xl p-3 bg-white/80 border border-slate-200 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-slate-100 flex items-center justify-center text-sm">⚙️</div>
    <div>
      <div class="font-bold text-sm text-slate-800">系统模块</div>
      <div class="text-xs text-slate-400">6 个</div>
    </div>
  </div>
  <div class="flex flex-wrap gap-1">
    <span v-for="e in ['订单模块','支付模块','库存模块','物流模块','售后模块','优惠模块']" class="px-1.5 py-0.5 rounded-md text-xs bg-white border border-slate-200 text-slate-700">{{ e }}</span>
  </div>
</div>

<div class="flex-1 rounded-xl p-3 bg-white/80 border border-slate-200 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-slate-100 flex items-center justify-center text-sm">📝</div>
    <div>
      <div class="font-bold text-sm text-slate-800">代码变更</div>
      <div class="text-xs text-slate-400">4 个</div>
    </div>
  </div>
  <div class="flex flex-wrap gap-1">
    <span v-for="e in ['Git Commit','代码文件','API 接口','测试用例']" class="px-1.5 py-0.5 rounded-md text-xs bg-white border border-slate-200 text-slate-700">{{ e }}</span>
  </div>
</div>

<div class="flex-1 rounded-xl p-3 bg-white/80 border border-slate-200 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-slate-100 flex items-center justify-center text-sm">🔴</div>
    <div>
      <div class="font-bold text-sm text-slate-800">故障日志</div>
      <div class="text-xs text-slate-400">5 个</div>
    </div>
  </div>
  <div class="flex flex-wrap gap-1">
    <span v-for="e in ['Issue','Bug','LogEvent','异常类型','TraceId']" class="px-1.5 py-0.5 rounded-md text-xs bg-white border border-slate-200 text-slate-700">{{ e }}</span>
  </div>
</div>

<div class="flex-1 rounded-xl p-3 bg-white/80 border border-slate-200 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-slate-100 flex items-center justify-center text-sm">👤</div>
    <div>
      <div class="font-bold text-sm text-slate-800">人员维护</div>
      <div class="text-xs text-slate-400">3 个</div>
    </div>
  </div>
  <div class="flex flex-wrap gap-1">
    <span v-for="e in ['开发人员','修复人员','负责人']" class="px-1.5 py-0.5 rounded-md text-xs bg-white border border-slate-200 text-slate-700">{{ e }}</span>
  </div>
</div>

</div>

<div class="mt-3 flex items-center gap-4 text-xs text-slate-400">
  <div class="flex items-center gap-1"><div class="w-2.5 h-2.5 rounded-sm bg-slate-100 border border-slate-200"></div> 业务实体</div>
  <div class="flex items-center gap-1"><div class="w-2.5 h-2.5 rounded-sm bg-slate-100 border border-slate-200"></div> 维护实体</div>
  <div class="ml-auto text-slate-500">设计重点：业务对象负责描述故障发生位置，维护对象负责解释故障来源与修复过程。</div>
</div>

---
layout: default
background: false
---

<!-- ===== Page 4: 实体思维导图 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">实体全景视图</h2>
<!-- <p class="text-slate-500 text-sm mb-3">五大类别 · 层次化展示</p> -->

```mermaid {scale: 0.6}
mindmap
  root((电商订单故障排查图谱实体))
    业务实体
      用户
      订单
      商品
      SKU
      支付单
      库存记录
      物流单
      售后单
    系统模块实体
      订单模块
      支付模块
      库存模块
      物流模块
      售后模块
      优惠模块
    代码变更实体
      GitCommit
      代码文件
      开发人员
      模块变更
    故障日志实体
      Issue
      Bug
      LogEvent
      异常类型
      TraceId
    接口测试实体
      API接口
      API文档
      测试用例
```

<div class="grid grid-cols-3 gap-2 mt-1 text-[10px] leading-snug">
  <div class="rounded-lg bg-white/80 border border-slate-200 px-2 py-1"><b class="text-slate-700">业务核心</b>：订单连接用户、支付、库存、物流和售后。</div>
  <div class="rounded-lg bg-white/80 border border-slate-200 px-2 py-1"><b class="text-slate-700">维护链路</b>：Commit、Issue、Bug 和人员记录变更来源。</div>
  <div class="rounded-lg bg-white/80 border border-slate-200 px-2 py-1"><b class="text-slate-700">测试闭环</b>：接口与测试用例用于推导回归范围。</div>
</div>

---
layout: default
background: false
---

<!-- ===== Page 5: 数据源关系卡片 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">数据源关系抽取总览</h2>
<p class="text-slate-500 text-sm mb-4">4 类数据源 → 16 条关系 → 汇入知识图谱</p>

<div class="grid grid-cols-2 gap-3 h-[72%]">

<div class="rounded-xl border border-slate-200 bg-white/80 p-3 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-slate-700 text-white flex items-center justify-center text-xs font-bold">G</div>
    <span class="font-bold text-sm text-slate-800">Git 提交记录</span>
    <span class="text-xs text-slate-400 ml-auto">4 条</span>
  </div>
  <div class="flex flex-col gap-1">
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">Commit</b><span class="text-slate-400">—— 修改 ——</span><b class="text-slate-700">代码文件</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">代码文件</b><span class="text-slate-400">—— 属于 ——</span><b class="text-slate-700">系统模块</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">Commit</b><span class="text-slate-400">—— 影响 ——</span><b class="text-slate-700">系统模块</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">开发人员</b><span class="text-slate-400">—— 提交 ——</span><b class="text-slate-700">Commit</b></div>
  </div>
</div>

<div class="rounded-xl border border-slate-200 bg-white/80 p-3 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-slate-700 text-white flex items-center justify-center text-xs font-bold">I</div>
    <span class="font-bold text-sm text-slate-800">Issue / Bug</span>
    <span class="text-xs text-slate-400 ml-auto">5 条</span>
  </div>
  <div class="flex flex-col gap-1">
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">Issue</b><span class="text-slate-400">—— 描述 ——</span><b class="text-slate-700">Bug</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">Bug</b><span class="text-slate-400">—— 影响 ——</span><b class="text-slate-700">系统模块</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">Bug</b><span class="text-slate-400">—— 关联 ——</span><b class="text-slate-700">API 接口</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">修复人员</b><span class="text-slate-400">—— 修复 ——</span><b class="text-slate-700">Bug</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">Bug</b><span class="text-slate-400">—— 关联 ——</span><b class="text-slate-700">Commit</b></div>
  </div>
</div>

<div class="rounded-xl border border-slate-200 bg-white/80 p-3 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-slate-700 text-white flex items-center justify-center text-xs font-bold">L</div>
    <span class="font-bold text-sm text-slate-800">运行日志</span>
    <span class="text-xs text-slate-400 ml-auto">4 条</span>
  </div>
  <div class="flex flex-col gap-1">
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">LogEvent</b><span class="text-slate-400">—— 属于 ——</span><b class="text-slate-700">系统模块</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">LogEvent</b><span class="text-slate-400">—— 聚类为 ——</span><b class="text-slate-700">异常类型</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">LogEvent</b><span class="text-slate-400">—— 关联 ——</span><b class="text-slate-700">TraceId</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">TraceId</b><span class="text-slate-400">—— 追踪 ——</span><b class="text-slate-700">订单</b></div>
  </div>
</div>

<div class="rounded-xl border border-slate-200 bg-white/80 p-3 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-slate-700 text-white flex items-center justify-center text-xs font-bold">A</div>
    <span class="font-bold text-sm text-slate-800">API 文档</span>
    <span class="text-xs text-slate-400 ml-auto">3 条</span>
  </div>
  <div class="flex flex-col gap-1">
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">API 接口</b><span class="text-slate-400">—— 属于 ——</span><b class="text-slate-700">系统模块</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">API 接口</b><span class="text-slate-400">—— 操作 ——</span><b class="text-slate-700">业务实体</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-slate-700">API 接口</b><span class="text-slate-400">—— 被测试 ——</span><b class="text-slate-700">测试用例</b></div>
  </div>
</div>

</div>

<div class="mt-2 rounded-lg border border-slate-200 bg-slate-50 px-3 py-1.5 text-xs text-slate-500">
  抽取原则：每条边都来自 Git、Issue、日志或 API 文档中的结构化证据，避免凭经验手动画关系。
</div>

---
layout: default
background: false
---

<!-- ===== Page 6: 数据源关系详细图 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">数据源关系抽取详图</h2>
<p class="text-slate-500 text-sm mb-3">Git · Issue · 日志 · API —— 四类数据源的结构化关系</p>


<div class="grid grid-cols-2 gap-3 h-[68%]">

<div class="rounded-xl border border-slate-200 bg-white/85 p-3 flex flex-col justify-between">
  <div>
    <div class="flex items-center justify-between mb-2">
      <div class="font-bold text-sm text-slate-800">Git 数据源</div>
      <div class="text-[10px] px-2 py-0.5 rounded-full bg-slate-100 text-slate-500">代码变更</div>
    </div>
    <div class="text-xs text-slate-500 mb-2">从提交记录抽取文件修改、模块归属和提交人员。</div>
  </div>
  <div class="grid grid-cols-4 items-center gap-1 text-[11px] text-center">
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-1 py-2">开发人员</div>
    <div class="text-slate-400">→</div>
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-1 py-2">Commit</div>
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-1 py-2">代码文件</div>
  </div>
  <div class="mt-2 text-[11px] text-slate-500">关键边：提交、修改、属于、影响</div>
</div>

<div class="rounded-xl border border-slate-200 bg-white/85 p-3 flex flex-col justify-between">
  <div>
    <div class="flex items-center justify-between mb-2">
      <div class="font-bold text-sm text-slate-800">Issue / Bug 数据源</div>
      <div class="text-[10px] px-2 py-0.5 rounded-full bg-slate-100 text-slate-500">故障描述</div>
    </div>
    <div class="text-xs text-slate-500 mb-2">从问题单中抽取 Bug、影响模块、修复人员和关联接口。</div>
  </div>
  <div class="grid grid-cols-4 items-center gap-1 text-[11px] text-center">
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-1 py-2">Issue</div>
    <div class="text-slate-400">→</div>
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-1 py-2">Bug</div>
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-1 py-2">系统模块</div>
  </div>
  <div class="mt-2 text-[11px] text-slate-500">关键边：描述、影响、关联、修复</div>
</div>

<div class="rounded-xl border border-slate-200 bg-white/85 p-3 flex flex-col justify-between">
  <div>
    <div class="flex items-center justify-between mb-2">
      <div class="font-bold text-sm text-slate-800">运行日志数据源</div>
      <div class="text-[10px] px-2 py-0.5 rounded-full bg-slate-100 text-slate-500">线上异常</div>
    </div>
    <div class="text-xs text-slate-500 mb-2">从 LogEvent 聚类异常类型，并通过 TraceId 追踪订单。</div>
  </div>
  <div class="grid grid-cols-4 items-center gap-1 text-[11px] text-center">
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-1 py-2">LogEvent</div>
    <div class="text-slate-400">→</div>
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-1 py-2">TraceId</div>
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-1 py-2">订单</div>
  </div>
  <div class="mt-2 text-[11px] text-slate-500">关键边：聚类为、关联、追踪、属于</div>
</div>

<div class="rounded-xl border border-slate-200 bg-white/85 p-3 flex flex-col justify-between">
  <div>
    <div class="flex items-center justify-between mb-2">
      <div class="font-bold text-sm text-slate-800">API 文档数据源</div>
      <div class="text-[10px] px-2 py-0.5 rounded-full bg-slate-100 text-slate-500">接口测试</div>
    </div>
    <div class="text-xs text-slate-500 mb-2">从接口文档建立接口、模块、业务实体和测试用例映射。</div>
  </div>
  <div class="grid grid-cols-4 items-center gap-1 text-[11px] text-center">
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-1 py-2">API 接口</div>
    <div class="text-slate-400">→</div>
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-1 py-2">系统模块</div>
    <div class="rounded-lg border border-slate-200 bg-slate-50 px-1 py-2">测试用例</div>
  </div>
  <div class="mt-2 text-[11px] text-slate-500">关键边：属于、操作、被覆盖</div>
</div>

</div>

<div class="mt-3 rounded-lg border border-slate-200 bg-white/80 px-3 py-2 text-xs text-slate-600">
  汇入规则：四类数据源虽然格式不同，但最终都落到 <b class="text-slate-800">系统模块、业务实体、测试用例</b> 三类核心节点上，形成统一排障路径。
</div>

---
layout: default
background: false
---

<!-- ===== Page 7: 核心知识图谱结构（PNG） ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">核心知识图谱结构</h2>
<p class="text-slate-500 text-sm mb-3">以订单模块为中心，串联五维关联</p>

<div class="flex justify-center h-[78%]">
  <img src="/kg-architecture.png" class="max-h-full max-w-full object-contain rounded-lg shadow-lg" />
</div>

<div class="mt-2 flex justify-center gap-2 text-xs">
  <span class="px-2 py-1 rounded bg-white/80 border border-slate-200 text-slate-700">业务维度</span>
  <span class="px-2 py-1 rounded bg-white/80 border border-slate-200 text-slate-700">代码维度</span>
  <span class="px-2 py-1 rounded bg-white/80 border border-slate-200 text-slate-700">问题维度</span>
  <span class="px-2 py-1 rounded bg-white/80 border border-slate-200 text-slate-700">日志维度</span>
  <span class="px-2 py-1 rounded bg-white/80 border border-slate-200 text-slate-700">测试维度</span>
</div>

---
layout: default
background: false
---

<!-- ===== Page 8: 订单模块核心图谱 Mermaid ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">订单模块知识图谱</h2>
<!-- <p class="text-slate-500 text-sm mb-3">业务链路 · 接口 · 代码 · Bug · 日志 —— 五维一体</p> -->

```mermaid {scale: 0.68}
flowchart LR
    User[用户] -->|创建| Order[订单]
    Order -->|生成| Payment[支付单]
    Order -->|占用| Inventory[库存记录]
    Order -->|生成| Logistics[物流单]
    Order -->|产生| AfterSale[售后单]

    OrderModule[订单模块]:::core -->|管理| Order
    PaymentModule[支付模块] -->|处理| Payment
    InventoryModule[库存模块] -->|管理| Inventory

    API[API 接口] -->|属于| OrderModule
    API -->|被覆盖| TestCase[测试用例]

    Dev[开发人员] -->|提交| Commit[Git Commit]
    Commit -->|修改| File[代码文件]
    File -->|属于| OrderModule

    Issue[Issue] -->|描述| Bug[Bug]
    Bug -->|影响| OrderModule
    Dev -->|修复| Bug

    LogEvent[LogEvent] -->|聚类为| Exception[异常类型]
    LogEvent -->|关联| TraceId[TraceId]
    TraceId -->|追踪| Order
    LogEvent -->|属于| OrderModule

    classDef core fill:#3b82f6,stroke:#1e40af,color:#fff,stroke-width:2px
```

<div class="grid grid-cols-2 gap-3 mt-2 text-xs">
  <div class="rounded-lg border border-slate-200 bg-white/80 p-2"><b class="text-slate-700">右侧业务链路</b>：用户下单后关联支付单、库存记录、物流单和售后单。</div>
  <div class="rounded-lg border border-slate-200 bg-white/80 p-2"><b class="text-slate-700">左侧维护链路</b>：Commit、代码文件、Issue、Bug、LogEvent 和测试用例解释故障来源。</div>
</div>

---
layout: default
background: false
---

<!-- ===== Page 9: 查询路径 Q1 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">查询路径：模块变更 → 影响哪些测试？</h2>
<p class="text-slate-500 text-sm mb-2">变更影响分析 · 回归测试范围选择</p>


<div class="rounded-xl border border-slate-200 bg-white/85 p-4 mb-3">
  <div class="grid grid-cols-[1fr_auto_1fr_auto_1fr_auto_1fr_auto_1fr] items-center gap-2 text-center">
    <div class="rounded-lg bg-slate-50 border border-slate-200 px-2 py-3">
      <div class="text-[10px] text-slate-400 mb-1">Step 1</div>
      <div class="text-sm font-bold text-slate-800">Git Commit</div>
      <div class="text-[11px] text-slate-500">变更入口</div>
    </div>
    <div class="text-slate-400 text-xl">→</div>
    <div class="rounded-lg bg-slate-50 border border-slate-200 px-2 py-3">
      <div class="text-[10px] text-slate-400 mb-1">Step 2</div>
      <div class="text-sm font-bold text-slate-800">代码文件</div>
      <div class="text-[11px] text-slate-500">定位文件</div>
    </div>
    <div class="text-slate-400 text-xl">→</div>
    <div class="rounded-lg bg-slate-50 border border-slate-200 px-2 py-3">
      <div class="text-[10px] text-slate-400 mb-1">Step 3</div>
      <div class="text-sm font-bold text-slate-800">订单模块</div>
      <div class="text-[11px] text-slate-500">映射模块</div>
    </div>
    <div class="text-slate-400 text-xl">→</div>
    <div class="rounded-lg bg-slate-50 border border-slate-200 px-2 py-3">
      <div class="text-[10px] text-slate-400 mb-1">Step 4</div>
      <div class="text-sm font-bold text-slate-800">API 接口</div>
      <div class="text-[11px] text-slate-500">关联接口</div>
    </div>
    <div class="text-slate-400 text-xl">→</div>
    <div class="rounded-lg bg-slate-50 border border-slate-200 px-2 py-3">
      <div class="text-[10px] text-slate-400 mb-1">Step 5</div>
      <div class="text-sm font-bold text-slate-800">测试用例</div>
      <div class="text-[11px] text-slate-500">输出范围</div>
    </div>
  </div>
</div>

<div class="grid grid-cols-[1.15fr_0.85fr] gap-4">
<div class="rounded-xl border border-slate-200 bg-white/85 p-4">
  <div class="text-sm font-bold text-slate-800 mb-3">返回测试范围</div>
  <div class="grid grid-cols-2 gap-2 text-xs">
    <div class="rounded-lg bg-slate-50 border border-slate-200 px-3 py-2">订单创建测试</div>
    <div class="rounded-lg bg-slate-50 border border-slate-200 px-3 py-2">支付回调测试</div>
    <div class="rounded-lg bg-slate-50 border border-slate-200 px-3 py-2">库存锁定测试</div>
    <div class="rounded-lg bg-slate-50 border border-slate-200 px-3 py-2">订单取消测试</div>
  </div>
</div>

<div class="rounded-xl border border-slate-200 bg-slate-50/80 p-4">
  <div class="text-sm font-bold text-slate-800 mb-2">排查价值</div>
  <div class="text-xs text-slate-600 leading-relaxed">
    当订单服务代码发生变更时，图谱根据“文件—模块—接口—测试”的路径自动推导回归测试范围，减少凭经验选测试导致的遗漏。
  </div>
</div>
</div>

---
layout: default
background: false
---

<!-- ===== Page 10: 查询路径 Q2 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">查询路径：异常日志 → 订单与模块定位</h2>
<p class="text-slate-500 text-sm mb-2">从日志反查业务影响 · 快速定位故障范围</p>

```mermaid {scale: 0.7}
flowchart LR
    LogEvent[LogEvent: OrderStatusUpdateFailed] -->|聚类为| Exception[订单状态更新异常]
    LogEvent -->|关联| TraceId[TraceId: T20260507001]
    TraceId -->|追踪| API[支付回调接口]
    API -->|属于| PaymentModule[支付模块]
    TraceId -->|追踪| Order[订单: ORD20260507001]
    Order -->|当前| Status[状态: 未支付]
    Order -->|生成| Payment[支付单: 已支付]
```

<div class="flex gap-4 mt-2">
<div class="flex-1 rounded-xl border border-slate-200 bg-white/80 p-3">
  <div class="text-sm font-bold text-slate-800 mb-1">查询路径</div>
  <div class="text-xs text-slate-600">
    <b class="text-slate-700">LogEvent</b> → <b class="text-slate-700">TraceId</b> → <b class="text-slate-700">订单</b> → <b class="text-slate-700">系统模块</b>
  </div>
</div>
<div class="flex-1 rounded-xl border border-slate-200 bg-white p-3">
  <div class="text-sm font-bold text-slate-800 mb-1">实例数据</div>
  <div class="text-xs space-y-1">
    <div><span class="text-slate-400">LogEvent</span> <code class="text-slate-700 bg-white/80 px-1 rounded">OrderStatusUpdateFailed</code></div>
    <div><span class="text-slate-400">TraceId</span> <code class="text-slate-700 bg-slate-50 px-1 rounded">T20260507001</code></div>
    <div><span class="text-slate-400">订单</span> <code class="text-slate-700 bg-white/80 px-1 rounded">ORD20260507001</code></div>
    <div><span class="text-slate-400">涉及</span> <b class="text-slate-700">订单模块 / 支付模块</b></div>
  </div>
</div>
</div>

<div class="mt-2 text-xs text-slate-400 bg-slate-50 rounded-lg p-1.5 border border-slate-100">
  🎯 发现订单状态为"未支付"但支付单已支付，定位到支付回调接口异常
</div>

<div class="mt-1 text-xs text-slate-500">
  定位结论：故障范围集中在支付回调接口，以及订单模块与支付模块之间的状态同步链路。
</div>

---
layout: default
background: false
---

<!-- ===== Page 11: 风险与对策 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">图谱维护：风险与对策</h2>
<p class="text-slate-500 text-sm mb-4">如果图谱不随版本更新，一周内就会失效</p>

```mermaid {scale: 0.72}
flowchart TB
    Risk[图谱维护风险] --> R1[数据源分散]
    Risk --> R2[图谱更新不及时]
    Risk --> R3[模块映射不准确]
    Risk --> R4[日志缺少 TraceId]
    Risk --> R5[Issue 描述不规范]

    R1 --> S1[统一抽取规则]
    R2 --> S2[随版本自动同步]
    R3 --> S3[核心关系人工校验]
    R4 --> S4[统一日志规范]
    R5 --> S5[制定 Issue 模板]
```

<div class="grid grid-cols-5 gap-2 mt-2 text-xs">
  <div class="rounded-lg border border-slate-200 bg-white p-2"><b>数据源分散</b><br/><span class="text-slate-500">统一抽取规则</span></div>
  <div class="rounded-lg border border-slate-200 bg-white p-2"><b>更新不及时</b><br/><span class="text-slate-500">版本自动同步</span></div>
  <div class="rounded-lg border border-slate-200 bg-white p-2"><b>映射不准确</b><br/><span class="text-slate-500">核心关系校验</span></div>
  <div class="rounded-lg border border-slate-200 bg-white p-2"><b>日志缺标识</b><br/><span class="text-slate-500">强制 TraceId</span></div>
  <div class="rounded-lg border border-slate-200 bg-white p-2"><b>Issue 不规范</b><br/><span class="text-slate-500">制定模板</span></div>
</div>

---
layout: default
background: false
---

<!-- ===== Page 12: 维护机制与闭环 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">维护机制与闭环</h2>
<p class="text-slate-500 text-sm mb-4">图谱随版本持续演进，而非一次性交付</p>

<div class="flex gap-5 h-[72%]">

<div class="w-[45%] flex flex-col gap-3">
  <div class="flex items-start gap-3 p-3 rounded-xl border border-slate-200 bg-white/80">
    <div class="w-8 h-8 rounded-full bg-slate-700 flex items-center justify-center text-white font-bold text-sm shrink-0">1</div>
    <div>
      <div class="font-bold text-sm text-slate-800">Git 提交触发更新</div>
      <div class="text-xs text-slate-500 mt-0.5">每次 Commit 后根据修改文件更新"文件—模块"关系</div>
    </div>
  </div>
  <div class="flex items-start gap-3 p-3 rounded-xl border border-slate-200 bg-white/80">
    <div class="w-8 h-8 rounded-full bg-slate-700 flex items-center justify-center text-white font-bold text-sm shrink-0">2</div>
    <div>
      <div class="font-bold text-sm text-slate-800">Issue 关闭时同步 Bug 关系</div>
      <div class="text-xs text-slate-500 mt-0.5">Bug 修复后记录修复人员、影响模块和关联 Commit</div>
    </div>
  </div>
  <div class="flex items-start gap-3 p-3 rounded-xl border border-slate-200 bg-white/80">
    <div class="w-8 h-8 rounded-full bg-slate-700 flex items-center justify-center text-white font-bold text-sm shrink-0">3</div>
    <div>
      <div class="font-bold text-sm text-slate-800">日志定期聚类更新异常</div>
      <div class="text-xs text-slate-500 mt-0.5">定期分析 LogEvent 将相似异常归类到同一异常类型</div>
    </div>
  </div>
  <div class="flex items-start gap-3 p-3 rounded-xl border border-slate-200 bg-white/80">
    <div class="w-8 h-8 rounded-full bg-slate-700 flex items-center justify-center text-white font-bold text-sm shrink-0">4</div>
    <div>
      <div class="font-bold text-sm text-slate-800">API 文档随版本同步</div>
      <div class="text-xs text-slate-500 mt-0.5">接口变更后同步更新"接口—模块—测试"关系</div>
    </div>
  </div>
</div>

<div class="flex-1 flex items-center justify-center">
  <img src="/maintenance-flow.png" class="max-h-full max-w-full object-contain rounded-lg shadow-lg" />
</div>

</div>

<div class="mt-3 text-center text-xs text-slate-400">
  本方案构建的是一个<strong class="text-slate-600">可维护</strong>的故障排查知识图谱，随系统版本持续更新
</div>

---
layout: center
background: false
---

<!-- ===== Page 13: Summary ===== -->

<div class="text-center">

<h2 class="text-4xl font-bold text-slate-800 mb-4">总结</h2>

<div class="grid grid-cols-3 gap-4 text-left mb-6">
  <div class="rounded-xl border border-slate-200 bg-white/80 p-4">
    <div class="font-bold text-slate-700 mb-2">实体层</div>
    <div class="text-sm text-slate-600 leading-relaxed">覆盖订单、支付、库存、物流、售后等业务对象，以及 Commit、Bug、LogEvent、TraceId、API 接口和测试用例。</div>
  </div>
  <div class="rounded-xl border border-slate-200 bg-white/80 p-4">
    <div class="font-bold text-slate-700 mb-2">关系层</div>
    <div class="text-sm text-slate-600 leading-relaxed">将代码变更、故障描述、日志异常、接口文档和测试用例连接为可追踪路径。</div>
  </div>
  <div class="rounded-xl border border-slate-200 bg-white/80 p-4">
    <div class="font-bold text-slate-700 mb-2">应用层</div>
    <div class="text-sm text-slate-600 leading-relaxed">支持影响分析、异常反查、Bug 统计、人员定位和回归测试范围判断。</div>
  </div>
</div>

<div class="inline-flex flex-col gap-2 rounded-xl border border-slate-200 bg-slate-50 px-8 py-5 text-left">
  <div class="text-lg font-bold text-slate-800">核心价值</div>
  <div class="text-sm text-slate-600">帮助开发和维护人员更快回答：哪个模块出了问题？这次变更影响什么？应该找谁修、测哪些内容？</div>
</div>

<div class="mt-7 text-3xl font-bold text-slate-800">谢谢大家</div>
<div class="mt-2 text-xs tracking-widest uppercase text-slate-400">Powered by Slidev</div>

</div>
