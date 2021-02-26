<template>
  <div class="EntryCard">
    <h2>Level {{data.id}}</h2>
    {{ data.points }}
    <button @click="$emit('increment')" :disabled="total < data.threshold">
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
  background-color: white;
  border-radius: 5px;
  box-shadow: 0 2px 10px 2px rgba(0, 0, 0, 0.2);
  padding: 1rem;
  margin-bottom: 1rem;
}
</style>