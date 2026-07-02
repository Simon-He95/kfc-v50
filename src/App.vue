<script setup>
import { computed, onMounted, ref } from 'vue'

const methods = [
  {
    id: 'alipay',
    label: '支付宝',
    tone: 'blue',
    image: '/pay/zhifubao-qr.jpg',
    note: '蓝色通道，适合嘴上说下次其实现在就付的人。',
    guide: ['手机直接扫屏幕上的码，或者打开大码后保存。', '微信里会拦支付宝，别硬点跳转。'],
    wechatGuide: ['点右上角在浏览器打开，再用支付宝扫。', '懒得切浏览器就截图，打开支付宝扫一扫，从相册选这张图。'],
  },
  {
    id: 'wechat',
    label: '微信',
    tone: 'green',
    image: '/pay/weixin-qr-clean.jpg',
    note: '绿色通道，适合把人情世故伪装成扫码的人。',
    guide: ['用微信扫一扫识别这张码。', '如果当前页识别失败，就截图后从扫一扫相册里选。'],
    wechatGuide: ['微信网页里点图片会提示暂不支持跳转，别点。', '截图这张码，回微信首页点 +，扫一扫，从相册选截图。'],
  },
]

const cravings = [
  {
    title: '刚出锅原味鸡',
    image: '/food/fried-chicken-plate.jpg',
    alt: '一盘金黄色炸鸡',
    copy: '外皮咔嚓，理智撤退。',
  },
  {
    title: '炸鸡山脉',
    image: '/food/fried-chicken-table.jpg',
    alt: '铺在叶子上的炸鸡',
    copy: '热气一上来，余额就装死。',
  },
]

const selectedId = ref('alipay')
const isWeChatBrowser = ref(false)
const selected = computed(() => methods.find((method) => method.id === selectedId.value))
const activeGuide = computed(() => (isWeChatBrowser.value ? selected.value.wechatGuide : selected.value.guide))

onMounted(() => {
  isWeChatBrowser.value = /MicroMessenger/i.test(window.navigator.userAgent)
})
</script>

<template>
  <main class="page-shell">
    <div class="intro-splash" aria-hidden="true">
      <div class="intro-stripes"></div>
      <div class="intro-burst">
        <img src="/food/fried-chicken-plate.jpg" alt="" />
        <span class="steam steam-one"></span>
        <span class="steam steam-two"></span>
        <span class="steam steam-three"></span>
        <span class="oil-pop oil-one"></span>
        <span class="oil-pop oil-two"></span>
        <span class="oil-pop oil-three"></span>
      </div>
      <div class="intro-copy">
        <span>开锅</span>
        <strong>KFC V50</strong>
        <span>火力正酣</span>
      </div>
    </div>

    <nav class="topbar" aria-label="主导航">
      <a class="brand" href="#top" aria-label="KFC V50 首页">
        <span class="brand-mark">V50</span>
        <span>KFC Thursday</span>
      </a>
      <div class="nav-links" aria-label="页面锚点">
        <a href="#menu">菜单</a>
        <a href="#pay">扫码</a>
        <a href="#fineprint">规矩</a>
      </div>
      <a class="topbar-action" href="#pay">开饭</a>
    </nav>

    <section id="top" class="hero-section" aria-labelledby="hero-title">
      <div class="hero-copy">
        <p class="hero-kicker">疯狂星期四民间急救站</p>
        <h1 id="hero-title">KFC V50</h1>
        <p class="hero-text">扫码投喂 50，嘴硬可围观。</p>
        <div class="hero-actions">
          <a class="primary-action" href="#pay">立刻投喂</a>
          <a class="secondary-action" href="#menu">先看借口</a>
        </div>
      </div>

      <aside class="deal-board" aria-label="今日 V50 套餐">
        <div class="deal-board-inner">
          <p class="deal-label">TODAY'S DAMAGE</p>
          <div class="deal-price">
            <span>50</span>
            <small>RMB</small>
          </div>
          <p class="deal-name">吮指原味人情债</p>
          <p class="deal-copy">付款不保证爱情，只保证我今天少饿一顿。</p>
          <div class="hot-preview" aria-label="热腾腾炸鸡预览">
            <img src="/food/fried-chicken-plate.jpg" alt="热腾腾炸鸡" />
            <span class="steam steam-one" aria-hidden="true"></span>
            <span class="steam steam-two" aria-hidden="true"></span>
            <span class="steam steam-three" aria-hidden="true"></span>
          </div>
        </div>
      </aside>
    </section>

    <section id="menu" class="menu-section" aria-labelledby="menu-title">
      <div class="menu-copy">
        <p class="section-label">借口菜单</p>
        <h2 id="menu-title">今天不叫要钱，叫众筹炸鸡研究。</h2>
      </div>
      <div class="ticket-grid">
        <article class="ticket ticket-main">
          <span class="ticket-tag">主餐</span>
          <h3>V 我 50</h3>
          <p>你负责扫码，我负责把尊严打包带走。</p>
        </article>
        <article class="ticket">
          <span class="ticket-tag">配菜</span>
          <h3>精神股东席位</h3>
          <p>到账后默认获得今日嘴硬观察权。</p>
        </article>
        <article class="ticket">
          <span class="ticket-tag">饮料</span>
          <h3>冰镇良心</h3>
          <p>付款前有，付款后也不一定剩多少。</p>
        </article>
      </div>
    </section>

    <section class="crave-section" aria-labelledby="crave-title">
      <div class="crave-copy">
        <p class="section-label">热气攻击</p>
        <h2 id="crave-title">别看了，油香开大了。</h2>
      </div>
      <div class="crave-grid">
        <article v-for="item in cravings" :key="item.title" class="crave-card">
          <div class="crave-image-wrap">
            <img class="crave-image" :src="item.image" :alt="item.alt" loading="lazy" />
            <span class="steam steam-one" aria-hidden="true"></span>
            <span class="steam steam-two" aria-hidden="true"></span>
            <span class="steam steam-three" aria-hidden="true"></span>
            <span class="oil-pop oil-one" aria-hidden="true"></span>
            <span class="oil-pop oil-two" aria-hidden="true"></span>
            <span class="oil-pop oil-three" aria-hidden="true"></span>
          </div>
          <h3>{{ item.title }}</h3>
          <p>{{ item.copy }}</p>
        </article>
        <article class="crave-card bucket-card">
          <div class="bucket-visual" aria-label="全家桶幻觉">
            <img src="/food/fried-chicken-plate.jpg" alt="炸鸡全家桶视觉" loading="lazy" />
            <span class="bucket-rim" aria-hidden="true"></span>
            <span class="steam steam-one" aria-hidden="true"></span>
            <span class="steam steam-two" aria-hidden="true"></span>
            <span class="steam steam-three" aria-hidden="true"></span>
          </div>
          <h3>全家桶幻觉</h3>
          <p>桶还没到，口水先到账。</p>
        </article>
      </div>
    </section>

    <section id="pay" class="pay-section" aria-labelledby="pay-title">
      <div class="pay-panel">
        <div class="pay-content">
          <p class="section-label">扫码付款</p>
          <h2 id="pay-title">选一个顺手的码，别让鸡翅等冷。</h2>
          <p class="pay-note">
            网页只展示个人收款码，不会自动确认到账。付款结果以微信或支付宝 App 为准。
          </p>
          <p v-if="isWeChatBrowser" class="wechat-warning">
            你现在在微信里，外部支付跳转会被拦。按下面步骤走，别和微信硬刚。
          </p>

          <div class="method-tabs" role="tablist" aria-label="选择付款方式">
            <button
              v-for="method in methods"
              :key="method.id"
              class="method-tab"
              :class="{ active: selectedId === method.id }"
              type="button"
              role="tab"
              :aria-selected="selectedId === method.id"
              @click="selectedId = method.id"
            >
              {{ method.label }}
            </button>
          </div>

          <dl class="receipt-lines">
            <div>
              <dt>建议金额</dt>
              <dd>50.00</dd>
            </div>
            <div>
              <dt>付款备注</dt>
              <dd>疯狂星期四</dd>
            </div>
            <div>
              <dt>到账确认</dt>
              <dd>看你的 App</dd>
            </div>
          </dl>
        </div>

        <div class="qr-stage" :class="`tone-${selected.tone}`">
          <div class="qr-card">
            <div class="qr-card-top">
              <span>{{ selected.label }}</span>
              <span>扫码区</span>
            </div>
            <div class="qr-link">
              <img class="qr-image" :src="selected.image" :alt="`${selected.label}收款二维码`" />
            </div>
            <p>{{ selected.note }}</p>
            <ol class="pay-steps">
              <li v-for="step in activeGuide" :key="step">{{ step }}</li>
            </ol>
          </div>
          <p v-if="isWeChatBrowser" class="wechat-action-note">截图或长按保存这张码</p>
          <a v-else class="image-action" :href="selected.image" target="_blank" rel="noreferrer">
            打开大码
          </a>
        </div>
      </div>
    </section>

    <footer id="fineprint" class="site-footer">
      <p>非官方整活页面。没有接入微信或支付宝官方支付 API，也不会保存付款信息。</p>
      <p>浏览器负责展示二维码，付款这口锅交给支付 App。</p>
    </footer>
  </main>
</template>
