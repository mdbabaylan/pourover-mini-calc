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
        <p class="is-size-4 has-text-weight-semibold">Total Output: {{ calculatedOutput }} grams</p>
      </div>

      <!-- Picker for selecting how many pours -->
      <div class="field">
        <label class="label">Select Pours</label>
        <div class="control">
          <div class="select is-fullwidth">
            <select v-model="selectedRatio">
              <option v-for="pours in pours" :key="pours" :value="pours">{{ pours }}</option>
            </select>
          </div>
        </div>
      </div>

      <div class="field">
        <div class="control">
          <input class="input" type="number" v-model="inputAmount" placeholder="Enter amount in grams" />
        </div>
      </div>

      Add bloom amount too, then deduct bloom in total amount to divide for X number of pours (yes get better at math
      too so u get better at coding)
      Match the number 1,2,3,4 with First Pour, Second Pour, Third Pour, Fourth Pour
      Use a text input, "Pour X next, new scale total should be X"

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
    const pours = ref([1, 2, 3, 4]);
    //const selectedPours = ref(pours.value[0]);
    const inputAmount = ref(0);

    const calculatedOutput = computed(() => {
      return (inputAmount.value * selectedRatio.value).toFixed(2);
    });

    return {
      ratios,
      selectedRatio,
      inputAmount,
      calculatedOutput,
      pours
    };
  },
};
</script>

<style scoped>
/* Minimal custom styles if needed */
</style>
