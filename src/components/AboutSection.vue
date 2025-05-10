<template>
  <section class="about" aria-labelledby="about-heading">
    <h2 id="about-heading">О себе</h2>
    <div class="about__main">
      <div class="about__bio">
        <p class="about__text">
          Fullstack-разработчик с опытом 2+ года в коммерческой разработке. Специализируюсь на C# (.NET, ASP.NET Core) и Vue.js, с глубоким пониманием архитектуры приложений, производительности и качества кода.<br><br>
          Люблю разбираться в сложных задачах, находить оптимальные решения и улучшать существующие процессы. Постоянно изучаю новые технологии и следую лучшим практикам разработки. Умею и люблю рефакторить, декомпозировать и оптимизировать код.
        </p>
        <ul class="about__list" role="list">
          <li role="listitem"><span class="about__icon" aria-hidden="true">🎯</span> Цели: Делать сложное простым, развиваться как Middle Fullstack-разработчик, создавать масштабируемые и производительные решения.</li>
          <li role="listitem"><span class="about__icon" aria-hidden="true">🚀</span> Стремления: Постоянное обучение, следование лучшим практикам, автоматизация процессов.</li>
          <li role="listitem"><span class="about__icon" aria-hidden="true">💡</span> Ценности: Чистый код, командная работа, ответственность, баланс качества и времени.</li>
        </ul>
      </div>
      <div class="about__hobbies">
        <div class="about__hobby-card" tabindex="0" aria-label="Спорт: Дисциплина, работа в команде, стрессоустойчивость.">
          <span class="about__hobby-icon" aria-hidden="true">💪</span>
          <span class="about__hobby-title">Спорт</span>
          <span class="about__hobby-desc">Дисциплина, работа в команде, стрессоустойчивость.</span>
        </div>
        <div class="about__hobby-card" tabindex="0" aria-label="Музыка: Творческий подход к задачам, вдохновение.">
          <span class="about__hobby-icon" aria-hidden="true">🎵</span>
          <span class="about__hobby-title">Музыка</span>
          <span class="about__hobby-desc">Творческий подход к задачам, вдохновение.</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// Мокаем данные, логика не требуется
</script>

<style scoped>
.about {
  max-width: 900px;
  margin: 0 auto 3rem auto;
  padding: 2.5rem 1rem 2rem 1rem;
  background: rgba(30,34,54,0.18);
  border-radius: 1.5rem;
  box-shadow: 0 8px 32px 0 rgba(31,38,135,0.18);
  backdrop-filter: blur(18px) saturate(180%);
  border: 1.5px solid rgba(255,255,255,0.25);
  position: relative;
  z-index: 1;
}
.about h2 {
  font-size: 2rem;
  margin-bottom: 2.2rem;
  color: #fff;
  text-align: center;
  text-shadow: 0 2px 12px #232a3bcc, 0 0 8px #65d6ff99;
}
.about__main {
  display: flex;
  gap: 2.5rem;
  justify-content: space-between;
  align-items: flex-start;
  flex-wrap: wrap;
}
.about__bio {
  flex: 2 1 320px;
  min-width: 220px;
}
.about__text {
  font-size: 1.1rem;
  color: #fff;
  margin-bottom: 1.2rem;
  opacity: 0.97;
}
.about__list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 0.7rem;
}
.about__icon {
  font-size: 1.3em;
  margin-right: 0.5em;
}
.about__hobbies {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 1.2rem;
  align-items: stretch;
  justify-content: center;
  width: 100%;
  box-sizing: border-box;
}
.about__hobby-card {
  flex: 1 1 220px;
  min-width: 220px;
  max-width: 320px;
  min-height: 180px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  color: #fff;
  font-size: 1rem;
  text-align: center;
  transition: box-shadow 0.18s, border 0.18s;
  background: rgba(255,255,255,0.13);
  border-radius: 1.2rem;
  box-shadow: 0 2px 8px #65d6ff22;
  border: 2px solid #65d6ff44;
  padding: 1.1rem 1.2rem;
  margin-bottom: 0;
}
.about__hobby-icon {
  font-size: 1.7em;
  margin-bottom: 0.2em;
}
.about__hobby-title {
  font-weight: 700;
  color: #65d6ff;
  margin-bottom: 0.1em;
}
.about__hobby-desc {
  font-size: 0.95em;
  color: #fff;
  opacity: 0.92;
  text-align: center;
}
@media (max-width: 900px) {
  .about__main {
    flex-direction: column;
    gap: 1.5rem;
    align-items: stretch;
  }
  .about__hobbies {
    flex-direction: row;
    gap: 1.2rem;
    align-items: flex-start;
    justify-content: flex-start;
  }
}
@media (max-width: 600px) {
  .about {
    padding: 2rem 1.2rem 1.5rem 1.2rem;
  }
  .about__main {
    gap: 1rem;
  }
  .about__hobbies {
    flex-direction: column;
    gap: 0.7rem;
    align-items: center;
    justify-content: center;
    flex-wrap: nowrap;
    width: 100%;
  }
  .about__hobby-card {
    width: 100%;
    max-width: 100%;
    min-width: 0;
    margin: 0 0 0.7rem 0;
    min-height: unset;
    padding: 0.5rem 0.7rem;
    font-size: 0.98rem;
    gap: 0.3rem;
  }
}
</style> 