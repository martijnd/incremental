<template>
  <div class="p-4 min-h-screen bg-gray-300">
    <h1 class="text-center mb-4 font-bold text-2xl">Incremental: {{ total }} points</h1>
    <entry-card
      v-for="level in data"
      :key="level.id"
      @increment="level.points++"
      :data="level"
      :total="total"
    />
  </div>
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
      {
        id: 3,
        points: 0,
        multiplier: 100,
        threshold: 50,
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
}

body {
  margin: 0;
}
</style>