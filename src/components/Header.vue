<script>
export default {
  props: {
    isDarkMode: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    toggleTheme() {
      const newTheme = !this.isDarkMode;
      this.$emit("theme-changed", newTheme);
      document.body.classList.toggle("dark", !this.isDarkMode);
    },
  },
};
</script>

<template>
  <header :class="{ light: !isDarkMode, dark: isDarkMode }">
    <div class="logo">
      <img v-if="isDarkMode" src="../assets/images/logo_dark.svg" alt="Logo" />
      <img v-else src="../assets/images/logo_light.svg" alt="Logo" />
    </div>
    <button
      @click="toggleTheme"
      class="theme-toggler"
      :class="{ light: !isDarkMode, dark: isDarkMode }"
    >
      <img
        v-if="isDarkMode"
        src="../assets/images/icon-sun.svg"
        alt="Show Light Mode"
      />
      <img v-else src="../assets/images/icon-moon.svg" alt="show Dark Mode" />
    </button>
  </header>
</template>

<style scoped>
header {
  display: flex;
  padding: 0.5rem 0.75rem;
  justify-content: space-between;
  align-items: center;
  border-radius: 0.625rem;
  border: 1px solid #d6e2f5;
  box-shadow: 0 2px 3px 0 #d9e5f4;
  margin: 1.25rem auto 2.5rem auto;
  width: 23.875rem;
}

.logo {
  background-image: url("../assets/images/logo.svg");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  width: 179px;
  height: 41px;
}

.text-color {
  fill: red;
}

button.theme-toggler {
  width: 3.125rem;
  height: 3.125rem;
  border-radius: 0.75rem;
  display: flex;
  justify-content: center;
  align-items: center;
  border: none;
}

button.theme-toggler.light {
  background-color: var(--colors-neutral-100);
  color: var(--colors-neutral-900);
}

/* button.theme-toggler.dark {
        background-color: var(--colors-neutral-100);
        color: var(--colors-neutral-900);
    } */
</style>
