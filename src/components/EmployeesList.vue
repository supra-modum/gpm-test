<template>
  <header-filter />
  <list-header />
  <list-component></list-component>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ListHeader from '../ui/ListHeader.vue';
import HeaderFilter from './HeaderFilter.vue';
import ListComponent from './ListComponent.vue';

export default defineComponent({
  name: 'EmployeesList',
  components: { ListHeader, ListComponent, HeaderFilter },
});
</script>