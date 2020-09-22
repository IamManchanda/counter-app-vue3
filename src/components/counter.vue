<template>
  <div class="button-container">
    <button
      class="btn btn-success btn-lg"
      :class="count >= 100 ? 'disabled' : ''"
      @click="increment"
    >
      Increment
    </button>
    <button
      class="btn btn-danger btn-lg"
      :class="count <= 0 ? 'disabled' : ''"
      @click="decrement"
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
    const state = reactive({
      count: 0,
      hundredMinusCount: computed(() => 100 - state.count),
    });

    watchEffect(() => {
      console.log(`Current Count: ${state.count}`);
    });

    return {
      ...toRefs(state),
      increment: () => {
        if (state.count < 100) {
          state.count += 1;
        }
      },
      decrement: () => {
        if (state.count > 0) {
          state.count -= 1;
        }
      },
    };
  },
};
</script>
