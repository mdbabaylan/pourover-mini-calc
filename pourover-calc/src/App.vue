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
        <label class="label">Enter Coffee Amount (grams):</label>
        <div class="control">
          <input class="input" type="number" v-model="inputAmount" placeholder="Enter amount in grams" />
        </div>
      </div>

      <!-- Picker for selecting how many pours -->
      <div class="field">
        <label class="label">Select # of pours</label>
        <div class="control">
          <div class="select is-fullwidth">
            <select v-model="selectedPours">
              <option v-for="pours in pours" :key="pours" :value="pours">{{ pours }}</option>
            </select>
          </div>
        </div>
      </div>

      <div class="field">
        <div class="control">
          <label class="label">Enter bloom amount</label>
          <input class="input" type="number" v-model="bloomAmount" />
        </div>
      </div>

      <hr class="is-divider">


      <div v-for="(pour, index) in selectedPours" :key="index" class="field">
        <label class="help">{{ formatPour(pour) }} pour</label>


        <input class="input" type="text" :value="(calculatedOutput - bloomAmount) / selectedPours" readonly />
        <label class="help">New total after {{ formatPour(pour) }} pour: {{ currentTotal(pour) }}g</label>




      </div>

    </div>

    <!-- Output display -->
    <div class="content has-text-centered">
      <p class="is-size-4 has-text-weight-semibold">Total Output: {{ calculatedOutput }} grams</p>
      <label class="help">(Including bloom)</label>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  name: 'App',
  setup() {
    const ratios = ref([10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]);
    const selectedRatio = ref(ratios.value[5]);
    const pours = ref([1, 2, 3, 4]);
    const selectedPours = ref(pours.value[2]);
    const inputAmount = ref(0);
    const bloomAmount = ref(0);

    const calculatedOutput = computed(() => {
      return (inputAmount.value * selectedRatio.value).toFixed(2);
    });

    const formatPour = computed(() => {
      return (pour) => {
        const suffixes = ["th", "st", "nd", "rd"];
        const value = pour % 100;
        return value + (suffixes[(value - 20) % 10] || suffixes[value] || suffixes[0]);
      };
    });

    const currentTotal = computed(() => {
      return (pour) => {
        return ((((calculatedOutput.value - bloomAmount.value) / selectedPours.value) * pour) + bloomAmount.value);
      }
    });

    return {
      ratios,
      selectedRatio,
      inputAmount,
      calculatedOutput,
      formatPour,
      pours,
      selectedPours,
      bloomAmount,
      currentTotal
    };
  },
};
</script>

<style scoped>
/* Minimal custom styles if needed */
</style>
