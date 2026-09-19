<script setup>
import { ref } from 'vue'
import ContactForm from './components/ContactForm.vue'

const isMenuOpen = ref(false)
const currentYear = new Date().getFullYear()

const benefits = [
  { number: '01', title: 'Вас услышат', text: 'Без осуждения и готовых советов — с вниманием к вашей ситуации и чувствам.' },
  { number: '02', title: 'Появится ясность', text: 'Разберём, что происходит в отношениях и на что вы действительно можете повлиять.' },
  { number: '03', title: 'Будет план действий', text: 'Найдём бережные шаги, которые помогут вернуть в семью спокойствие и близость.' },
]

const steps = [
  ['01', 'Знакомимся', 'Вы рассказываете, что происходит сейчас и чего хотите достичь.'],
  ['02', 'Разбираем ситуацию', 'Смотрим на отношения без обвинений и ищем точку, с которой можно начать.'],
  ['03', 'Выбираем шаги', 'В конце у вас есть понимание, что делать дальше и как поддержать себя.'],
]

const testimonials = [
  { text: 'После разговора я впервые увидела, что у ситуации есть решение. Появились силы и спокойствие.', name: 'Елена', role: 'жена и мама', image: '/images/avatar-1.webp' },
  { text: 'Симона умеет слушать и задавать очень точные вопросы. Я стала лучше понимать себя и мужа.', name: 'Иванка', role: 'клиентка', image: '/images/avatar-2.webp' },
  { text: 'Наши отношения с дочкой мужа стали теплее. Спасибо за бережный и понятный подход.', name: 'Анна', role: 'предприниматель', image: '/images/avatar-3.webp' },
]

const resources = [
  { title: 'Курсы', text: 'Практические материалы для самостоятельной работы с отношениями.', image: '/images/news.webp', href: '#booking', action: 'Узнать о курсе' },
  { title: 'Фото', text: 'Больше личных материалов и новостей — во ВКонтакте.', image: '/images/photo.webp', href: 'https://vk.com/id195803100?z=albums195803100', action: 'Открыть фото' },
  { title: 'Видео', text: 'Разговоры об отношениях на YouTube-канале Симоны.', image: '/images/video.webp', href: 'https://www.youtube.com/channel/UCOn_y5VfWGQrZL7cSwXvlCg', action: 'Смотреть видео' },
]

function closeMenu() {
  isMenuOpen.value = false
}
</script>

<template>
  <header class="site-header" :class="{ 'is-open': isMenuOpen }">
    <div class="container header-inner">
      <a class="brand" href="#top" aria-label="Симона Любимова — на главную" @click="closeMenu">
        <span class="brand-mark">С</span>
        <span><strong>Симона Любимова</strong><small>консультант по отношениям</small></span>
      </a>

      <button class="menu-toggle" type="button" :aria-expanded="isMenuOpen" aria-controls="main-nav" :aria-label="isMenuOpen ? 'Закрыть меню' : 'Открыть меню'" @click="isMenuOpen = !isMenuOpen" @keyup.esc="closeMenu">
        <span></span><span></span><span></span>
      </button>

      <nav id="main-nav" class="main-nav" :class="{ 'is-open': isMenuOpen }" aria-label="Основная навигация">
        <a href="#about-me" @click="closeMenu">Обо мне</a>
        <a href="#process" @click="closeMenu">Как проходит</a>
        <a href="#reviews" @click="closeMenu">Отзывы</a>
        <a href="#price" @click="closeMenu">Стоимость</a>
        <a class="nav-cta" href="#booking" @click="closeMenu">Записаться</a>
      </nav>
    </div>
  </header>

  <main id="top">
    <section class="hero section-shell">
      <div class="container hero-grid">
        <div class="hero-content">
          <p class="eyebrow">Консультации онлайн · конфиденциально</p>
          <h1>Отношения в семье могут стать теплее</h1>
          <p class="hero-lead">Помогаю разобраться в чувствах, границах и отношениях с ребёнком партнёра — спокойно, бережно и без обвинений.</p>
          <div class="hero-actions">
            <a class="button button-primary" href="#booking">Записаться на консультацию</a>
            <a class="text-link" href="#process">Узнать, как всё проходит <span aria-hidden="true">→</span></a>
          </div>
          <div class="hero-note"><span class="status-dot"></span> Первая встреча — 60 минут в удобном онлайн-формате</div>
        </div>
        <div class="hero-visual">
          <div class="hero-orbit orbit-one"></div><div class="hero-orbit orbit-two"></div>
          <div class="portrait-card"><img src="/images/home-03.webp" alt="Симона Любимова" width="1600" height="416" fetchpriority="high" decoding="async" /></div>
          <div class="hero-quote">«Вы не обязаны справляться со всем в одиночку»</div>
        </div>
      </div>
      <div class="hero-bottom container"><span>Помощь для женщин, которые хотят сохранить близость и опору в семье</span><span class="scroll-hint">Листайте, чтобы узнать больше ↓</span></div>
    </section>

    <section class="section section-light" id="about">
      <div class="container narrow-heading"><p class="eyebrow">Если сейчас непросто</p><h2>Вы не плохая. Вы оказались в сложной ситуации</h2><p class="section-intro">Когда в семье появляется ребёнок от предыдущих отношений, меняется привычный уклад. Можно одновременно любить мужа, уставать, ревновать, испытывать вину и не понимать, как поступить правильно.</p></div>
      <div class="container benefits-grid">
        <article v-for="benefit in benefits" :key="benefit.number" class="benefit-card"><span class="card-number">{{ benefit.number }}</span><h3>{{ benefit.title }}</h3><p>{{ benefit.text }}</p></article>
      </div>
    </section>

    <section class="section section-sand" id="process">
      <div class="container process-grid">
        <div><p class="eyebrow">Без давления и оценок</p><h2>Как проходит консультация</h2><p class="section-intro">Моя задача — помочь вам увидеть свою ситуацию яснее и вернуть ощущение опоры. Мы двигаемся в вашем темпе и говорим о том, что важно именно вам.</p><a class="button button-dark" href="#booking">Выбрать время</a></div>
        <div class="steps-list"><article v-for="step in steps" :key="step[0]" class="step-item"><span class="step-number">{{ step[0] }}</span><div><h3>{{ step[1] }}</h3><p>{{ step[2] }}</p></div></article></div>
      </div>
    </section>

    <section class="section section-white" id="reviews">
      <div class="container narrow-heading centered"><p class="eyebrow">Слова клиентов</p><h2>Изменения начинаются с честного разговора</h2></div>
      <div class="container reviews-grid"><article v-for="review in testimonials" :key="review.name" class="review-card"><span class="quote-mark" aria-hidden="true">“</span><p>{{ review.text }}</p><div class="review-author"><img :src="review.image" :alt="`Фото ${review.name}`" width="50" height="50" loading="lazy" decoding="async" /><span><strong>{{ review.name }}</strong><small>{{ review.role }}</small></span></div></article></div>
    </section>

    <section class="section resources-section">
      <div class="container narrow-heading centered"><p class="eyebrow">Полезные материалы</p><h2>Продолжайте знакомство</h2></div>
      <div class="container resources-grid"><article v-for="resource in resources" :key="resource.title" class="resource-card"><img :src="resource.image" :alt="resource.title" width="153" height="151" loading="lazy" decoding="async" /><div><h3>{{ resource.title }}</h3><p>{{ resource.text }}</p><a class="text-link" :href="resource.href" :target="resource.href.startsWith('http') ? '_blank' : undefined" :rel="resource.href.startsWith('http') ? 'noopener noreferrer' : undefined">{{ resource.action }} <span aria-hidden="true">→</span></a></div></article></div>
    </section>

    <section id="about-me" class="section section-cream about-section">
      <div class="container about-grid"><div class="about-photo"><img src="/images/home-03.webp" srcset="/images/home-03-mobile.webp 900w, /images/home-03.webp 1600w" sizes="(max-width: 700px) calc(100vw - 36px), 560px" alt="Симона Любимова консультирует онлайн" width="1600" height="416" loading="lazy" decoding="async" /></div><div class="about-copy"><p class="eyebrow">Обо мне</p><h2>Я знаю, как непросто принять новую семейную реальность</h2><p>Когда-то я сама строила отношения с ребёнком мужа от первого брака. Мне понадобились годы, чтобы понять, как сохранить уважение к себе, близость с мужем и доверие ребёнка.</p><p>Теперь я помогаю женщинам проходить этот путь бережнее: замечать свою зону влияния, говорить о чувствах и постепенно менять атмосферу дома.</p><a class="text-link" href="#booking">Поговорить о вашей ситуации <span aria-hidden="true">→</span></a></div></div>
    </section>

    <section class="section section-sage" id="price">
      <div class="container price-grid"><div><p class="eyebrow">Формат работы</p><h2>Всё прозрачно с самого начала</h2><p class="section-intro">Разовая консультация помогает разложить ситуацию по полочкам. Если понадобится длительная работа, формат и стоимость мы обсудим отдельно.</p></div><div class="price-card"><span class="price-label">Онлайн-консультация</span><strong>3 200 ₽</strong><span>60 минут · Skype или другой удобный формат</span><a class="button button-primary" href="#booking">Записаться</a></div></div>
    </section>

    <section class="section section-light" id="booking">
      <div class="container form-section-grid"><div class="form-copy"><p class="eyebrow">Первый шаг</p><h2>Запишитесь на консультацию</h2><p class="section-intro">Оставьте контакты и несколько слов о ситуации. Я отвечу, чтобы согласовать время и формат встречи.</p><ul class="check-list"><li>Конфиденциальный разговор онлайн</li><li>Без оценок, давления и готовых шаблонов</li><li>Конкретные шаги по итогам встречи</li></ul></div><ContactForm kind="booking" /></div>
    </section>

    <section class="section question-section" id="question"><div class="container question-grid"><div><p class="eyebrow">Остались вопросы?</p><h2>Напишите мне</h2><p>Если вы пока не готовы к консультации, можно начать с короткого вопроса.</p></div><ContactForm kind="question" /></div></section>
  </main>

  <footer class="site-footer"><div class="container footer-inner"><a class="brand" href="#top"><span class="brand-mark">С</span><span><strong>Симона Любимова</strong><small>консультант по отношениям</small></span></a><div class="footer-contact">Skype: <strong>simona7997</strong><br /><a href="https://www.youtube.com/channel/UCOn_y5VfWGQrZL7cSwXvlCg" target="_blank" rel="noopener noreferrer">YouTube-канал →</a></div><small>© {{ currentYear }} Симона Любимова</small></div></footer>
</template>
