<template>
  <ul>
    <li v-for="user in usersRaw" :key="user.length">
      {{ user }}
    </li>
  </ul>
  <!-- <pre>{{ usersRaw }}</pre> -->
</template>

<script lang="ts">
import { defineComponent } from "vue";

const url = "https://60feae682574110017078723.mockapi.io/users";

export default defineComponent({
  name: "GetUsers",
  data() {
    return {
      //@ts-ignore
      usersRaw: null || [String],
    };
  },
  async mounted() {
    const response = await fetch(url);
    const data = await response.json();
    const stringData = JSON.stringify(data);
    //@ts-ignore
    this.usersRaw = JSON.parse(stringData);
  },
});
</script>