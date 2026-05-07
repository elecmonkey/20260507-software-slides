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
background: https://cover.sli.dev
---

<!-- ===== Page 1: Cover ===== -->

<div class="text-center">

<div class="text-white-500 text-xs tracking-widest uppercase mb-2">Knowledge Graph for E-Commerce Troubleshooting</div>

# 电商订单故障排查知识图谱

<div class="text-white-500 text-base mb-8">多源数据融合 · 故障定位 · 影响分析</div>

<div class="flex justify-center gap-5 items-end mb-5">
  <div class="w-20 h-14 rounded-xl border-2 border-orange-400/50 bg-orange-50 flex flex-col items-center justify-center">
    <span class="text-base font-bold text-orange-500">Git</span>
    <span class="text-xs text-slate-400">提交记录</span>
  </div>
  <div class="text-slate-300 mb-2">→</div>
  <div class="w-20 h-14 rounded-xl border-2 border-red-400/50 bg-red-50 flex flex-col items-center justify-center">
    <span class="text-base font-bold text-red-500">Issue</span>
    <span class="text-xs text-slate-400">Bug 追踪</span>
  </div>
  <div class="text-slate-300 mb-2">→</div>
  <div class="w-20 h-14 rounded-xl border-2 border-yellow-500/50 bg-yellow-50 flex flex-col items-center justify-center">
    <span class="text-base font-bold text-yellow-600">日志</span>
    <span class="text-xs text-slate-400">运行日志</span>
  </div>
  <div class="text-slate-300 mb-2">→</div>
  <div class="w-20 h-14 rounded-xl border-2 border-green-400/50 bg-green-50 flex flex-col items-center justify-center">
    <span class="text-base font-bold text-green-500">API文档</span>
    <span class="text-xs text-slate-400">接口规范</span>
  </div>
</div>

<div class="inline-flex px-8 py-3 rounded-full bg-gradient-to-r from-blue-600 to-cyan-500 text-white text-lg font-bold shadow-lg mb-6">
  故障排查知识图谱
</div>

<div class="flex justify-center gap-3">
  <span class="px-3 py-1 rounded-full bg-slate-100 border border-slate-200 text-sm text-slate-600">影响分析</span>
  <span class="px-3 py-1 rounded-full bg-slate-100 border border-slate-200 text-sm text-slate-600">故障定位</span>
  <span class="px-3 py-1 rounded-full bg-slate-100 border border-slate-200 text-sm text-slate-600">Bug 统计</span>
  <span class="px-3 py-1 rounded-full bg-slate-100 border border-slate-200 text-sm text-slate-600">回归测试</span>
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

---
layout: default
background: false
---

<!-- ===== Page 3: 实体分类卡片 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">实体分类设计</h2>
<p class="text-slate-500 text-sm mb-5">5 大类 · 20+ 实体 · 覆盖业务链路与维护链路</p>

<div class="flex gap-3 h-[62%]">

<div class="flex-1 rounded-xl p-3 bg-blue-50/60 border border-blue-200 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-blue-100 flex items-center justify-center text-sm">📦</div>
    <div>
      <div class="font-bold text-sm text-slate-800">业务实体</div>
      <div class="text-xs text-slate-400">8 个</div>
    </div>
  </div>
  <div class="flex flex-wrap gap-1">
    <span v-for="e in ['用户','订单','商品','SKU','支付单','物流单','库存记录','售后单']" class="px-1.5 py-0.5 rounded-md text-xs bg-white border border-blue-200 text-blue-700">{{ e }}</span>
  </div>
</div>

<div class="flex-1 rounded-xl p-3 bg-violet-50/60 border border-violet-200 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-violet-100 flex items-center justify-center text-sm">⚙️</div>
    <div>
      <div class="font-bold text-sm text-slate-800">系统模块</div>
      <div class="text-xs text-slate-400">6 个</div>
    </div>
  </div>
  <div class="flex flex-wrap gap-1">
    <span v-for="e in ['订单模块','支付模块','库存模块','物流模块','售后模块','优惠模块']" class="px-1.5 py-0.5 rounded-md text-xs bg-white border border-violet-200 text-violet-700">{{ e }}</span>
  </div>
</div>

<div class="flex-1 rounded-xl p-3 bg-amber-50/60 border border-amber-200 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-amber-100 flex items-center justify-center text-sm">📝</div>
    <div>
      <div class="font-bold text-sm text-slate-800">代码变更</div>
      <div class="text-xs text-slate-400">4 个</div>
    </div>
  </div>
  <div class="flex flex-wrap gap-1">
    <span v-for="e in ['Git Commit','代码文件','API 接口','测试用例']" class="px-1.5 py-0.5 rounded-md text-xs bg-white border border-amber-200 text-amber-700">{{ e }}</span>
  </div>
</div>

<div class="flex-1 rounded-xl p-3 bg-red-50/60 border border-red-200 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-red-100 flex items-center justify-center text-sm">🔴</div>
    <div>
      <div class="font-bold text-sm text-slate-800">故障日志</div>
      <div class="text-xs text-slate-400">5 个</div>
    </div>
  </div>
  <div class="flex flex-wrap gap-1">
    <span v-for="e in ['Issue','Bug','LogEvent','异常类型','TraceId']" class="px-1.5 py-0.5 rounded-md text-xs bg-white border border-red-200 text-red-700">{{ e }}</span>
  </div>
</div>

<div class="flex-1 rounded-xl p-3 bg-emerald-50/60 border border-emerald-200 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-emerald-100 flex items-center justify-center text-sm">👤</div>
    <div>
      <div class="font-bold text-sm text-slate-800">人员维护</div>
      <div class="text-xs text-slate-400">3 个</div>
    </div>
  </div>
  <div class="flex flex-wrap gap-1">
    <span v-for="e in ['开发人员','修复人员','负责人']" class="px-1.5 py-0.5 rounded-md text-xs bg-white border border-emerald-200 text-emerald-700">{{ e }}</span>
  </div>
</div>

</div>

<div class="mt-3 flex items-center gap-4 text-xs text-slate-400">
  <div class="flex items-center gap-1"><div class="w-2.5 h-2.5 rounded-sm bg-blue-100 border border-blue-300"></div> 业务实体</div>
  <div class="flex items-center gap-1"><div class="w-2.5 h-2.5 rounded-sm bg-amber-100 border border-amber-300"></div> 维护实体</div>
</div>

---
layout: default
background: false
---

<!-- ===== Page 4: 实体思维导图 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">实体全景视图</h2>
<!-- <p class="text-slate-500 text-sm mb-3">五大类别 · 层次化展示</p> -->

```mermaid {scale: 0.72}
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

---
layout: default
background: false
---

<!-- ===== Page 5: 数据源关系卡片 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">数据源关系抽取总览</h2>
<p class="text-slate-500 text-sm mb-4">4 类数据源 → 16 条关系 → 汇入知识图谱</p>

<div class="grid grid-cols-2 gap-3 h-[72%]">

<div class="rounded-xl border border-orange-200 bg-orange-50/30 p-3 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-orange-500 text-white flex items-center justify-center text-xs font-bold">G</div>
    <span class="font-bold text-sm text-slate-800">Git 提交记录</span>
    <span class="text-xs text-slate-400 ml-auto">4 条</span>
  </div>
  <div class="flex flex-col gap-1">
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-orange-700">Commit</b><span class="text-slate-400">—— 修改 ——</span><b class="text-orange-700">代码文件</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-orange-700">代码文件</b><span class="text-slate-400">—— 属于 ——</span><b class="text-orange-700">系统模块</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-orange-700">Commit</b><span class="text-slate-400">—— 影响 ——</span><b class="text-orange-700">系统模块</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-orange-700">开发人员</b><span class="text-slate-400">—— 提交 ——</span><b class="text-orange-700">Commit</b></div>
  </div>
</div>

<div class="rounded-xl border border-red-200 bg-red-50/30 p-3 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-red-500 text-white flex items-center justify-center text-xs font-bold">I</div>
    <span class="font-bold text-sm text-slate-800">Issue / Bug</span>
    <span class="text-xs text-slate-400 ml-auto">5 条</span>
  </div>
  <div class="flex flex-col gap-1">
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-red-700">Issue</b><span class="text-slate-400">—— 描述 ——</span><b class="text-red-700">Bug</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-red-700">Bug</b><span class="text-slate-400">—— 影响 ——</span><b class="text-red-700">系统模块</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-red-700">Bug</b><span class="text-slate-400">—— 关联 ——</span><b class="text-red-700">API 接口</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-red-700">修复人员</b><span class="text-slate-400">—— 修复 ——</span><b class="text-red-700">Bug</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-red-700">Bug</b><span class="text-slate-400">—— 关联 ——</span><b class="text-red-700">Commit</b></div>
  </div>
</div>

<div class="rounded-xl border border-yellow-200 bg-yellow-50/30 p-3 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-yellow-500 text-white flex items-center justify-center text-xs font-bold">L</div>
    <span class="font-bold text-sm text-slate-800">运行日志</span>
    <span class="text-xs text-slate-400 ml-auto">4 条</span>
  </div>
  <div class="flex flex-col gap-1">
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-yellow-700">LogEvent</b><span class="text-slate-400">—— 属于 ——</span><b class="text-yellow-700">系统模块</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-yellow-700">LogEvent</b><span class="text-slate-400">—— 聚类为 ——</span><b class="text-yellow-700">异常类型</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-yellow-700">LogEvent</b><span class="text-slate-400">—— 关联 ——</span><b class="text-yellow-700">TraceId</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-yellow-700">TraceId</b><span class="text-slate-400">—— 追踪 ——</span><b class="text-yellow-700">订单</b></div>
  </div>
</div>

<div class="rounded-xl border border-green-200 bg-green-50/30 p-3 flex flex-col">
  <div class="flex items-center gap-2 mb-2">
    <div class="w-7 h-7 rounded-lg bg-green-500 text-white flex items-center justify-center text-xs font-bold">A</div>
    <span class="font-bold text-sm text-slate-800">API 文档</span>
    <span class="text-xs text-slate-400 ml-auto">3 条</span>
  </div>
  <div class="flex flex-col gap-1">
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-green-700">API 接口</b><span class="text-slate-400">—— 属于 ——</span><b class="text-green-700">系统模块</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-green-700">API 接口</b><span class="text-slate-400">—— 操作 ——</span><b class="text-green-700">业务实体</b></div>
    <div class="flex items-center gap-2 text-xs px-2 py-1 rounded bg-white/80"><b class="text-green-700">API 接口</b><span class="text-slate-400">—— 被测试 ——</span><b class="text-green-700">测试用例</b></div>
  </div>
</div>

</div>

---
layout: default
background: false
---

<!-- ===== Page 6: 数据源关系详细图 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">数据源关系抽取详图</h2>
<p class="text-slate-500 text-sm mb-3">Git · Issue · 日志 · API —— 四类数据源的结构化关系</p>


<div class="flex flex-row">

```mermaid {scale: 0.38}
flowchart LR
    subgraph Git数据源
        Dev[开发人员] -->|提交| Commit[Git Commit]
        Commit -->|修改| File[代码文件]
        File -->|属于| ModuleA[系统模块]
        Commit -->|影响| ModuleA
    end

    subgraph Issue数据源
        Issue[Issue] -->|描述| Bug[Bug]
        Bug -->|影响| ModuleB[系统模块]
        Dev2[修复人员] -->|修复| Bug
        Bug -->|关联| API1[API 接口]
    end

```

```mermaid {scale: 0.5}
flowchart LR
    subgraph 日志数据源
        LogEvent[LogEvent] -->|聚类为| Exception[异常类型]
        LogEvent -->|关联| TraceId[TraceId]
        TraceId -->|追踪| Order[订单]
        LogEvent -->|属于| ModuleC[系统模块]
    end

    subgraph API文档数据源
        API2[API 接口] -->|属于| ModuleD[系统模块]
        API2 -->|操作| Entity[业务实体]
        API2 -->|被覆盖| TestCase[测试用例]
    end
```

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

---
layout: default
background: false
---

<!-- ===== Page 9: 查询路径 Q1 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">查询路径：模块变更 → 影响哪些测试？</h2>
<p class="text-slate-500 text-sm mb-2">变更影响分析 · 回归测试范围选择</p>


```mermaid {scale: 0.72}
flowchart LR
    Commit[Git Commit] -->|修改| File[代码文件]
    File -->|属于| OrderModule[订单模块]
    OrderModule -->|提供| API[API 接口]
    API -->|被覆盖| TestCase[测试用例]

    TestCase --> TC1[订单创建测试]
    TestCase --> TC2[支付回调测试]
    TestCase --> TC3[库存锁定测试]
    TestCase --> TC4[订单取消测试]
```

<div class="flex gap-4 mt-2">
<div class="flex-1 rounded-xl border border-blue-200 bg-blue-50/20 p-3">
  <div class="text-sm font-bold text-slate-800 mb-1">查询路径</div>
  <div class="text-xs text-slate-600">
    <b class="text-blue-700">Commit</b> → <b class="text-blue-700">文件</b> → <b class="text-blue-700">订单模块</b> → <b class="text-blue-700">API 接口</b> → <b class="text-blue-700">测试用例</b>
  </div>
</div>
<div class="flex-1 rounded-xl border border-green-200 bg-green-50/20 p-3">
  <div class="text-sm font-bold text-slate-800 mb-1">返回结果</div>
  <div class="flex flex-wrap gap-1">
    <span class="px-2 py-0.5 rounded-md bg-green-100 border border-green-200 text-green-700 text-xs">订单创建测试</span>
    <span class="px-2 py-0.5 rounded-md bg-green-100 border border-green-200 text-green-700 text-xs">支付回调测试</span>
    <span class="px-2 py-0.5 rounded-md bg-green-100 border border-green-200 text-green-700 text-xs">库存锁定测试</span>
    <span class="px-2 py-0.5 rounded-md bg-green-100 border border-green-200 text-green-700 text-xs">订单取消测试</span>
  </div>
</div>
</div>

<div class="mt-2 text-xs text-slate-400 bg-slate-50 rounded-lg p-1.5 border border-slate-100">
  🎯 帮助确定回归测试范围，减少遗漏
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
<div class="flex-1 rounded-xl border border-red-200 bg-red-50/20 p-3">
  <div class="text-sm font-bold text-slate-800 mb-1">查询路径</div>
  <div class="text-xs text-slate-600">
    <b class="text-red-700">LogEvent</b> → <b class="text-red-700">TraceId</b> → <b class="text-red-700">订单</b> → <b class="text-red-700">系统模块</b>
  </div>
</div>
<div class="flex-1 rounded-xl border border-slate-200 bg-white p-3">
  <div class="text-sm font-bold text-slate-800 mb-1">实例数据</div>
  <div class="text-xs space-y-1">
    <div><span class="text-slate-400">LogEvent</span> <code class="text-red-700 bg-red-50 px-1 rounded">OrderStatusUpdateFailed</code></div>
    <div><span class="text-slate-400">TraceId</span> <code class="text-slate-700 bg-slate-50 px-1 rounded">T20260507001</code></div>
    <div><span class="text-slate-400">订单</span> <code class="text-blue-700 bg-blue-50 px-1 rounded">ORD20260507001</code></div>
    <div><span class="text-slate-400">涉及</span> <b class="text-violet-700">订单模块 / 支付模块</b></div>
  </div>
</div>
</div>

<div class="mt-2 text-xs text-slate-400 bg-slate-50 rounded-lg p-1.5 border border-slate-100">
  🎯 发现订单状态为"未支付"但支付单已支付，定位到支付回调接口异常
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

---
layout: default
background: false
---

<!-- ===== Page 12: 维护机制与闭环 ===== -->

<h2 class="text-3xl font-bold text-slate-800 mb-1">维护机制与闭环</h2>
<p class="text-slate-500 text-sm mb-4">图谱随版本持续演进，而非一次性交付</p>

<div class="flex gap-5 h-[72%]">

<div class="w-[45%] flex flex-col gap-3">
  <div class="flex items-start gap-3 p-3 rounded-xl border border-orange-200 bg-orange-50/30">
    <div class="w-8 h-8 rounded-full bg-orange-500 flex items-center justify-center text-white font-bold text-sm shrink-0">1</div>
    <div>
      <div class="font-bold text-sm text-slate-800">Git 提交触发更新</div>
      <div class="text-xs text-slate-500 mt-0.5">每次 Commit 后根据修改文件更新"文件—模块"关系</div>
    </div>
  </div>
  <div class="flex items-start gap-3 p-3 rounded-xl border border-red-200 bg-red-50/30">
    <div class="w-8 h-8 rounded-full bg-red-500 flex items-center justify-center text-white font-bold text-sm shrink-0">2</div>
    <div>
      <div class="font-bold text-sm text-slate-800">Issue 关闭时同步 Bug 关系</div>
      <div class="text-xs text-slate-500 mt-0.5">Bug 修复后记录修复人员、影响模块和关联 Commit</div>
    </div>
  </div>
  <div class="flex items-start gap-3 p-3 rounded-xl border border-yellow-200 bg-yellow-50/30">
    <div class="w-8 h-8 rounded-full bg-yellow-500 flex items-center justify-center text-white font-bold text-sm shrink-0">3</div>
    <div>
      <div class="font-bold text-sm text-slate-800">日志定期聚类更新异常</div>
      <div class="text-xs text-slate-500 mt-0.5">定期分析 LogEvent 将相似异常归类到同一异常类型</div>
    </div>
  </div>
  <div class="flex items-start gap-3 p-3 rounded-xl border border-green-200 bg-green-50/30">
    <div class="w-8 h-8 rounded-full bg-green-500 flex items-center justify-center text-white font-bold text-sm shrink-0">4</div>
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
