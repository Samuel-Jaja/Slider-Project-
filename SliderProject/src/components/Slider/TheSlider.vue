<script>
import { ref, computed, reactive, toRefs } from "vue";
export default {
  props: {
    minimum: {
      type: Number,
      default: 0,
    },
    maximum: {
      type: Number,
      default: 0,
    },
    targetvalue: {
      type: Number,
      default: 0,
    },
  },
  emits: ["age_value_changed"],

  setup(props, context) {
    const allotment = ref("");
    const sliderroller = ref(null);

    const emitChangedValue = (e) => {
      const value = Number(e.target.value);
      context.emit("age_value_changed", value);
    };

    const extensiveness = computed(() => {
      allotment.value =
        (props.targetvalue - props.minimum) / (props.maximum - props.minimum);
      return allotment.value;
    });

    return {
      sliderroller,
      extensiveness,
      emitChangedValue,
    };
  },
};
</script>

<template>
  <div class="theslider">
    <div>{{ minimum }}</div>
    <div
      class="the-slide_span"
      ref="sliderrollerr"
      :style="{ '--sliderroller': extensiveness }"
    >
      <input
        type="range"
        :minimum="minimum"
        :maximum="maximum"
        :targetvalue="targetvalue"
        @input="emitChangedValue"
      />
    </div>
    <div>{{ maximum }}</div>
  </div>
</template>

<style scoped>
.theslider {
  display: flex;
  align-items: stretch;
  width: 100%;
  max-width: 800px;
  gap: 80px;
}

.the-slide_span {
  display: flex;
  align-items: center;
  flex-grow: 1;
}

input[type="range"] {
  height: 2.9px;
  margin: 20px 0;
  width: 100%;
}
</style>
