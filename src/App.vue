<script>
import Header from "./components/Header.vue";
import Dashboard from "./components/Dashboard.vue";

export default {
  components: {
    Header,
    Dashboard,
  },
  data() {
    return {
      isDarkMode: false,
    };
  },
  methods: {
    handleThemeChange(newTheme) {
      this.isDarkMode = newTheme;
    },
  },
};
</script>

<template>
  <div>
    <Header :is-dark-mode="isDarkMode" @theme-changed="handleThemeChange"></Header>
    <Dashboard :is-dark-mode="isDarkMode" />
  </div>
</template>

<style scoped></style>
