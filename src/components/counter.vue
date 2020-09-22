<template>
  <div class="button-container">
    <button class="btn btn-success btn-lg" @click="increment">
      Increment
    </button>
    <button
      class="btn btn-danger btn-lg"
      @click="decrement"
      :class="count <= 0 ? 'disabled' : ''"
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
        state.count += 1;
      },
      decrement: () => {
        state.count -= 1;
      },
    };
  },
};
</script>
