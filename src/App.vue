<script setup>
import { computed, ref } from 'vue'

const selectedModel = ref('pro')

const models = {
  pro: {
    name: 'DeepSeek‑V4‑Pro',
    tone: '复杂推理 / Agentic Coding / 世界知识',
    promise: '面向高难任务的旗舰版本，在 Agent 能力、数学、STEM 与竞赛型代码评测中达到开源前列，并向顶级闭源模型靠近。',
    points: ['适合长链路 Agent', '建议复杂场景启用思考模式 max', 'API 并发限制 500'],
    price: [
      ['缓存命中输入', '0.025 元 / 百万 tokens'],
      ['缓存未命中输入', '3 元 / 百万 tokens'],
      ['输出', '6 元 / 百万 tokens'],
    ],
  },
  flash: {
    name: 'DeepSeek‑V4‑Flash',
    tone: '低成本 / 高并发 / 日常生产流量',
    promise: '更小参数与激活规模带来更快、更经济的服务体验，在简单 Agent 任务中接近 Pro，是大规模调用的实用入口。',
    points: ['适合高频业务调用', '支持非思考与思考模式', 'API 并发限制 2500'],
    price: [
      ['缓存命中输入', '0.02 元 / 百万 tokens'],
      ['缓存未命中输入', '1 元 / 百万 tokens'],
      ['输出', '2 元 / 百万 tokens'],
    ],
  },
}

const activeModel = computed(() => models[selectedModel.value])

const coordinates = [
  { value: '1M', label: '上下文长度', note: '百万级上下文成为官方服务标配' },
  { value: '384K', label: '最大输出', note: '为长文档生成与复杂 Agent 留足余量' },
  { value: 'DSA', label: '稀疏注意力', note: '在 token 维度压缩，降低长上下文计算与显存压力' },
  { value: '2', label: '模型形态', note: 'Pro 追求上限，Flash 追求速度与经济性' },
]

const capabilities = [
  '非思考模式与思考模式同框可选',
  'OpenAI ChatCompletions 与 Anthropic 接口兼容',
  'JSON Output、Tool Calls、FIM 补全能力保留',
  '针对 Claude Code、OpenClaw、OpenCode、CodeBuddy 等 Agent 产品优化',
]

const sources = [
  { label: 'DeepSeek-V4 预览版公告', href: 'https://api-docs.deepseek.com/zh-cn/news/news260424' },
  { label: '模型与 API 价格', href: 'https://api-docs.deepseek.com/zh-cn/quick_start/pricing' },
  { label: '开源权重合集', href: 'https://huggingface.co/collections/deepseek-ai/deepseek-v4' },
]
</script>

<template>
  <div class="page-shell">
    <header class="masthead" aria-label="页面导航">
      <a class="masthead__brand" href="#top" aria-label="返回顶部">
        <span class="brand-mark" aria-hidden="true">
          <svg viewBox="0 0 27 23" role="img">
            <path class="whale__official" d="M26.5174 3.39471C26.235 3.2567 26.1137 3.52006 25.9487 3.65346C25.8923 3.69659 25.8446 3.75294 25.7969 3.80469C25.3846 4.24516 24.9027 4.53439 24.2737 4.49989C23.3536 4.44814 22.5682 4.73737 21.8735 5.44119C21.7258 4.57349 21.2353 4.0554 20.4889 3.72304C20.0985 3.55054 19.7034 3.37746 19.4297 3.00197C19.2388 2.73459 19.1865 2.43673 19.091 2.14289C19.0301 1.96579 18.9697 1.78466 18.7656 1.75418C18.5442 1.71968 18.4574 1.90541 18.3705 2.06067C18.0232 2.69549 17.8887 3.39471 17.9019 4.10313C17.9324 5.6965 18.6051 6.96556 19.9421 7.86834C20.0939 7.97184 20.133 8.07535 20.0852 8.22658C19.9938 8.53766 19.8857 8.83955 19.7903 9.15063C19.7293 9.34901 19.6384 9.39271 19.4257 9.30588C18.692 8.9994 18.0583 8.54571 17.4982 7.99772C16.5477 7.07827 15.6881 6.06336 14.6162 5.26869C14.3644 5.08296 14.1125 4.91045 13.8521 4.746C12.7584 3.68394 13.9952 2.81164 14.2816 2.70814C14.5812 2.60003 14.3857 2.22857 13.4179 2.23317C12.4502 2.2372 11.5646 2.56151 10.4359 2.99335C10.2708 3.05832 10.0972 3.10547 9.91951 3.14457C8.8954 2.95022 7.83162 2.90709 6.72069 3.03245C4.62877 3.26533 2.95777 4.25436 1.72954 5.94261C0.254043 7.97184 -0.0932678 10.2777 0.33167 12.6824C0.778458 15.2171 2.07225 17.3153 4.06008 18.9558C6.12152 20.6567 8.49577 21.4905 11.2047 21.3306C12.8498 21.2358 14.6812 21.0155 16.7473 19.2669C17.2682 19.5262 17.8151 19.6297 18.7219 19.7074C19.4205 19.7723 20.0933 19.6729 20.6143 19.5648C21.4302 19.3923 21.3739 18.6367 21.0789 18.4981C18.6874 17.3843 19.2124 17.8374 18.7351 17.4706C19.9501 16.033 21.8063 13.4776 22.379 9.99821C22.4353 9.61409 22.5072 9.073 22.4986 8.76192C22.494 8.57216 22.5377 8.49856 22.7545 8.47671C23.3536 8.40771 23.935 8.24383 24.4692 7.94999C26.0188 7.10357 26.6439 5.71318 26.7911 4.04678C26.8129 3.79204 26.7865 3.52869 26.5174 3.39471ZM13.0143 18.3946C10.6964 16.5724 9.5722 15.9726 9.10816 15.9985C8.67402 16.0244 8.75222 16.5212 8.84768 16.8449C8.94773 17.1646 9.07768 17.3849 9.25996 17.6655C9.38589 17.8512 9.47272 18.1272 9.13404 18.3348C8.38766 18.7965 7.08985 18.1796 7.0289 18.1491C5.51833 17.2595 4.25559 16.0853 3.36546 14.4793C2.50581 12.9337 2.0067 11.2753 1.92447 9.50542C1.90262 9.07818 2.02855 8.92695 2.45406 8.84932C3.01413 8.74582 3.59144 8.72397 4.15093 8.80619C6.51656 9.15178 8.53027 10.2092 10.2185 11.8848C11.1822 12.8388 11.9114 13.979 12.6623 15.0929C13.461 16.2757 14.3201 17.4027 15.4144 18.3268C15.8008 18.6505 16.109 18.8966 16.404 19.0783C15.5144 19.1778 14.0297 19.1991 13.0143 18.3958V18.3946ZM14.1252 11.2489C14.1252 11.0591 14.277 10.9079 14.4679 10.9079C14.511 10.9079 14.5501 10.9165 14.5852 10.9292C14.6329 10.9464 14.6766 10.9723 14.7111 11.0114C14.7721 11.0718 14.8066 11.158 14.8066 11.2489C14.8066 11.4386 14.6548 11.5899 14.4639 11.5899C14.273 11.5899 14.1252 11.4386 14.1252 11.2489ZM17.5759 13.0188C17.3545 13.1096 17.1331 13.1873 16.9203 13.1959C16.5903 13.2131 16.2303 13.0791 16.0348 12.9153C15.7312 12.6605 15.5139 12.5179 15.423 12.0734C15.3839 11.8837 15.4057 11.5899 15.4402 11.4214C15.5185 11.0585 15.4316 10.8257 15.1757 10.614C14.9676 10.4415 14.7025 10.3938 14.4115 10.3938C14.3029 10.3938 14.2034 10.3461 14.1292 10.3076C14.0079 10.2472 13.9078 10.096 14.0033 9.91023C14.0338 9.84985 14.1815 9.70322 14.216 9.67734C14.6111 9.45251 15.0665 9.52612 15.488 9.6946C15.8784 9.85445 16.174 10.1477 16.5989 10.5623C17.033 11.0631 17.1112 11.2011 17.3585 11.5772C17.554 11.871 17.7317 12.1729 17.8536 12.5185C17.9272 12.7341 17.8317 12.9107 17.5759 13.0188Z" />
          </svg>
        </span>
        <span>DeepSeek V4</span>
      </a>
      <nav class="masthead__nav">
        <a href="#context">百万上下文</a>
        <a href="#models">模型选择</a>
        <a href="#api">API</a>
      </nav>
      <a class="masthead__source" href="https://chat.deepseek.com/" target="_blank" rel="noreferrer">立即体验</a>
    </header>

    <main id="top">
      <section class="hero" aria-labelledby="hero-title">
        <div class="hero__visual" aria-hidden="true">
          <svg class="chart context-map" viewBox="0 0 640 640" role="img">
            <defs>
              <linearGradient id="pageWash" x1="0" x2="1" y1="0" y2="1">
                <stop offset="0%" stop-color="#fffcef" stop-opacity="0.92" />
                <stop offset="100%" stop-color="#d8d0bb" stop-opacity="0.52" />
              </linearGradient>
              <linearGradient id="tokenFlow" x1="0" x2="1" y1="0" y2="0">
                <stop offset="0%" stop-color="#273e91" stop-opacity="0.24" />
                <stop offset="62%" stop-color="#273e91" stop-opacity="0.72" />
                <stop offset="100%" stop-color="#c8f05a" stop-opacity="0.96" />
              </linearGradient>
            </defs>
            <g class="context-map__papers" transform="rotate(-5 320 320)">
              <rect class="context-map__paper context-map__paper--back" x="138" y="70" width="370" height="452" rx="16" />
              <rect class="context-map__paper context-map__paper--mid" x="112" y="92" width="396" height="452" rx="16" />
              <rect class="context-map__paper" x="86" y="114" width="420" height="424" rx="16" />
              <path class="context-map__header" d="M118 174H474" />
              <text x="118" y="152" class="context-map__title">LONG CONTEXT BUFFER</text>
              <g class="context-map__rows">
                <path d="M120 206H438" />
                <path d="M120 236H386" />
                <path d="M120 266H464" />
                <path d="M120 296H328" />
                <path d="M120 326H450" />
                <path d="M120 356H404" />
                <path d="M120 386H468" />
                <path d="M120 416H350" />
                <path d="M120 446H430" />
              </g>
              <g class="context-map__chunks">
                <rect x="330" y="222" width="118" height="22" rx="4" />
                <rect x="146" y="282" width="138" height="22" rx="4" />
                <rect x="292" y="402" width="126" height="22" rx="4" />
              </g>
            </g>
            <g class="context-map__ruler">
              <path d="M548 112h34v396h-34" />
              <path d="M534 178h35M534 244h35M534 310h35M534 376h35M534 442h35" />
              <text x="612" y="310" transform="rotate(90 612 310)">1M context window</text>
            </g>
            <g class="context-map__flow">
              <path d="M116 486C210 442 286 428 362 438C425 446 464 424 524 360" />
              <path d="M154 520C236 486 304 472 382 478C438 482 484 454 540 402" />
              <circle cx="524" cy="360" r="10" />
            </g>
          </svg>
          <div class="metric-slab">
            <div class="metric-slab__content">
              <strong>1M</strong>
              <span>tokens context</span>
            </div>
          </div>
          <div class="coordinate-card coordinate-card--a">DSA / token 压缩</div>
          <div class="coordinate-card coordinate-card--b">Pro + Flash</div>
        </div>

        <div class="hero__copy">
          <p class="dateline">2026.04.24 预览版开放 · Web / App / API 同步上线</p>
          <h1 id="hero-title">
            <span>百万上下文</span>
            <span>完整现场</span>
          </h1>
          <p class="hero__lead">
            DeepSeek-V4 以百万级上下文、Agent 能力专项优化和开源权重，面向长代码库、复杂文档、研究档案与自动化工作流。
          </p>
          <div class="hero__cta" aria-label="主要操作">
            <a class="primary-link" href="https://api-docs.deepseek.com/zh-cn/news/news260424" target="_blank" rel="noreferrer">阅读官方公告</a>
            <span>API 模型名：<code>deepseek-v4-pro</code> / <code>deepseek-v4-flash</code></span>
          </div>
        </div>
      </section>

      <section id="context" class="coordinates" aria-label="DeepSeek V4 核心指标">
        <article v-for="item in coordinates" :key="item.label" class="coordinate-tile">
          <strong>{{ item.value }}</strong>
          <span>{{ item.label }}</span>
          <p>{{ item.note }}</p>
        </article>
      </section>

      <section class="field-note" aria-labelledby="field-title">
        <p class="field-note__quote">“百万上下文”最有价值的地方，不是变长本身，而是让模型少一点遗忘、多一点现场感。</p>
        <div class="field-note__body">
          <h2 id="field-title">一次提交完整材料</h2>
          <p>
            在旧流程里，长代码仓库、会议纪要、财报附件与工具日志往往需要被人工拆段、摘要、再拼接。V4 将 1M 上下文作为官方服务标配，并通过 DSA 稀疏注意力与 token 维度压缩降低长上下文成本，让“完整输入”更接近默认工作方式。
          </p>
        </div>
      </section>

      <section id="models" class="model-studio" aria-labelledby="model-title">
        <div class="model-studio__intro">
          <h2 id="model-title">
            <span>长上下文</span>
            <span>一快一强</span>
          </h2>
          <p>Pro 冲上限，Flash 跑规模。上下文窗口一致，按任务难度和调用成本选择。</p>
        </div>

        <div class="model-switch" role="tablist" aria-label="选择模型版本">
          <button
            type="button"
            :class="{ 'is-active': selectedModel === 'pro' }"
            role="tab"
            :aria-selected="selectedModel === 'pro'"
            @click="selectedModel = 'pro'"
          >
            Pro / 上限
          </button>
          <button
            type="button"
            :class="{ 'is-active': selectedModel === 'flash' }"
            role="tab"
            :aria-selected="selectedModel === 'flash'"
            @click="selectedModel = 'flash'"
          >
            Flash / 规模
          </button>
        </div>

        <article class="model-card">
          <div>
            <p class="model-card__eyebrow">{{ activeModel.tone }}</p>
            <h3>{{ activeModel.name }}</h3>
            <p>{{ activeModel.promise }}</p>
          </div>
          <ul class="model-card__points">
            <li v-for="point in activeModel.points" :key="point">{{ point }}</li>
          </ul>
          <dl class="price-strip">
            <div v-for="row in activeModel.price" :key="row[0]">
              <dt>{{ row[0] }}</dt>
              <dd>{{ row[1] }}</dd>
            </div>
          </dl>
        </article>
      </section>

      <section class="capability-wall" aria-labelledby="capability-title">
        <div class="capability-wall__intro">
          <div>
            <h2 id="capability-title">它被设计成<br />Agent 的工作台</h2>
            <p>把调用、工具、文档与长任务放在同一张桌面上，让模型不只回答，也能接续行动。</p>
          </div>
          <span>Agent-ready surface</span>
        </div>
        <ul>
          <li v-for="capability in capabilities" :key="capability">{{ capability }}</li>
        </ul>
      </section>

      <section id="api" class="api-board" aria-labelledby="api-title">
        <div class="api-board__copy">
          <h2 id="api-title">切换模型名，即可接入</h2>
          <p>
            Base URL 保持不变，同时支持 OpenAI ChatCompletions 与 Anthropic 格式。旧模型名 <code>deepseek-chat</code> 与 <code>deepseek-reasoner</code> 已进入兼容过渡期，将于 2026-07-24 停止使用。
          </p>
        </div>
        <pre class="code-window"><code>import OpenAI from 'openai'

const client = new OpenAI({
  baseURL: 'https://api.deepseek.com',
  apiKey: process.env.DEEPSEEK_API_KEY,
})

await client.chat.completions.create({
  model: 'deepseek-v4-pro',
  messages: [{ role: 'user', content: '阅读整个仓库并给出迁移方案' }],
  reasoning_effort: 'max',
})</code></pre>
      </section>

      <section class="source-panel" aria-label="资料来源与开源入口">
        <p>当上下文不再被切碎，问题会带着它的来路抵达模型；答案也不必只像一句回声，而可以像完整海图上的下一道航线。</p>
        <div>
          <a v-for="source in sources" :key="source.href" :href="source.href" target="_blank" rel="noreferrer">
            {{ source.label }}
          </a>
        </div>
      </section>
    </main>
  </div>
</template>
