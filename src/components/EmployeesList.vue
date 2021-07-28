<template>
  <header-filter />
  <main>
    <list-header />
    <list-component></list-component>
  </main>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import ListHeader from "./ListHeader.vue";
import HeaderFilter from "./HeaderFilter.vue";
import ListComponent from "./ListComponent.vue";

interface Raw {
  name: string;
  avatar: string;
  phone: string;
  employeeCode: string;
  designation: string;
  joiningDate: string;
  id: number;
}

export default defineComponent({
  name: "EmployeesList",
  components: { ListHeader, HeaderFilter, ListComponent },
});
</script>