<template>
  <header :class="['header', darkMode ? 'dark' : 'light']">
    <div class="header-container">
      <h1 class="logo">Ticket Landing Page</h1>

      <button class="mode-toggle" @click="$emit('toggle-theme')">
        <span v-if="darkMode">🌙 Dark</span>
        <span v-else>☀️ Light</span>
      </button>
    </div>
  </header>
</template>

<script>
export default {
  name: "HeaderBar",
  props: {
    darkMode: Boolean
  }
}
</script>

<style scoped>
.header {
  width: 100%;
  padding: 20px 30px;
  box-sizing: border-box;
  border-bottom: 1px solid rgba(255,255,255,0.15);
  backdrop-filter: blur(8px);
}

.light {
  background: rgba(255, 255, 255, 0.9);
  border-bottom: 1px solid rgba(0,0,0,0.15);
  color: #111;
}

.dark {
  background: rgba(0, 0, 0, 0.55);
  border-bottom: 1px solid rgba(255,255,255,0.2);
  color: #f1f1f1;
}

.header-container {
  max-width: 1280px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  margin: 0;
  font-size: 26px;
  font-weight: 700;
}

.mode-toggle {
  padding: 8px 18px;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  font-size: 15px;
  transition: 0.2s ease-in-out;
}

.light .mode-toggle {
  background: #111;
  color: white;
}

.dark .mode-toggle {
  background: white;
  color: #111;
}

.mode-toggle:hover {
  transform: scale(1.05);
}
</style>
