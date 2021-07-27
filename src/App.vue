<template>
  <div class="app-container">
    <Header />
    <main>
      <List />
    </main>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import List from "./components/List.vue";
import Header from "./components/Header.vue";

export default defineComponent({
  name: "App",
  components: {
    List,
    Header,
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
