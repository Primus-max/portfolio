<template>
  <section class="contacts" aria-labelledby="contacts-heading">
    <h2 id="contacts-heading">Контакты</h2>
    <div class="contacts__content">
      <form class="contacts__form" role="form" aria-label="Форма обратной связи" @submit.prevent>
        <label>
          <span class="visually-hidden">Имя</span>
          <input type="text" placeholder="Имя" required autocomplete="name" aria-label="Имя" />
        </label>
        <label>
          <span class="visually-hidden">Email</span>
          <input type="email" placeholder="Email" required autocomplete="email" aria-label="Email" />
        </label>
        <label>
          <span class="visually-hidden">Сообщение</span>
          <textarea placeholder="Сообщение" required aria-label="Сообщение"></textarea>
        </label>
        <button type="submit" aria-label="Отправить сообщение">Отправить</button>
      </form>
      <div class="contacts__links" role="navigation" aria-label="Быстрые контакты">
        <a href="https://t.me/valosya" target="_blank" class="contacts__icon-link contacts__icon-link--tg" aria-label="Telegram">
          <span class="visually-hidden">Telegram</span>
          <span class="contacts__icon-bg">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" aria-hidden="true"><path d="M21.8 4.6c-.2-.2-.5-.3-.8-.2L3.2 10.2c-.3.1-.5.4-.5.7 0 .3.2.6.5.7l4.7 1.5 1.7 5.2c.1.3.4.5.7.5h.1c.3 0 .6-.2.7-.5l2-3.7 4.7 2.2c.1 0 .2.1.3.1.1 0 .2 0 .3-.1.2-.1.3-.3.3-.5l2-12c0-.3-.1-.6-.3-.7z" fill="#229ED9"/></svg>
          </span>
        </a>
        <a href="https://github.com/Primus-max" target="_blank" class="contacts__icon-link contacts__icon-link--gh" aria-label="GitHub">
          <span class="visually-hidden">GitHub</span>
          <span class="contacts__icon-bg">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" aria-hidden="true"><path d="M12 2C6.48 2 2 6.48 2 12c0 4.42 2.87 8.17 6.84 9.5.5.09.66-.22.66-.48 0-.24-.01-.87-.01-1.7-2.78.6-3.37-1.34-3.37-1.34-.45-1.15-1.1-1.46-1.1-1.46-.9-.62.07-.6.07-.6 1 .07 1.53 1.03 1.53 1.03.89 1.52 2.34 1.08 2.91.83.09-.65.35-1.08.63-1.33-2.22-.25-4.56-1.11-4.56-4.95 0-1.09.39-1.98 1.03-2.68-.1-.25-.45-1.27.1-2.65 0 0 .84-.27 2.75 1.02A9.56 9.56 0 0 1 12 6.8c.85.004 1.71.115 2.51.337 1.91-1.29 2.75-1.02 2.75-1.02.55 1.38.2 2.4.1 2.65.64.7 1.03 1.59 1.03 2.68 0 3.85-2.34 4.7-4.57 4.95.36.31.68.92.68 1.85 0 1.33-.01 2.4-.01 2.73 0 .27.16.58.67.48A10.01 10.01 0 0 0 22 12c0-5.52-4.48-10-10-10z" fill="#181717"/></svg>
          </span>
        </a>
        <a href="mailto:pr1musmax@yandex.ru" target="_blank" class="contacts__icon-link contacts__icon-link--mail" aria-label="Email">
          <span class="visually-hidden">Email</span>
          <span class="contacts__icon-bg">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" aria-hidden="true"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 2v.01L12 13 4 6.01V6h16zm0 12H4V8.99l8 6.99 8-6.99V18z" fill="#EA4335"/></svg>
          </span>
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
// Мокаем, логика не требуется
</script>

<style scoped>
.contacts {
  max-width: 700px;
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
.contacts h2 {
  font-size: 2rem;
  margin-bottom: 2.2rem;
  color: #fff;
  text-align: center;
  text-shadow: 0 2px 12px #232a3bcc, 0 0 8px #65d6ff99;
}
.contacts__content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}
.contacts__form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 100%;
  max-width: 350px;
}
.contacts__form input,
.contacts__form textarea {
  padding: 0.8em 1em;
  border-radius: 0.8em;
  border: 1.5px solid #65d6ff44;
  font-size: 1rem;
  font-family: inherit;
  background: #fff;
  resize: none;
  width: 100%;
  box-sizing: border-box;
}
.contacts__form textarea {
  min-height: 90px;
}
.contacts__form button {
  padding: 0.7em 1.5em;
  border-radius: 2em;
  border: none;
  background: #65d6ff;
  color: #fff;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.2s;
  outline: none;
}
.contacts__form button:focus {
  outline: 3px solid #ff7eb3;
  outline-offset: 2px;
}
.contacts__links {
  display: flex;
  gap: 1.2rem;
  justify-content: center;
  align-items: center;
  margin-top: 1.5rem;
  flex-wrap: wrap;
}
.contacts__icon-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: transparent;
  border: none;
  transition: background 0.18s, box-shadow 0.18s, transform 0.18s;
  outline: none;
  cursor: pointer;
  box-shadow: none;
  position: relative;
}
.contacts__icon-link:hover, .contacts__icon-link:focus {
  background: rgba(101,214,255,0.13);
  box-shadow: 0 2px 8px #65d6ff22;
  transform: scale(1.08);
}
.contacts__icon-link svg {
  width: 32px;
  height: 32px;
  display: block;
}
@media (max-width: 600px) {
  .contacts {
    padding: 2rem 1.2rem 1.5rem 1.2rem;
  }
  .contacts__content {
    gap: 1.2rem;
  }
  .contacts__form {
    max-width: 100%;
  }
  .contacts__links {
    flex-direction: row;
    gap: 1.2rem;
    align-items: center;
    margin-top: 1.2rem;
  }
  .contacts__icon-link {
    width: 44px;
    height: 44px;
  }
}
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0,0,0,0);
  border: 0;
}
.contacts__icon-bg {
  background: #fff;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 32px;
  height: 32px;
}
</style> 