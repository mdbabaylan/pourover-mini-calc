<template>
  <div class="app section">
    <h1 class="title has-text-centered">Pour-Over Calculator</h1>
    <div class="box">
      <!-- Picker for selecting the ratio -->
      <div class="field">
        <label class="label">Select Ratio:</label>
        <div class="control">
          <div class="select is-fullwidth">
            <select v-model="selectedRatio">
              <option v-for="ratio in ratios" :key="ratio" :value="ratio">{{ ratio }}</option>
            </select>
          </div>
        </div>
      </div>

      <!-- Input for amount -->
      <div class="field">
        <label class="label">Enter Amount (grams):</label>
        <div class="control">
          <input class="input" type="number" v-model="inputAmount" placeholder="Enter amount in grams" />
        </div>
      </div>

      <!-- Output display -->
      <div class="content has-text-centered">
        <p class="is-size-4 has-text-weight-semibold">Output: {{ calculatedOutput }} grams</p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  name: 'App',
  setup() {
    const ratios = ref([15, 16, 17]);
    const selectedRatio = ref(ratios.value[0]);
    const inputAmount = ref(0);

    const calculatedOutput = computed(() => {
      return (inputAmount.value * selectedRatio.value).toFixed(2);
    });

    return {
      ratios,
      selectedRatio,
      inputAmount,
      calculatedOutput,
    };
  },
};
</script>

<style scoped>
/* Minimal custom styles if needed */
</style>
