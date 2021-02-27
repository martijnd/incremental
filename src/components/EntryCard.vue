<template>
  <div class="text-center bg-white shadow EntryCard">
    <h2 class="">Level {{ data.id }}</h2>
    <div>+{{ data.multiplier }} points</div>
    <div>{{ data.points }} points</div>
    <button
      class="px-4 py-2 mt-2 border border-gray-300 rounded"
      @click="$emit('increment')"
      :disabled="total < data.threshold"
    >
      Increment
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export type EntryCardData = {
  id: number;
  points: number;
  multiplier: number;
  threshold: number;
};

export default defineComponent({
  props: {
    data: {
      type: Object as () => EntryCardData,
      required: true,
    },
    total: {
      type: Number,
      required: true,
    },
  },
});
</script>

<style lang="scss" scoped>
.EntryCard {
  border-radius: 5px;
  padding: 1rem;
  margin-bottom: 1rem;
}
</style>