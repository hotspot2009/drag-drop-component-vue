<template>
  <div class="card">Card</div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "Card",
  data() {
    return {};
  },
  setup() {},
});
</script>

<style scoped>
.card {
  width: 80px;
  height: 80px;
  background-color: blueviolet;
}
</style>
