<template>
  <div class="select__word items-center justify-center flex column">
    <img src="/images/logo.png" class="hangman__game-logo" />

    <p>{{ subtitle }}</p>
  </div>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "PageIndex",
  props: {
    title: {
      type: [String],
      default: "",
    },
    subtitle: {
      type: [String],
      default: "",
    },
  },
  setup(props) {},
});
</script>
<style scoped>
.hangman__game-logo {
  width: 300px;
}
</style>
