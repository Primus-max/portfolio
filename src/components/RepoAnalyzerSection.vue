<template>
  <section class="repo-analyzer" aria-labelledby="repo-analyzer-heading">
    <h2 id="repo-analyzer-heading">AI-анализатор репозитория</h2>
    <div class="repo-analyzer__coming-soon">
      🚧 <b>Фича в разработке / Coming soon!</b>
    </div>
    <p class="repo-analyzer__desc">
      Вставьте ссылку на публичный GitHub-репозиторий — и получите AI-резюме по стеку, качеству кода, тестам, документации и CI/CD. Это поможет быстро оценить проект, навыки автора и зрелость разработки. <br>
      <span style="color:#65d6ff">В будущем будет работать на реальных данных!</span>
    </p>
    <form class="repo-analyzer__form" @submit.prevent="analyzeRepo">
      <input v-model="repoUrl" type="url" placeholder="Вставьте ссылку на GitHub-репозиторий" required />
      <button type="submit">Анализировать</button>
    </form>
    <transition name="fade">
      <div v-if="result" class="repo-analyzer__result">
        <h3>📝 Резюме проекта</h3>
        <p><b>Проект:</b> {{ result.project }}</p>
        <p><b>Навыки:</b> <span v-for="skill in result.skills" :key="skill" class="repo-analyzer__skill">{{ skill }}</span></p>
        <p><b>Чистота кода:</b> {{ result.codeQuality }}/10</p>
        <p><b>Документация:</b> {{ result.docs }}</p>
        <p><b>Тесты:</b> {{ result.tests }}</p>
        <p><b>CI/CD:</b> {{ result.cicd }}</p>
        <p><b>AI-заметка:</b> {{ result.aiNote }}</p>
        <button @click="downloadReport">Скачать отчёт</button>
      </div>
    </transition>
  </section>
</template>

<script setup>
import { ref } from 'vue';

const repoUrl = ref('')
const result = ref(null)

function analyzeRepo() {
  // Мок-данные, имитируем анализ
  result.value = {
    project: repoUrl.value.split('/').pop() || 'Demo Project',
    skills: ['TypeScript', 'Vue 3', 'Vite', 'Jest', 'Docker'],
    codeQuality: 8.5,
    docs: 'README, JSDoc, Storybook',
    tests: 'Покрытие 72%, e2e и unit',
    cicd: 'GitHub Actions, линтеры, автотесты',
    aiNote: 'Код структурирован, используются современные практики, хорошее покрытие тестами. Рекомендуется добавить больше e2e-тестов.'
  }
}

function downloadReport() {
  if (!result.value) return;
  const text = `# AI-анализ репозитория\n\n- **Проект:** ${result.value.project}\n- **Навыки:** ${result.value.skills.join(', ')}\n- **Чистота кода:** ${result.value.codeQuality}/10\n- **Документация:** ${result.value.docs}\n- **Тесты:** ${result.value.tests}\n- **CI/CD:** ${result.value.cicd}\n- **AI-заметка:** ${result.value.aiNote}`;
  const blob = new Blob([text], { type: 'text/markdown' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = `repo-analysis-${result.value.project}.md`;
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
}
</script>

<style scoped>
.repo-analyzer {
  max-width: 700px;
  margin: 0 auto 3rem auto;
  padding: 2.5rem 1rem 2rem 1rem;
  background: rgba(255,255,255,0.13);
  border-radius: 1.5rem;
  box-shadow: 0 8px 32px 0 rgba(31,38,135,0.18);
  backdrop-filter: blur(18px) saturate(180%);
  border: 1.5px solid rgba(255,255,255,0.25);
  position: relative;
  z-index: 1;
  text-align: center;
}
.repo-analyzer h2 {
  font-size: 2rem;
  margin-bottom: 2.2rem;
  color: #fff;
  text-align: center;
  text-shadow: 0 2px 12px #232a3bcc, 0 0 8px #65d6ff99;
}
.repo-analyzer__form {
  display: flex;
  gap: 1rem;
  justify-content: center;
  margin-bottom: 2rem;
}
.repo-analyzer__form input {
  padding: 0.7em 1.2em;
  border-radius: 1em;
  border: 1.5px solid #65d6ff44;
  font-size: 1rem;
  width: 340px;
  max-width: 100%;
}
.repo-analyzer__form button {
  padding: 0.7em 1.7em;
  border-radius: 2em;
  background: linear-gradient(90deg, #65d6ff 0%, #ff7eb3 100%);
  color: #fff;
  font-weight: 600;
  font-size: 1rem;
  border: none;
  box-shadow: 0 2px 8px #3a7bd522;
  transition: background 0.2s;
}
.repo-analyzer__form button:hover {
  background: linear-gradient(90deg, #ff7eb3 0%, #65d6ff 100%);
}
.repo-analyzer__result {
  background: rgba(255,255,255,0.98);
  color: #232a3b;
  border-radius: 1.2rem;
  box-shadow: 0 4px 18px 0 #65d6ff33;
  padding: 2rem 1.5rem 1.5rem 1.5rem;
  margin: 0 auto;
  max-width: 480px;
  text-align: left;
  animation: fadeInUp 0.7s cubic-bezier(.4,0,.2,1);
}
.repo-analyzer__result h3 {
  color: #65d6ff;
  margin-bottom: 1.2rem;
  text-align: center;
}
.repo-analyzer__skill {
  display: inline-block;
  background: linear-gradient(90deg, #65d6ff22 0%, #ff7eb322 100%);
  color: #181c2a;
  font-weight: 600;
  border-radius: 1.2em;
  padding: 0.35em 1.1em;
  font-size: 1rem;
  margin: 0 0.3em 0.3em 0;
}
.repo-analyzer__result button {
  margin-top: 1.5rem;
  padding: 0.7em 1.7em;
  border-radius: 2em;
  background: linear-gradient(90deg, #65d6ff 0%, #ff7eb3 100%);
  color: #fff;
  font-weight: 600;
  font-size: 1rem;
  border: none;
  box-shadow: 0 2px 8px #3a7bd522;
  transition: background 0.2s;
  display: block;
  width: 100%;
}
.repo-analyzer__result button:hover {
  background: linear-gradient(90deg, #ff7eb3 0%, #65d6ff 100%);
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.18s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}
.repo-analyzer__coming-soon {
  background: linear-gradient(90deg, #ffd86b 0%, #ff7eb3 100%);
  color: #232a3b;
  font-weight: 700;
  border-radius: 1em;
  padding: 0.5em 1.2em;
  margin-bottom: 1.2em;
  display: inline-block;
  font-size: 1.1em;
  box-shadow: 0 2px 8px #ffd86b44;
}
.repo-analyzer__desc {
  color: #fff;
  font-size: 1.08em;
  margin-bottom: 2em;
  opacity: 0.93;
}
</style> 