<template>
  <section class="skills" aria-labelledby="skills-heading">
    <h2 id="skills-heading">Навыки</h2>
    <div class="skills__groups" role="list">
      <div v-for="group in skillGroups" :key="group.title" class="skills__group" :style="{ '--accent': group.color }" role="listitem">
        <div class="skills__group-header">
          <span class="skills__group-icon" :style="{ background: group.color }" aria-hidden="true">
            <svg v-if="group.icon === 'frontend'" width="22" height="22" viewBox="0 0 24 24"><path fill="#fff" d="M3 5v14h18V5zm16 12H5V7h14zm-9-2h4v-2h-4zm0-4h4V9h-4z"/></svg>
            <svg v-else-if="group.icon === 'backend'" width="22" height="22" viewBox="0 0 24 24"><path fill="#fff" d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.41 0-8-3.59-8-8s3.59-8 8-8 8 3.59 8 8-3.59 8-8 8zm-1-13h2v6h-2zm0 8h2v2h-2z"/></svg>
            <svg v-else-if="group.icon === 'devops'" width="22" height="22" viewBox="0 0 24 24"><path fill="#fff" d="M12 4V1L8 5l4 4V6c3.31 0 6 2.69 6 6 0 1.3-.42 2.5-1.13 3.47l1.46 1.46C19.07 15.07 20 13.13 20 11c0-4.42-3.58-8-8-8zm-6.87 3.53L3.67 7.53C2.93 8.5 2.5 9.7 2.5 11c0 2.13.93 4.07 2.47 5.53l1.46-1.46C6.42 15.5 6 14.3 6 13c0-3.31 2.69-6 6-6v3l4-4-4-4v3c-4.42 0-8 3.58-8 8 0 2.13.93 4.07 2.47 5.53z"/></svg>
            <svg v-else-if="group.icon === 'test'" width="22" height="22" viewBox="0 0 24 24"><path fill="#fff" d="M21 7L9 19l-5.5-5.5 1.41-1.41L9 16.17l10.59-10.59z"/></svg>
          </span>
          <span class="skills__group-title">{{ group.title }}</span>
        </div>
        <div class="skills__tags">
          <span v-for="skill in group.skills" :key="skill" class="skills__tag" :aria-label="'Навык: ' + skill">{{ skill }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const skillGroups = [
  {
    title: 'Frontend',
    color: '#65d6ff',
    icon: 'frontend',
    skills: [
      'JavaScript', 'TypeScript', 'Vue.js', 'Vuex', 'Pinia', 'Vuetify', 'Element+', 'PrimeVue',
      'Tailwind CSS', 'SCSS', 'Bootstrap', 'HTML', 'CSS', 'BEM', 'A11y', 'Mobile First',
      'Vite', 'Webpack', 'Gulp', 'Axios', 'Fetch API', 'REST API', 'GraphQL', 'WebSocket', 'RPC/gRPC', 'SignalR'
    ]
  },
  {
    title: 'Backend',
    color: '#ff7eb3',
    icon: 'backend',
    skills: [
      'C#', '.NET', '.NET Core', '.NET Framework', 'Node.js', 'Express', 'NestJS', 'Firebase',
      'ASP.NET Core', 'WPF', 'WinForms', 'Console Apps',
      'MS SQL', 'PostgreSQL', 'MySQL', 'SQLite', 'MongoDB', 'Entity Framework Core', 'Dapper',
      'RESTful', 'Minimal APIs', 'gRPC', 'SignalR'
    ]
  },
  {
    title: 'Архитектура и паттерны',
    color: '#a1e3ff',
    icon: 'frontend',
    skills: [
      'MVC', 'MVVM', 'Clean Architecture'
    ]
  },
  {
    title: 'DevOps & Tools',
    color: '#ffd86b',
    icon: 'devops',
    skills: [
      'Docker', 'Git', 'GitHub', 'GitLab', 'GitHub Actions', 'CI/CD', 'Jira', 'Trello', 'GitHub Projects', 'GitHub Issues'
    ]
  },
  {
    title: 'Тестирование',
    color: '#7fffbe',
    icon: 'test',
    skills: [
      'Jest', 'xUnit', 'NUnit', 'Vue Test Utils', 'Playwright', 'Selenium'
    ]
  },
  {
    title: 'Принципы и документация',
    color: '#b3a1ff',
    icon: 'frontend',
    skills: [
      'Clean Code', 'SOLID', 'DRY', 'Performance Optimization', 'Storybook', 'JSDoc', 'Внутренние гайды'
    ]
  }
]
</script>

<style scoped>
.skills {
  max-width: 900px;
  margin: 0 auto 3rem auto;
  padding: 2.5rem 1rem 2rem 1rem;
  background: rgba(255,255,255,0.13);
  border-radius: 1.5rem;
  box-shadow: 0 8px 32px 0 rgba(31,38,135,0.18);
  backdrop-filter: blur(18px) saturate(180%);
  border: 1.5px solid rgba(255,255,255,0.35);
  position: relative;
  z-index: 1;
}
.skills h2 {
  font-size: 2rem;
  margin-bottom: 2.2rem;
  color: #fff;
  text-shadow: 0 2px 12px #232a3bcc, 0 0 8px #65d6ff99;
  text-align: center;
}
.skills__groups {
  display: flex;
  flex-wrap: wrap;
  gap: 2.2rem;
  justify-content: center;
}
.skills__group {
  min-width: 220px;
  max-width: 320px;
  flex: 1 1 220px;
  background: rgba(255,255,255,0.18);
  border-radius: 1.2rem;
  box-shadow: 0 2px 8px #65d6ff22;
  border: 2.5px solid var(--accent);
  padding: 1.2rem 1.1rem 1.1rem 1.1rem;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 0.7rem;
  position: relative;
  animation: fadeInUp 0.7s cubic-bezier(.4,0,.2,1);
}
.skills__group-header {
  display: flex;
  align-items: center;
  gap: 0.7rem;
  margin-bottom: 0.5rem;
}
.skills__group-icon {
  width: 2.2rem;
  height: 2.2rem;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 8px var(--accent);
}
.skills__group-title {
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--accent);
}
.skills__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}
.skills__tag {
  background: linear-gradient(90deg, var(--accent) 0%, #fff 100%);
  color: #181c2a;
  font-weight: 600;
  border-radius: 1.2em;
  padding: 0.35em 1.1em;
  font-size: 1rem;
  box-shadow: 0 1px 4px var(--accent);
  opacity: 0.92;
  transition: transform 0.18s, box-shadow 0.18s;
  cursor: pointer;
  animation: tagAppear 0.7s cubic-bezier(.4,0,.2,1);
}
.skills__tag:hover {
  transform: scale(1.08) rotate(-2deg);
  box-shadow: 0 4px 16px var(--accent);
  opacity: 1;
}
@media (max-width: 900px) {
  .skills__groups {
    gap: 1.2rem;
  }
  .skills__group {
    min-width: 160px;
    max-width: 98vw;
    padding: 0.8rem 0.7rem 0.7rem 0.7rem;
  }
}
@media (max-width: 600px) {
  .skills {
    padding: 2rem 1.2rem 1.5rem 1.2rem;
  }
  .skills__groups {
    flex-direction: column;
    gap: 1.2rem;
  }
  .skills__group {
    min-width: 0;
    max-width: 100vw;
    padding: 0.7rem 0.5rem 0.5rem 0.5rem;
  }
  .skills h2 {
    font-size: 1.3rem;
    margin-bottom: 1.2rem;
  }
}
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}
@keyframes tagAppear {
  from { opacity: 0; transform: scale(0.8); }
  to { opacity: 1; transform: scale(1); }
}
</style> 