<template>
  <header>
    <section class="top-heading">
      <h1>Dashboard</h1>
      <div class="button">
        <button class="add-employee" name="Add Employee">+ Add Employee</button>
      </div>
    </section>
    <section class="filter">
      <div class="col all">
        <label for="all-select"
          ><input
            type="radio"
            v-model="selectedValue"
            value="All"
            id="all-select"
          />Employee List</label
        >
      </div>
      <div class="col dev">
        <label for="developer-select"
          ><input
            type="radio"
            v-model="selectedValue"
            value="Developer"
            id="developer-select"
          />Development</label
        >
      </div>
      <div class="col managment">
        <label for="manager-select"
          ><input
            type="radio"
            v-model="selectedValue"
            value="Manager"
            id="manager-select"
          />Managment</label
        >
      </div>
    </section>
  </header>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "HeaderFilter",
  data() {
    return {
      selectedValue: "",
    };
  },
});
</script>

<style lang="scss" scoped>
$actionColor: rgb(0, 220, 129);
$basicPadding: 20px;

header {
  display: flex;
  flex-flow: column nowrap;
  text-align: center;
  padding-bottom: 2rem;

  h1 {
    color: darkslategray;
    font-size: 2rem;
  }

  .button-col {
    max-width: 200px;
  }

  section.top-heading {
    display: flex;
    align-items: baseline;
    justify-content: space-between;
  }

  section.filter {
    display: flex;
    color: silver;
    font-weight: 600;
    border-bottom: 0.1rem solid rgb(222, 231, 227);
    .col {
      display: flex;
      flex-flow: row nowrap;
      align-content: center;
      align-items: center;
      justify-content: center;

      &.all,
      &.dev,
      &.managment {
        flex-basis: 15%;
        text-align: center;
        padding: 1rem 0;
      }
      &:hover,
      &:active {
        color: slategray;
      }
    }
  }

  button.add-employee {
    text-align: center;
    color: white;
    background: $actionColor;
    border-radius: 0.2rem;
    border-style: none;
    padding: 0.6rem 0.8rem;
  }
}
</style>