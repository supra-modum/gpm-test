<template>
  <header>
    <section class="top-heading">
      <h1>Dashboard</h1>
      <div class="button">
        <button class="add-employee" name="Add Employee">+ Add Employee</button>
      </div>
    </section>
    <div class="filter-container">
      <ul class="filter-menu">
        <li class="li-all" :class="calcActiveClass('all')" @click="handleFilterClick('all')">Employee List</li>
        <li class="li-dev" :class="calcActiveClass('Developer')" @click="handleFilterClick('Developer')">Development</li>
        <li class="li-m" :class="calcActiveClass('Manager')" @click="handleFilterClick('Manager')">Managment</li>
      </ul>
    </div>
  </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'HeaderFilter',
  data() {
    return {
      selectedCategory: 'all',
    };
  },
  methods: {
    handleFilterClick(cat: string) {
      this.selectedCategory = cat;
      this.$emit('changeCat', cat);
    },
    calcActiveClass(cat: string) {
      if (this.selectedCategory === cat) return 'active'
      return '';
    }
  }
});
</script>

<style lang="scss" scoped>
$actionColor: rgb(0, 220, 129);

header {
  display: flex;
  flex-flow: column nowrap;
  text-align: center;
  padding-bottom: 2rem;

  h1 {
    color: darkslategray;
    font-size: 2rem;
  }

  section.top-heading {
    display: flex;
    align-items: baseline;
    justify-content: space-between;
  }

  .filter-container {
    margin-bottom: 20px;
  }

  .filter-menu {
    color: silver;
    font-weight: 600;
    border-bottom: 1px solid rgb(222, 231, 227);
    list-style: none;
    display: flex;
    flex-flow: row nowrap;
    align-content: center;
    align-items: center;
    justify-content: flex-start;
    padding: 0;
  }

  .li-all,
  .li-dev,
  .li-m {
    padding: 20px;
    display: flex;
    text-align: center;
    margin: 0 20px;
    border-bottom: 1px solid rgba(0, 0, 0, 0);

    &.active,
    &:hover,
    &:active {
      color: slategray;
      border-bottom-color: $actionColor;
      transition: border-bottom ease-in-out 0.8s;
    }
  }
}

button.add-employee {
  text-align: center;
  color: white;
  background: $actionColor;
  border-radius: 5px;
  border-style: none;
  padding: 10px 20px;

  &:hover {
    box-shadow: rgba(149, 157, 165, 0.4) 0px 8px 24px;
    transition: box-shadow ease-in-out 0.8s;
  }
}

@media (max-width: 960px) {
  header {
    section.top-heading {
      display: flex;
      flex-flow: column nowrap;
      align-content: center;
      justify-content: center;
      align-items: center;
    }

    .filter-container {
      display: none;
    }
  }
}
</style>