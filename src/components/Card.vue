<script>
export default {
  name: "Card",
  props: {
    logo: String,
    title: String,
    description: String,
    status: Boolean,
  },
};
</script>

<template>
  <div class="card">
    <div><img :src="logo" alt=""></div>
    <div>
      <h2>{{ title }}</h2>
      <p>{{ description }}</p>
    </div>
    <div>
      <button>Remove</button>
      <label class="switch">
        <input type="checkbox" />
        <span class="slider round"></span>
      </label>
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 23.875rem;
  height: 12.5rem;
  padding: 1.25rem;
  border-radius: var(--corner-radius-20, 1.25rem);
  border: 1px solid var(--colors-neutral-200);
  background-color: var(--colors-neutral-0);
  box-shadow: 0 2px 2px 0 rgba(194, 206, 225, 0.2),
    0 1px 5px 1px rgba(194, 206, 225, 0.22);

  display: grid;
  grid-template-rows: auto 1fr 2.375rem;
  grid-template-columns: 60px 1fr;
  gap: 1rem;
}

.card div:nth-child(1) {
  grid-column: 1; /* Icon in der ersten Spalte */
  grid-row: 1; /* In der ersten Zeile */
}

.card div:nth-child(2) {
  grid-column: 2;
  grid-row: 1;
}

.card div:nth-child(3) {
  grid-column: 1 / 3;
  grid-row: 3;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

p {
  margin-top: 0.5rem;
}

button {
  font-family: "Noto Sans Medium";
  font-size: 1rem;
  font-style: normal;
  font-weight: 500;
  line-height: 140%;
  letter-spacing: -0.03125rem;
  color: var(--colors-neutral-900);
}

.switch {
  position: relative;
  display: inline-block;
  width: 2.25rem;
  height: 1.25rem;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: var(--colors-neutral-300);
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 1rem;
  width: 1rem;
  left: 0.125rem;
  bottom: 0.125rem;
  background-color: var(--colors-neutral-0);
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider {
  background-color: var(--colors-red-700);
  box-shadow: 0 1px 3px 0 rgba(10, 13, 18, 0.15),
    0 1px 2px -1px rgba(10, 13, 18, 0.15);
}

input:focus + .slider {
  box-shadow: 0 1px 3px 0 rgba(10, 13, 18, 0.15),
    0 1px 2px -1px rgba(10, 13, 18, 0.15);
}

input:checked + .slider:before {
  -webkit-transform: translateX(1rem);
  -ms-transform: translateX(1rem);
  transform: translateX(1rem);
}

/* Rounded sliders */
.slider.round {
  border-radius: 62.4375rem;
}

.slider.round:before {
  border-radius: 624.9375rem;
}
</style>
