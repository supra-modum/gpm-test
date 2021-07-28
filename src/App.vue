<template>
  <div class="app-container">
    <employees-list />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import EmployeesList from "./components/EmployeesList.vue";

export default defineComponent({
  name: "App",
  components: {
    EmployeesList,
  },
});
</script>

<style lang="scss" scoped>
.app-container {
  max-width: 1024px;
  margin: 0 auto;
  padding: 50px;
}
</style>
