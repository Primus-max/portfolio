<template>
  <section class="certificates">
    <h2>Сертификаты и достижения</h2>
    <div class="certificates-list">
      <div class="certificate-card placeholder">
        [Здесь будут твои сертификаты и достижения]
      </div>
    </div>
  </section>
</template>

<script setup>
// Позже добавим анимации и реальные данные
</script>

<style scoped>
.certificates {
  max-width: 900px;
  margin: 0 auto 3rem auto;
  padding: 2rem 1rem;
  background: #fff;
  border-radius: 1.5rem;
  box-shadow: 0 2px 16px #e3f0ff33;
}
.certificates h2 {
  font-size: 2rem;
  margin-bottom: 1.5rem;
  color: #3a7bd5;
  text-align: center;
}
.certificates-list {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  justify-content: center;
}
.certificate-card.placeholder {
  min-width: 260px;
  min-height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #aaa;
  font-size: 1.1rem;
  border: 2px dashed #e3f0ff;
  border-radius: 1rem;
  background: #fafdff;
}
</style> 