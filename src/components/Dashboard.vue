<script>
import Card from "./Card.vue";

export default {
  name: "Dashboard",
  components: { Card },
  data() {
    return {
      cards: [],
      filter: "all", // standardfilter
    };
  },
  mounted() {
    this.loadCards();
  },
  methods: {
    async loadCards() {
      try {
        const response = await fetch("../../data.json");
        this.cards = await response.json();
      } catch (error) {
        console.error("Fehler beim Laden der Daten:", error);
      }
    },
    updateCardStatus(cardName, newStatus) {
      const card = this.cards.find(card => card.name === cardName);
      if (card) {
        card.isActive = newStatus; // Status aktualisieren
      }
    },
    async removeCard(cardName) {
      this. cards = this.cards.filter(card => card.name !== cardName);
    }
  },
  computed: {
    filteredCards() {
      if (this.filter === "all") {
        return this.cards;
      } else if (this.filter === "active") {
        return this.cards.filter((card) => card.isActive);
      } else {
        return this.cards.filter((card) => !card.isActive);
      }
    },
  },
};
</script>

<template>
  <main>
    <h1 class="title">Extension List</h1>
    <div class="filter-container">
      <button class="light" :class="{ active: filter === 'all' }" @click="filter = 'all'">All</button>
      <button class="light" :class="{ active: filter === 'active' }" @click="filter = 'active'">Active</button>
      <button class="light" :class="{ active: filter === 'inactive' }" @click="filter = 'inactive'">Inactive</button>
    </div>
    <section>
      <div class="card-container">
        <Card
          v-for="card in filteredCards"
          :key="card.name"
          :logo="card.logo"
          :title="card.name"
          :description="card.description"
          :status="card.isActive"
          :onStatusChange="(newStatus) => updateCardStatus(card.name, newStatus)"
          :onRemove="removeCard"
        />
      </div>
    </section>
  </main>
</template>

<style scoped>
.title {
  text-align: center;
}

.filter-container {
  margin: 1.5rem auto 2.5rem auto;
  width: 295px;
  display: flex;
  justify-content: space-between;
}

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
