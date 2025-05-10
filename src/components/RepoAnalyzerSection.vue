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
    <div class="repo-analyzer__mode-switch">
      <div class="switcher">
        <span :class="['switcher-label', {active: mode==='hr'}]">Для HR</span>
        <label class="switcher-toggle">
          <input type="checkbox" v-model="isDevMode">
          <span class="slider"></span>
        </label>
        <span :class="['switcher-label', {active: mode==='dev'}]">Для соискателя</span>
      </div>
    </div>
    <form class="repo-analyzer__form" @submit.prevent="analyzeRepo">
      <input v-model="repoUrl" type="url" placeholder="Вставьте ссылку на GitHub-репозиторий" required class="repo-analyzer__input" />
      <div class="repo-analyzer__hh-group">
        <input v-model="hhUrl" type="url" placeholder="Ссылка на вакансию hh.ru (опционально)" class="repo-analyzer__input" />
        <!-- <span class="repo-analyzer__hh-desc">Анализирует вакансию и !</span> -->
      </div>
      <template v-if="mode==='dev'">
        <select v-model="desiredPosition" class="repo-analyzer__input repo-analyzer__select">
          <option disabled value="">Желаемая позиция</option>
          <option>Junior Frontend</option>
          <option>Middle Frontend</option>
          <option>Senior Frontend</option>
          <option>Junior Backend</option>
          <option>Middle Backend</option>
          <option>Senior Backend</option>
          <option>Fullstack Developer</option>
          <option>DevOps Engineer</option>
          <option>QA Engineer</option>
          <option>Mobile Developer</option>
          <option>Data Engineer</option>
          <option>Другое...</option>
        </select>
        <input v-if="desiredPosition==='Другое...'" v-model="customPosition" type="text" placeholder="Введите свою позицию" class="repo-analyzer__input repo-analyzer__custom-input" />
      </template>
      <button type="submit" :disabled="isLoading" class="repo-analyzer__button repo-analyzer__analyze-btn" :class="{'repo-analyzer__button--loading': isLoading}">
        <span class="repo-analyzer__button-text" v-if="!isLoading">Анализировать</span>
        <span class="repo-analyzer__button-text" v-else>Анализирую...</span>
        <span v-if="isLoading" class="repo-analyzer__progress-bar" :style="{width: progress + '%'}"></span>
      </button>
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
        <div v-if="mode==='dev'" class="repo-analyzer__grade-block">
          <p><b>Грейд:</b> <span :class="'grade-badge grade-' + result.grade.toLowerCase()">{{ result.grade }}</span></p>
          <p><b>Рекомендация по позиции:</b> {{ result.positionAdvice }}</p>
          <p><b>Советы по прокачке:</b> {{ result.upgradeAdvice }}</p>
          <p v-if="finalPosition"> <b>Желаемая позиция:</b> {{ finalPosition }}<br>
            <span v-if="result.gradeAdvice">{{ result.gradeAdvice }}</span>
          </p>
          <div v-if="result.hhAnalysis" class="repo-analyzer__hh-block">
            <h4>{{ result.hhAnalysis.title }}</h4>
            <p><b>Требования:</b> {{ result.hhAnalysis.requirements }}</p>
            <p><b>Совпадение:</b> {{ result.hhAnalysis.match }}</p>
            <p><b>Советы:</b> {{ result.hhAnalysis.advice }}</p>
          </div>
        </div>
        <div v-if="mode==='hr'" class="repo-analyzer__hr-block">
          <p><b>Оценка для HR:</b> {{ result.hrSummary }}</p>
          <div v-if="result.hhAnalysis" class="repo-analyzer__hh-block">
            <h4>{{ result.hhAnalysis.title }}</h4>
            <p><b>Требования:</b> {{ result.hhAnalysis.requirements }}</p>
            <p><b>Совпадение:</b> {{ result.hhAnalysis.match }}</p>
            <p><b>Советы:</b> {{ result.hhAnalysis.advice }}</p>
          </div>
        </div>
        <button @click="downloadReport">Скачать отчёт</button>
      </div>
    </transition>
  </section>
</template>

<script setup>
import {
  computed,
  ref,
  watch,
} from 'vue';

const repoUrl = ref('')
const hhUrl = ref('')
const result = ref(null)
const isDevMode = ref(true)
const mode = computed(() => isDevMode.value ? 'dev' : 'hr')
const desiredPosition = ref('')
const customPosition = ref('')
const finalPosition = computed(() => desiredPosition.value === 'Другое...' ? customPosition.value : desiredPosition.value)

// --- Loading/progress state for Analyze button ---
const isLoading = ref(false)
const progress = ref(0)
let progressTimer = null

function startLoading(cb) {
  isLoading.value = true
  progress.value = 0
  // Animate progress bar
  const duration = 1600 // ms
  const steps = 32
  let step = 0
  clearInterval(progressTimer)
  progressTimer = setInterval(() => {
    step++
    progress.value = Math.min(100, Math.round((step / steps) * 100))
    if (step >= steps) {
      clearInterval(progressTimer)
      isLoading.value = false
      progress.value = 100
      cb && cb()
    }
  }, duration / steps)
}

function analyzeRepo() {
  startLoading(() => {
    // Мок-данные, имитируем анализ
    const pos = finalPosition.value;
    if (mode.value === 'dev') {
      const grade = 'Middle';
      result.value = {
        project: repoUrl.value.split('/').pop() || 'Demo Project',
        skills: ['TypeScript', 'Vue 3', 'Vite', 'Jest', 'Docker'],
        codeQuality: 8.5,
        docs: 'README, JSDoc, Storybook',
        tests: 'Покрытие 72%, e2e и unit',
        cicd: 'GitHub Actions, линтеры, автотесты',
        aiNote: 'Код структурирован, используются современные практики, хорошее покрытие тестами. Рекомендуется добавить больше e2e-тестов.',
        grade,
        positionAdvice: 'Рекомендуем претендовать на Middle Frontend Developer.',
        upgradeAdvice: 'Для перехода на Senior: добавьте больше e2e-тестов, внедрите code review, улучшите документацию.',
        gradeAdvice: pos && grade !== (pos.split(' ')[0] || '')
          ? `Для позиции "${pos}" нужно прокачать: архитектуру, тесты, CI/CD.` : '',
        hhAnalysis: hhUrl.value ? {
          title: 'Анализ вакансии с hh.ru',
          requirements: 'Требуется опыт с Vue 3, знание TypeScript, опыт CI/CD, тестирование (Jest), опыт работы с REST API.',
          match: 'Совпадение по стеку: 80%. Рекомендуется прокачать опыт с e2e-тестами и Docker.',
          advice: 'Для полного соответствия вакансии: добавить примеры CI/CD, покрыть больше кода тестами, оформить README с примерами.'
        } : null
      }
    } else {
      result.value = {
        project: repoUrl.value.split('/').pop() || 'Demo Project',
        skills: ['TypeScript', 'Vue 3', 'Vite', 'Jest', 'Docker'],
        codeQuality: 8.5,
        docs: 'README, JSDoc, Storybook',
        tests: 'Покрытие 72%, e2e и unit',
        cicd: 'GitHub Actions, линтеры, автотесты',
        aiNote: 'Код структурирован, используются современные практики, хорошее покрытие тестами. Рекомендуется добавить больше e2e-тестов.',
        hrSummary: 'Проект соответствует уровню Middle. Хороший стек, тесты, CI/CD. Рекомендуется для рассмотрения на позицию Middle Frontend.',
        hhAnalysis: hhUrl.value ? {
          title: 'Анализ вакансии с hh.ru',
          requirements: 'Требуется опыт с Vue 3, знание TypeScript, опыт CI/CD, тестирование (Jest), опыт работы с REST API.',
          match: 'Совпадение по стеку: 80%. Рекомендуется прокачать опыт с e2e-тестами и Docker.',
          advice: 'Для полного соответствия вакансии: добавить примеры CI/CD, покрыть больше кода тестами, оформить README с примерами.'
        } : null
      }
    }
  })
}

function downloadReport() {
  if (!result.value) return;
  let text = `# AI-анализ репозитория\n\n- **Проект:** ${result.value.project}\n- **Навыки:** ${result.value.skills.join(', ')}\n- **Чистота кода:** ${result.value.codeQuality}/10\n- **Документация:** ${result.value.docs}\n- **Тесты:** ${result.value.tests}\n- **CI/CD:** ${result.value.cicd}\n- **AI-заметка:** ${result.value.aiNote}`;
  if (mode.value === 'dev') {
    text += `\n- **Грейд:** ${result.value.grade}\n- **Рекомендация по позиции:** ${result.value.positionAdvice}\n- **Советы по прокачке:** ${result.value.upgradeAdvice}`;
    if (finalPosition) text += `\n- **Желаемая позиция:** ${finalPosition}\n  ${result.value.gradeAdvice || ''}`;
  } else {
    text += `\n- **Оценка для HR:** ${result.value.hrSummary}`;
  }
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
  flex-direction: column;
  gap: 1.1rem;
  align-items: center;
  width: 100%;
  max-width: 420px;
  margin: 0 auto 2rem auto;
}
.repo-analyzer__form > * {
  margin-bottom: 0;
  width: 100%;
  max-width: 420px;
  box-sizing: border-box;
}
.repo-analyzer__form input,
.repo-analyzer__form select,
.repo-analyzer__form button {
  width: 100%;
  max-width: 420px;
  box-sizing: border-box;
}
.repo-analyzer__form button {
  margin-top: 0.5rem;
}
.repo-analyzer__hh-group {
  width: 100%;
  max-width: 420px;
  align-items: flex-start;
}
.repo-analyzer__hh-desc {
  font-size: 0.93em;
  color: #b3e6ff;
  margin-top: 0.2em;
  margin-left: 0.1em;
  line-height: 1.2;
  max-width: 100%;
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
.repo-analyzer__mode-switch {
  display: flex;
  justify-content: center;
  gap: 1.2em;
  margin-bottom: 1.2em;
}
.switcher {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.7em;
  margin-bottom: 1.2em;
}
.switcher-label {
  font-weight: 600;
  color: #fff;
  opacity: 0.7;
  transition: color 0.18s, opacity 0.18s;
}
.switcher-label.active {
  color: #232a3b;
  opacity: 1;
}
.switcher-toggle {
  position: relative;
  display: inline-block;
  width: 54px;
  height: 28px;
}
.switcher-toggle input {
  opacity: 0;
  width: 0;
  height: 0;
}
.slider {
  position: absolute;
  cursor: pointer;
  top: 0; left: 0; right: 0; bottom: 0;
  background: linear-gradient(90deg, #65d6ff 0%, #ff7eb3 100%);
  border-radius: 28px;
  transition: .3s;
}
.slider:before {
  position: absolute;
  content: "";
  height: 22px;
  width: 22px;
  left: 3px;
  bottom: 3px;
  background: #fff;
  border-radius: 50%;
  transition: .3s;
  box-shadow: 0 2px 8px #65d6ff33;
}
.switcher-toggle input:checked + .slider {
  background: linear-gradient(90deg, #ff7eb3 0%, #65d6ff 100%);
}
.switcher-toggle input:checked + .slider:before {
  transform: translateX(26px);
}
.repo-analyzer__hh-input {
  padding: 0.7em 1.2em;
  border-radius: 1em;
  border: 1.5px solid #65d6ff44;
  font-size: 1rem;
  min-width: 200px;
  max-width: 100%;
  margin-bottom: 0.5em;
}
.grade-badge {
  display: inline-block;
  padding: 0.3em 1.2em;
  border-radius: 1.2em;
  font-weight: 700;
  font-size: 1.1em;
  margin-left: 0.5em;
}
.grade-junior { background: #ffd86b; color: #232a3b; }
.grade-middle { background: #65d6ff; color: #232a3b; }
.grade-senior { background: #ff7eb3; color: #fff; }
.repo-analyzer__hr-block {
  margin: 1.2em 0 1.2em 0;
  background: #f7faff;
  border-radius: 1.2em;
  padding: 1em 1.2em;
  color: #232a3b;
  box-shadow: 0 2px 8px #65d6ff22;
}
.repo-analyzer__select, .repo-analyzer__custom-input {
  padding: 0.7em 1.2em;
  border-radius: 1em;
  border: 1.5px solid #65d6ff44;
  font-size: 1rem;
  min-width: 200px;
  max-width: 100%;
  margin-bottom: 0.5em;
}
.repo-analyzer__input {
  padding: 0.7em 1.2em;
  border-radius: 1em;
  border: 1.5px solid #65d6ff44;
  font-size: 1rem;
  background: #fff;
  transition: border 0.18s, box-shadow 0.18s;
  box-sizing: border-box;
}
.repo-analyzer__input:focus {
  border: 1.5px solid #65d6ff;
  box-shadow: 0 0 0 2px #65d6ff33;
  outline: none;
}
@media (max-width: 900px) {
  .repo-analyzer__form,
  .repo-analyzer__hh-group {
    max-width: 100%;
  }
}
@media (max-width: 600px) {
  .repo-analyzer__form,
  .repo-analyzer__hh-group {
    max-width: 100%;
  }
  .repo-analyzer__form > * {
    max-width: 100%;
  }
}
.repo-analyzer__button {
  position: relative;
  overflow: hidden;
  padding: 0.7em 1.7em;
  border-radius: 2em;
  background: linear-gradient(90deg, #65d6ff 0%, #ff7eb3 100%);
  color: #fff;
  font-weight: 600;
  font-size: 1rem;
  border: none;
  box-shadow: 0 2px 8px #3a7bd522;
  transition: background 0.2s, opacity 0.2s;
  display: block;
  width: 100%;
  max-width: 420px;
  cursor: pointer;
}
.repo-analyzer__button:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}
.repo-analyzer__button--loading {
  color: #fff;
  pointer-events: none;
}
.repo-analyzer__button-text {
  position: relative;
  z-index: 2;
}
.repo-analyzer__progress-bar {
  position: absolute;
  left: 0; top: 0; bottom: 0;
  height: 100%;
  background: linear-gradient(90deg, #65d6ff 0%, #ff7eb3 100%);
  border-radius: 2em;
  z-index: 1;
  transition: width 0.18s linear;
}
</style> 