<template>
  <header-filter @change-cat="handleChangeCat" />
  <list-header />
  <list-component :currentCat="currentCat" />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ListHeader from '../ui/ListHeader.vue';
import HeaderFilter from './HeaderFilter.vue';
import ListComponent from './ListComponent.vue';

export default defineComponent({
  name: 'EmployeesList',
  components: { ListHeader, ListComponent, HeaderFilter },
  data() {
    return {
      currentCat: 'all'
    }
  },
  methods: {
    handleChangeCat(cat: string) {
      this.currentCat = cat;  
    }
  }
});
</script>