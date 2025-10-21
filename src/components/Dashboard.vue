<script>
import Card from "./Card.vue";

export default {
  name: "Dashboard",
  components: { Card },
  data() {
    return {
      items: [],
    };
  },
  mounted() {
    this.loadData();
  },
  methods: {
    loadData() {
      fetch("../../data.json")
        .then((response) => response.json())
        .then((data) => {
          this.items = data;
        })
        .catch((error) => console.log("Error loading data:", error));
    },
  },
};
</script>

<template>
  <main>
    <h1 class="title">Extension List</h1>
    <div class="filter-container">
      <button>All</button>
      <button>Active</button>
      <button>Inactive</button>
    </div>
    <section>
      <div class="card-container">
        <Card
          v-for="item in items"
          :key="item.name"
          :logo="item.logo"
          :title="item.name"
          :description="item.description"
          :status="item.isActive"
        />
      </div>
    </section>
  </main>
</template>

<style scoped>
.card-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 1fr);
  gap: 0.75rem;
  margin: 0 auto;
  max-width: calc(3 * 23.875rem + 2 * 0.75rem);
}

@media (max-width: 767px) {
  .card-container {
    grid-template-columns: 1fr;
    max-width: calc(1 * 23.875rem + 0 * 0.75rem);
  }
}

@media (min-width: 768px) and (max-width: 1443px) {
  .card-container {
    grid-template-columns: repeat(2, 1fr);
    max-width: calc(2 * 23.875rem + 1 * 0.75rem);
  }
}

@media (min-width: 1440px) {
  .card-container {
    grid-template-columns: repeat(3, 1fr);
    max-width: calc(3 * 23.875rem + 2 * 0.75rem);
  }
}
</style>
