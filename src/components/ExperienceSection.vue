<template>
  <section class="experience" aria-labelledby="experience-heading">
    <h2 id="experience-heading">Опыт работы</h2>
    <div class="experience__timeline" role="list">
      <div v-for="(item, idx) in experience" :key="idx" class="experience__item" role="listitem">
        <div class="experience__dot" aria-hidden="true"></div>
        <div class="experience__content">
          <div class="experience__header">
            <span class="experience__position" :aria-label="'Должность: ' + item.position">{{ item.position }}</span>
            <span class="experience__company" :aria-label="'Компания: ' + item.company">@ {{ item.company }}</span>
          </div>
          <div class="experience__period">{{ item.period }}</div>
          <div class="experience__desc">{{ item.desc }}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const experience = [
  {
    position: 'Frontend-разработчик',
    company: 'sez.us',
    period: 'Август 2024 — сейчас (10 мес.)',
    desc: 'Разработка современных SPA на Vue.js, внедрение CI/CD, оптимизация UX.'
  },
  {
    position: 'Full stack разработчик',
    company: 'fl.ru',
    period: 'Февраль 2023 — Август 2024 (1 г. 7 мес.)',
    desc: 'Создание и поддержка fullstack-приложений на C# и Vue.js, интеграция с REST API.'
  },
  {
    position: 'Директор по развитию',
    company: '3DВектор',
    period: 'Август 2018 — Февраль 2023 (4 г. 7 мес.)',
    desc: 'Управление командой, развитие новых направлений, внедрение цифровых решений.'
  },
  {
    position: 'Инженер по 3D-моделированию',
    company: '3DВектор',
    period: 'Январь 2016 — Июль 2018 (2 г. 7 мес.)',
    desc: '3D-моделирование, прототипирование, автоматизация процессов.'
  },
  {
    position: 'Директор филиала',
    company: 'Ассистент',
    period: 'Июнь 2009 — Декабрь 2012 (3 г. 7 мес.)',
    desc: 'Организация работы филиала, управление персоналом.'
  },
  {
    position: 'Юрист по корпоративному сопровождению',
    company: 'Первая юридическая компания',
    period: 'Февраль 2007 — Июнь 2009 (2 г. 5 мес.)',
    desc: 'Юридическое сопровождение бизнеса, договорная работа.'
  }
]
</script>

<style scoped>
.experience {
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
.experience h2 {
  font-size: 2rem;
  margin-bottom: 2.2rem;
  color: #fff;
  text-align: center;
  text-shadow: 0 2px 12px #232a3bcc, 0 0 8px #65d6ff99;
}
.experience__timeline {
  position: relative;
  margin-left: 1.5rem;
  padding-left: 1.5rem;
  border-left: 3px solid #65d6ff;
}
.experience__item {
  position: relative;
  margin-bottom: 2.5rem;
  animation: fadeInUp 0.7s cubic-bezier(.4,0,.2,1);
}
.experience__dot {
  position: absolute;
  left: -1.7rem;
  top: 0.5rem;
  width: 1.2rem;
  height: 1.2rem;
  background: #65d6ff;
  border-radius: 50%;
  border: 3px solid #fff;
  box-shadow: 0 0 0 2px #65d6ff33;
}
.experience__content {
  background: rgba(255,255,255,0.13);
  border-radius: 1rem;
  box-shadow: 0 2px 8px #65d6ff22;
  padding: 1.2rem 1.5rem;
  margin-bottom: 0.5rem;
  color: #fff;
}
.experience__header {
  font-weight: 600;
  font-size: 1.1rem;
  margin-bottom: 0.2rem;
}
.experience__position {
  color: #65d6ff;
}
.experience__company {
  color: #fff;
  margin-left: 0.5em;
}
.experience__period {
  font-size: 0.95rem;
  color: #b3e6ff;
  margin-bottom: 0.5rem;
}
.experience__desc {
  font-size: 1rem;
  color: #fff;
}
@media (max-width: 600px) {
  .experience {
    padding: 2rem 1.2rem 1.5rem 1.2rem;
  }
  .experience__content {
    padding: 0.8rem 0.7rem;
  }
  .experience__timeline {
    margin-left: 0.7rem;
    padding-left: 0.7rem;
  }
}
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}
</style> 