<template>
  <section class="projects" aria-labelledby="projects-heading">
    <h2 id="projects-heading">Проекты</h2>
    <div class="projects__list" role="list">
      <div v-for="(project, idx) in projects" :key="idx" class="projects__card" role="listitem" @mouseenter="hoverIdx = idx" @mouseleave="hoverIdx = null">
        <div class="projects__img" aria-hidden="true">
          <svg width="48" height="48" viewBox="0 0 48 48" fill="none">
            <circle cx="24" cy="24" r="24" :fill="project.color" fill-opacity="0.22"/>
            <text x="50%" y="55%" text-anchor="middle" fill="#fff" font-size="18" font-family="Manrope, Segoe UI, Arial" dy=".3em">{{ project.icon }}</text>
          </svg>
        </div>
        <div class="projects__info">
          <div class="projects__title">{{ project.title }}</div>
          <div class="project-badges">
            <span v-for="badge in project.badges" :key="badge" class="project-badge">{{ badge }}</span>
          </div>
          <div class="projects__desc">{{ project.desc }}</div>
          <div class="projects__links">
            <a v-if="project.demo" :href="project.demo" target="_blank" class="projects__link" :aria-label="'Demo проекта ' + project.title">Demo</a>
            <button v-else class="projects__link" @click="openPreview(project)" :aria-label="'Открыть предпросмотр проекта ' + project.title">Demo</button>
            <a v-if="project.github" :href="project.github" target="_blank" class="projects__link" :aria-label="'GitHub проекта ' + project.title">GitHub</a>
          </div>
        </div>
      </div>
    </div>
    <div v-if="showModal" class="projects__modal-backdrop" @click.self="closePreview" aria-modal="true" role="dialog">
      <div class="projects__modal-content">
        <h3>{{ modalProject.title }}</h3>
        <div class="projects__modal-img" aria-hidden="true">
          <svg width="220" height="120" viewBox="0 0 220 120" fill="none">
            <rect width="220" height="120" rx="18" :fill="modalProject.color" fill-opacity="0.18"/>
            <text x="50%" y="55%" text-anchor="middle" fill="#fff" font-size="32" font-family="Manrope, Segoe UI, Arial" dy=".3em">{{ modalProject.icon }}</text>
          </svg>
        </div>
        <div class="projects__modal-desc">{{ modalProject.desc }}</div>
        <button class="projects__modal-close" @click="closePreview" aria-label="Закрыть предпросмотр">Закрыть</button>
      </div>
    </div>
  </section>
</template>

<script setup>
import {
  ref,
  watch,
} from 'vue';

const projects = [
  {
    title: 'Avatar.AI',
    desc: 'Платформа для создания, управления и интеграции цифровых личностей (аватаров) с AI, VR/AR и блокчейном.',
    demo: 'https://primus-max.github.io/avatar.ai/',
    github: 'https://github.com/Primus-max/avatar.ai',
    badges: ['Vue 3', 'Vuetify 3', 'Node.js', 'GraphQL', 'TensorFlow.js', 'OpenAI API', 'Ethereum', 'WebXR', 'Three.js'],
    color: '#232a3b',
    icon: 'AI'
  },
  {
    title: 'Netmax',
    desc: 'Многофункциональное десктопное приложение на Electron для управления сетевыми задачами, автоматизации и мониторинга.',
    demo: '',
    github: 'https://github.com/Primus-max/Netmax',
    badges: ['JavaScript', 'Electron', 'HTML', 'CSS'],
    color: '#2a1e3d',
    icon: 'NM'
  },
  {
    title: 'StaticRustLauncher',
    desc: 'Минималистичный лаунчер для запуска Rust-серверов с удобным интерфейсом и статической сборкой.',
    demo: '',
    github: 'https://github.com/Primus-max/StaticRustLauncher',
    badges: ['C#', '.NET', 'WPF'],
    color: '#1e3d2a',
    icon: 'SRL'
  },
  {
    title: 'PatternReformatter',
    desc: 'Утилита для форматирования и преобразования текстовых паттернов с поддержкой регулярных выражений.',
    demo: '',
    github: 'https://github.com/Primus-max/PatternReformatter',
    badges: ['C#', '.NET', 'WinForms'],
    color: '#3d2a1e',
    icon: 'PR'
  },
  {
    title: 'CryptoApp',
    desc: 'Приложение для шифрования и дешифрования данных с поддержкой различных алгоритмов.',
    demo: '',
    github: 'https://github.com/Primus-max/CryptoApp',
    badges: ['C#', '.NET', 'WPF'],
    color: '#1e2a3d',
    icon: 'CA'
  }
]
const hoverIdx = ref(null)
const showModal = ref(false)
const modalProject = ref({})
function openPreview(project) {
  modalProject.value = project
  showModal.value = true
}
function closePreview() {
  showModal.value = false
}
// Блокировка скролла body при открытии модалки
watch(showModal, (val) => {
  if (val) {
    document.body.style.overflow = 'hidden';
  } else {
    document.body.style.overflow = '';
  }
})
</script>

<style scoped>
.projects {
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
.projects h2 {
  font-size: 2rem;
  margin-bottom: 2.2rem;
  color: #fff;
  text-shadow: 0 2px 12px #232a3bcc, 0 0 8px #65d6ff99;
  text-align: center;
}
.projects__list {
  display: flex;
  flex-wrap: wrap;
  gap: 2.2rem;
  justify-content: center;
}
.projects__card {
  background: rgba(30,34,54,0.92);
  border-radius: 1.2rem;
  box-shadow: 0 4px 24px #65d6ff22;
  border: 2.5px solid rgba(101,214,255,0.18);
  padding: 1.5rem 1.2rem 1.2rem 1.2rem;
  width: 290px;
  display: flex;
  flex-direction: column;
  align-items: stretch;
  transition: transform 0.18s cubic-bezier(.4,0,.2,1), box-shadow 0.18s, border 0.18s, box-shadow 0.18s;
  cursor: pointer;
  animation: fadeInUp 0.7s cubic-bezier(.4,0,.2,1);
  position: relative;
  z-index: 1;
}
.projects__card:hover {
  transform: translateY(-8px) scale(1.04);
  box-shadow: 0 8px 32px #65d6ff44, 0 0 16px 2px #65d6ff99;
  border: 2.5px solid #65d6ff;
}
.projects__img {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  margin-bottom: 1.1rem;
  align-self: center;
  background: none;
  display: flex;
  align-items: center;
  justify-content: center;
}
.projects__info {
  display: flex;
  flex-direction: column;
  gap: 0.7rem;
}
.projects__title {
  font-size: 1.15rem;
  font-weight: 700;
  color: #65d6ff;
  margin-bottom: 0.2rem;
}
.project-badges {
  margin: 0.7em 0 0.2em 0;
  display: flex;
  flex-wrap: wrap;
  gap: 0.4em;
}
.project-badge {
  background: #e3f0ff;
  color: #232a3b;
  border-radius: 1em;
  padding: 0.2em 0.9em;
  font-size: 0.95em;
  font-weight: 600;
  letter-spacing: 0.01em;
}
.projects__desc {
  font-size: 1rem;
  color: #fff;
  min-height: 48px;
  opacity: 0.97;
}
.projects__links {
  display: flex;
  gap: 1.2rem;
  margin-top: 0.5rem;
}
.projects__link {
  color: #65d6ff;
  font-weight: 600;
  text-decoration: none;
  transition: color 0.18s, text-decoration 0.18s;
  background: none;
  border: none;
  font-size: 1rem;
  cursor: pointer;
  padding: 0;
}
.projects__link:hover {
  color: #ff7eb3;
  text-decoration: underline;
}
/* Modal styles */
.projects__modal-backdrop {
  position: fixed;
  inset: 0;
  z-index: 1000;
  background: rgba(20,24,34,0.82);
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  width: 100vw;
  transition: background 0.25s;
  overflow: hidden;
}
.projects__modal-content {
  background: rgba(30,34,54,0.98);
  border-radius: 1.2rem;
  box-shadow: 0 8px 32px #65d6ff44;
  padding: 2.2rem 2.2rem 1.5rem 2.2rem;
  min-width: 320px;
  max-width: 480px;
  width: 100%;
  min-height: 320px;
  text-align: center;
  color: #fff;
  animation: fadeInUp 0.5s cubic-bezier(.4,0,.2,1);
  margin: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  word-break: break-word;
  white-space: normal;
}
.projects__modal-img {
  margin: 1.2rem auto 1.2rem auto;
}
.projects__modal-desc {
  font-size: 1.1rem;
  margin-bottom: 1.5rem;
  color: #fff;
}
.projects__modal-close {
  background: linear-gradient(90deg, #65d6ff 0%, #ff7eb3 100%);
  color: #fff;
  border: none;
  border-radius: 2em;
  padding: 0.7em 1.7em;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.2s;
}
.projects__modal-close:hover {
  background: linear-gradient(90deg, #ff7eb3 0%, #65d6ff 100%);
}
@media (max-width: 900px) {
  .projects__list {
    gap: 1.2rem;
  }
  .projects__card {
    width: 98vw;
    max-width: 340px;
    padding: 1.1rem 0.7rem 1rem 0.7rem;
  }
}
@media (max-width: 600px) {
  .projects {
    padding: 2rem 1.2rem 1.5rem 1.2rem;
  }
  .projects__info {
    padding: 0;
  }
  .projects__modal-content {
    padding: 1.2rem 0.7rem 1rem 0.7rem;
    min-width: 0;
    max-width: 98vw;
  }
}
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}
</style> 