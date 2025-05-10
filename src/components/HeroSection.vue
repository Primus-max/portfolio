<template>
  <section class="hero">
    <div class="hero-content">
      <div class="hero-photo-blob">
        <svg class="hero-blob" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
          <path fill="#ff7eb3" fill-opacity="0.22" d="M44.8,-67.2C57.7,-59.2,67.7,-48.1,74.2,-34.9C80.7,-21.7,83.7,-6.4,80.2,7.7C76.7,21.8,66.7,34.7,56.1,46.2C45.5,57.7,34.3,67.8,20.7,73.7C7.1,79.6,-8.9,81.3,-23.2,76.2C-37.5,71.1,-50.1,59.2,-59.2,45.2C-68.3,31.2,-73.9,15.1,-74.2,-1.1C-74.5,-17.3,-69.5,-34.6,-59.6,-43.7C-49.7,-52.8,-34.9,-53.7,-21.1,-60.2C-7.3,-66.7,5.5,-78.8,19.7,-81.2C33.9,-83.6,49.6,-76.2,44.8,-67.2Z" transform="translate(100 100)"/>
        </svg>
        <div class="hero-photo">
          <!-- Моковое фото -->
          <img src="https://api.dicebear.com/7.x/identicon/svg?seed=primus" alt="avatar" />
        </div>
      </div>
      <h1>Владимир Примус</h1>
      <h2>Fullstack Developer (C# / Vue.js)</h2>
      <p class="hero-slogan">Создаю масштабируемые и эффективные решения с WOW-эффектом</p>
      <div class="hero-actions">
        <a class="resume-btn" href="#" download>Скачать резюме</a>
        <!-- <button class="theme-toggle" aria-label="Переключить тему">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <circle cx="12" cy="12" r="10" stroke="#65d6ff" stroke-width="2" fill="none"/>
            <path d="M12 6V2M12 22V18M4.93 4.93L2.81 2.81M21.19 21.19L19.07 19.07M2 12H6M18 12H22M4.93 19.07L2.81 21.19M21.19 2.81L19.07 4.93" stroke="#65d6ff" stroke-width="2"/>
          </svg>
        </button> -->
      </div>
    </div>
  </section>
</template>

<script setup>
// Пока без логики
</script>

<style scoped>
.hero {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 70vh;
  position: relative;
  z-index: 1;
}
.hero-content {
  text-align: center;
  padding: 2.5rem 1.5rem 2rem 1.5rem;
  border-radius: 2rem;
  background: rgba(255,255,255,0.13);
  box-shadow: 0 8px 32px 0 rgba(31,38,135,0.18);
  backdrop-filter: blur(18px) saturate(180%);
  border: 1.5px solid rgba(255,255,255,0.35);
  position: relative;
  max-width: 420px;
  width: 100%;
  animation: contentAppear 1.5s cubic-bezier(.4,0,.2,1);
}
.hero-photo-blob {
  position: relative;
  width: 140px;
  height: 140px;
  margin: 0 auto 1.2rem auto;
  display: flex;
  align-items: center;
  justify-content: center;
}
.hero-blob {
  position: absolute;
  left: 0; top: 0;
  width: 140px;
  height: 140px;
  z-index: 0;
  animation: blobHeroAnim 8s ease-in-out infinite alternate;
}
@keyframes blobHeroAnim {
  0% { transform: scale(1) rotate(0deg); }
  100% { transform: scale(1.08) rotate(8deg); }
}
.hero-photo {
  position: relative;
  z-index: 1;
  width: 110px;
  height: 110px;
  border-radius: 50%;
  overflow: hidden;
  border: 5px solid;
  /* border-image: linear-gradient(135deg, #ff7eb3 0%, #65d6ff 100%) 1; */
  box-shadow: 0 0 32px 0 #ff7eb355, 0 0 0 8px #65d6ff22;
  background: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
}
.hero-photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}
.hero h1 {
  font-size: 2.2rem;
  font-weight: 700;
  margin-bottom: 0.3rem;
  letter-spacing: 0.01em;
  color: #fff;
}
.hero h2 {
  font-size: 1.2rem;
  font-weight: 400;
  color: #65d6ff;
  margin-bottom: 1.1rem;
}
.hero-slogan {
  font-size: 1.1rem;
  color: #fff;
  margin-bottom: 2rem;
  animation: fadeIn 2s ease-in;
}
.hero-actions {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-top: 1rem;
}
.resume-btn {
  display: inline-block;
  padding: 0.7em 1.7em;
  background: linear-gradient(90deg, #65d6ff 0%, #ff7eb3 100%);
  color: #fff;
  border-radius: 2em;
  text-decoration: none;
  font-weight: 600;
  box-shadow: 0 2px 8px #3a7bd522;
  transition: background 0.2s;
  font-size: 1rem;
  border: none;
}
.resume-btn:hover {
  background: linear-gradient(90deg, #ff7eb3 0%, #65d6ff 100%);
}
.theme-toggle {
  background: rgba(101,214,255,0.13);
  border: none;
  border-radius: 50%;
  padding: 0.6em;
  cursor: pointer;
  transition: background 0.2s;
  display: flex;
  align-items: center;
  justify-content: center;
}
.theme-toggle:hover {
  background: #65d6ff;
}
.theme-toggle:hover svg {
  stroke: #fff;
}
@media (max-width: 600px) {
  .hero-content {
    padding: 1.2rem 0.5rem 1.2rem 0.5rem;
    max-width: 98vw;
  }
  .hero h1 {
    font-size: 1.3rem;
  }
  .hero h2 {
    font-size: 1rem;
  }
  .hero-slogan {
    font-size: 0.95rem;
  }
  .hero-photo-blob, .hero-blob {
    width: 90px;
    height: 90px;
  }
  .hero-photo {
    width: 70px;
    height: 70px;
  }
}
@keyframes contentAppear {
  from { opacity: 0; transform: translateY(40px); }
  to { opacity: 1; transform: translateY(0); }
}
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style> 