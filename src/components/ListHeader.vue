<template>
  <section class="list-heading">
    <div class="col info">
      <label class="label">Basic info</label>
    </div>
    <div class="col code">
      <label class="label">Employee code</label>
    </div>
    <div class="col designation">
      <label class="label">Designation</label>
    </div>
    <div class="col phone">
      <label class="label">Phone number</label>
    </div>
    <div class="col date">
      <label class="label">Joining Date</label>
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
      flex-flow: row nowrap;
      justify-content: flex-start;
      .label {
        padding-left: 2.75rem;
      }
    }
    &.code,
    &.phone,
    &.date,
    &.designation {
      flex-basis: 15%;
    }
  }
}

@media (max-width: 960px) {
  section.list-heading {
    display: none;
  }
}
</style>