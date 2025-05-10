<script setup>
import AboutSection from './components/AboutSection.vue';
import ContactsSection from './components/ContactsSection.vue';
import ExperienceSection from './components/ExperienceSection.vue';
import HeroSection from './components/HeroSection.vue';
import ProjectsSection from './components/ProjectsSection.vue';
import RepoAnalyzerSection from './components/RepoAnalyzerSection.vue';
import SkillsSection from './components/SkillsSection.vue';
</script>

<template>
  <div class="portfolio-root">
    <div class="background-blobs">
      <!-- SVG blob background -->
      <svg class="blob1" viewBox="0 0 600 600" xmlns="http://www.w3.org/2000/svg">
        <g transform="translate(300,300)">
          <path d="M120,-180C160,-140,200,-100,200,-60C200,-20,160,20,120,60C80,100,40,140,0,180C-40,220,-80,260,-120,220C-160,180,-200,140,-200,100C-200,60,-160,20,-120,-20C-80,-60,-40,-100,0,-140C40,-180,80,-220,120,-180Z" fill="#ff7eb3" fill-opacity="0.18"/>
        </g>
      </svg>
      <svg class="blob2" viewBox="0 0 600 600" xmlns="http://www.w3.org/2000/svg">
        <g transform="translate(300,300)">
          <path d="M120,-180C160,-140,200,-100,200,-60C200,-20,160,20,120,60C80,100,40,140,0,180C-40,220,-80,260,-120,220C-160,180,-200,140,-200,100C-200,60,-160,20,-120,-20C-80,-60,-40,-100,0,-140C40,-180,80,-220,120,-180Z" fill="#65d6ff" fill-opacity="0.13"/>
        </g>
      </svg>
    </div>
    <HeroSection />
    <RepoAnalyzerSection />
    <svg class="wave" viewBox="0 0 1440 80" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M0,40 C360,80 1080,0 1440,40 L1440,80 L0,80 Z" fill="url(#grad1)" fill-opacity="0.18"/><defs><linearGradient id="grad1" x1="0" y1="0" x2="1440" y2="80" gradientUnits="userSpaceOnUse"><stop stop-color="#65d6ff"/><stop offset="1" stop-color="#ff7eb3"/></linearGradient></defs></svg>
    <AboutSection />
    <svg class="wave" viewBox="0 0 1440 80" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M0,40 C360,80 1080,0 1440,40 L1440,80 L0,80 Z" fill="url(#grad2)" fill-opacity="0.18"/><defs><linearGradient id="grad2" x1="0" y1="0" x2="1440" y2="80" gradientUnits="userSpaceOnUse"><stop stop-color="#ff7eb3"/><stop offset="1" stop-color="#ffd86b"/></linearGradient></defs></svg>
    <SkillsSection />
    <svg class="wave" viewBox="0 0 1440 80" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M0,40 C360,80 1080,0 1440,40 L1440,80 L0,80 Z" fill="url(#grad3)" fill-opacity="0.18"/><defs><linearGradient id="grad3" x1="0" y1="0" x2="1440" y2="80" gradientUnits="userSpaceOnUse"><stop stop-color="#ffd86b"/><stop offset="1" stop-color="#7fffbe"/></linearGradient></defs></svg>
    <ProjectsSection />
    <svg class="wave" viewBox="0 0 1440 80" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M0,40 C360,80 1080,0 1440,40 L1440,80 L0,80 Z" fill="url(#grad4)" fill-opacity="0.18"/><defs><linearGradient id="grad4" x1="0" y1="0" x2="1440" y2="80" gradientUnits="userSpaceOnUse"><stop stop-color="#7fffbe"/><stop offset="1" stop-color="#65d6ff"/></linearGradient></defs></svg>
    <ExperienceSection />
    <svg class="wave" viewBox="0 0 1440 80" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M0,40 C360,80 1080,0 1440,40 L1440,80 L0,80 Z" fill="url(#grad5)" fill-opacity="0.18"/><defs><linearGradient id="grad5" x1="0" y1="0" x2="1440" y2="80" gradientUnits="userSpaceOnUse"><stop stop-color="#65d6ff"/><stop offset="1" stop-color="#ff7eb3"/></linearGradient></defs></svg>
    <ContactsSection />
  </div>
</template>

<style scoped>
.portfolio-root {
  font-family: 'Manrope', 'Segoe UI', 'Roboto', 'Arial', sans-serif;
  background: none;
  color: #fff;
  min-height: 100vh;
  padding: 20px;
  position: relative;
  overflow-x: hidden;
}
.background-blobs {
  position: fixed;
  z-index: 0;
  top: 0; left: 0; width: 100vw; height: 100vh;
  pointer-events: none;
}
.blob1 {
  position: absolute;
  left: -180px; top: -120px;
  width: 700px; height: 700px;
  animation: blobMove1 18s ease-in-out infinite alternate;
}
.blob2 {
  position: absolute;
  right: -200px; bottom: -120px;
  width: 700px; height: 700px;
  animation: blobMove2 22s ease-in-out infinite alternate;
}
@keyframes blobMove1 {
  0% { transform: scale(1) rotate(0deg); }
  100% { transform: scale(1.08) rotate(12deg); }
}
@keyframes blobMove2 {
  0% { transform: scale(1) rotate(0deg); }
  100% { transform: scale(0.95) rotate(-8deg); }
}
.wave {
  width: 100vw;
  height: 60px;
  display: block;
  margin: -1.5rem 0 -1.5rem 0;
  z-index: 2;
  pointer-events: none;
}
</style>
