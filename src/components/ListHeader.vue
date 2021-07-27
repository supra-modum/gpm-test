<template>
  <section class="list-heading">
    <div class="col info">
      <label>Basic info</label>
    </div>
    <div class="col code">
      <label>Employee code</label>
    </div>
    <div class="col designation">
      <label>Designation</label>
    </div>
    <div class="col phone">
      <label>Phone number</label>
    </div>
    <div class="col date">
      <label>Joining Date</label>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "ListHeader",
});
</script>

<style lang="scss" scoped>
section.list-heading {
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-evenly;
  align-items: center;
  font-size: 1em;
  font-weight: 600;
  color: silver;
  padding: 20px 0;
  box-sizing: border-box;
  text-align: center;

  .col {
    display: flex;
    flex-flow: row nowrap;
    align-content: center;
    justify-content: center;
    align-items: center;
    padding: 4px;

    &.info {
      flex-basis: 35%;
      display: flex;
    }
    &.code,
    &.phone,
    &.date {
      flex-basis: 15%;
    }
    &.designation {
      flex-basis: 15%;
    }
  }
}
</style>