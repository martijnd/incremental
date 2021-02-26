<template>
  <h1>Incremental: {{ total }}</h1>
  <entry-card
    v-for="level in data"
    :key="level.id"
    @increment="level.points++"
    :data="level"
    :total="total"
  />
</template>

<script lang="ts">
import { computed, defineComponent, ref } from "vue";
import EntryCard, { EntryCardData } from "./components/EntryCard.vue";

export default defineComponent({
  name: "App",
  components: {
    EntryCard,
  },
  setup() {
    const data = ref<EntryCardData[]>([
      {
        id: 1,
        points: 0,
        multiplier: 1,
        threshold: 0,
      },
      {
        id: 2,
        points: 0,
        multiplier: 10,
        threshold: 5,
      },
    ]);

    const total = computed(() =>
      data.value.reduce(
        (sum, { points, multiplier }) => sum + points * multiplier,
        0
      )
    );

    return {
      data,
      total,
    };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 1rem;
  min-height: 100vh;
  background-color: #ccc;
}

body {
  margin: 0;
}
</style>