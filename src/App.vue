<script setup>
import { reactive, ref } from 'vue'

const dishes = [
  {
    category: 'SEASONAL SPECIAL',
    name: '陈皮炭烤乳鸽',
    image: 'https://images.unsplash.com/photo-1547592180-85f173990554?auto=format&fit=crop&w=1000&q=80',
  },
  {
    category: 'FROM THE RIVER',
    name: '清蒸黄鱼',
    image: 'https://images.unsplash.com/photo-1569718212165-3a8278d5f624?auto=format&fit=crop&w=900&q=80',
  },
  {
    category: 'GARDEN HARVEST',
    name: '松露时蔬',
    image: 'https://images.unsplash.com/photo-1504674900247-0877df9cc836?auto=format&fit=crop&w=900&q=80',
  },
]

const reservation = reactive({ name: '', phone: '', date: '', guests: '' })
const submitted = ref(false)

function submitReservation() {
  submitted.value = true
}
</script>

<template>
  <nav class="nav" aria-label="主导航">
    <a class="brand" href="#top">兰亭</a>
    <div class="links">
      <a href="#story">关于我们</a>
      <a href="#menu">当季菜单</a>
      <a href="#visit">到访兰亭</a>
      <a class="booking" href="#reserve">在线预订</a>
    </div>
  </nav>

  <main id="top">
    <section class="hero" aria-labelledby="hero-title">
      <div class="hero-content">
        <div class="eyebrow">LANTING · SHANGHAI</div>
        <h1 id="hero-title">一席风土，<br />四时入味</h1>
        <p>从江南的晨雾到餐桌上的一盏暖茶，以当代手法重新演绎熟悉的中国滋味。</p>
        <a class="button" href="#reserve">预订餐席 <span aria-hidden="true">→</span></a>
      </div>
      <div class="scroll">向下探索</div>
    </section>

    <section id="story" class="intro" aria-labelledby="story-title">
      <div class="section-label">OUR PHILOSOPHY</div>
      <div>
        <h2 id="story-title">一席雅叙，<br />尽兴相逢。</h2>
        <p>兰亭想做的，是一张让人愿意久坐的餐桌。这里有刚出锅的热气、有惦记着你口味的用心，也有把日常说成故事的时间。愿每一次举杯与夹菜，都能让你和身边的人，感到被好好招待。</p>
      </div>
    </section>

    <section id="menu" class="signature" aria-labelledby="menu-title">
      <div class="section-top">
        <h2 id="menu-title">当季精选</h2>
        <a class="more" href="#reserve">查看完整菜单 →</a>
      </div>
      <div class="dishes">
        <article
          v-for="dish in dishes"
          :key="dish.name"
          class="dish"
          :style="{ '--dish-image': `url('${dish.image}')` }"
        >
          <div class="dish-copy">
            <small>{{ dish.category }}</small>
            <h3>{{ dish.name }}</h3>
          </div>
        </article>
      </div>
    </section>

    <section id="reserve" class="reserve" aria-labelledby="reserve-title">
      <div>
        <div class="section-label">MAKE A RESERVATION</div>
        <h2 id="reserve-title">留一张桌，<br />等一场相聚。</h2>
        <p>每日 11:30 – 14:00 · 17:30 – 22:00<br />上海市静安区南阳路 188 号</p>
      </div>
      <form class="form" @submit.prevent="submitReservation">
        <input v-model="reservation.name" aria-label="姓名" required placeholder="您的姓名" />
        <input v-model="reservation.phone" aria-label="电话" required placeholder="联系电话" />
        <select v-model="reservation.date" aria-label="日期" required>
          <option disabled value="">选择日期</option>
          <option>2026 年 8 月 3 日</option>
          <option>2026 年 8 月 4 日</option>
          <option>2026 年 8 月 5 日</option>
        </select>
        <select v-model="reservation.guests" aria-label="人数" required>
          <option disabled value="">用餐人数</option>
          <option>2 位</option>
          <option>4 位</option>
          <option>6 位及以上</option>
        </select>
        <button class="button" type="submit">
          {{ submitted ? '预订已提交 ✓' : '确认预订' }}
          <span v-if="!submitted" aria-hidden="true">→</span>
        </button>
        <p v-if="submitted" class="success" role="status">已收到您的预订需求，我们将尽快与您确认。</p>
      </form>
    </section>
  </main>

  <footer id="visit">
    <strong>兰亭</strong>
    <span>© 2026 LANTING RESTAURANT</span>
    <span>021 · 6868 1888</span>
  </footer>
</template>
