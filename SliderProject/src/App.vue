<script>
import { ref } from "vue";
import TheSlider from "./components/Slider/TheSlider.vue";
export default {
  components: {
    TheSlider,
  },

  setup() {
    const myage = ref(50);
    const OnAgeValueChanged = (value) => {
      myage.value = value;
    };

    return {
      myage,
      OnAgeValueChanged,
    };
  },
};
</script>

<template>
  <h1>Hello Age Slider</h1>
  <div>Sam's Age:{{ myage }}</div>
  <TheSlider
    :targetvalue="myage"
    :minimum="0"
    :maximum="100"
    @age_value_changed="OnAgeValueChanged"
  />
</template>

<style scoped></style>
