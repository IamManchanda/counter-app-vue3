<template>
  <div class="button-container">
    <button
      class="btn btn-success btn-lg"
      :class="count >= 100 ? 'disabled' : ''"
      @click="handleIncrement"
    >
      Increment
    </button>
    <button
      class="btn btn-danger btn-lg"
      :class="count <= 0 ? 'disabled' : ''"
      @click="handleDecrement"
    >
      Decrement
    </button>
  </div>
  <hr />
  <h4>Current Count: {{ count }}</h4>
  <hr />
  <h4>Hundred Minus Count: {{ hundredMinusCount }}</h4>
</template>

<script>
import { reactive, computed, watchEffect, toRefs } from "vue";

export default {
  setup() {
    //#region Data & Computed Properties
    const state = reactive({
      count: 0,
      hundredMinusCount: computed(computeHundredMinusCount),
    });
    //#endregion

    //#region Watchers
    watchEffect(() => {
      logCount();
      logHundredMinusCount();
    });
    //#endregion

    //#region Methods
    function computeHundredMinusCount() {
      return 100 - state.count;
    }

    function logCount() {
      console.log(`Current Count: ${state.count}`);
    }

    function logHundredMinusCount() {
      console.log(`Hundred Minus Count: ${state.hundredMinusCount}`);
    }

    function handleIncrement() {
      if (state.count < 100) {
        state.count += 1;
      }
    }

    function handleDecrement() {
      if (state.count > 0) {
        state.count -= 1;
      }
    }
    //#endregion

    return {
      ...toRefs(state),
      handleIncrement,
      handleDecrement,
    };
  },
};
</script>
