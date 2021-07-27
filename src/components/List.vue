<template>
  <ListHeader />
  <ul class="employee-list">
    <li class="item" v-for="user in usersRaw" :key="user.id">
      <div class="col basic">
        <div class="userId">
          <p>{{ user.user_id }}</p>
        </div>
        <div class="avatar">
          <img :src="user.avatar" alt="user avatar" />
        </div>
        <div class="name">
          <p>{{ user.name }}</p>
          <p>3mfhognm5@relay.firefox.com</p>
        </div>
      </div>
      <div class="col code">
        <p>{{ user.employeeCode }}</p>
      </div>
      <div class="col designation">
        <p>{{ user.designation }}</p>
      </div>
      <div class="col phone">
        <p>{{ user.phone }}</p>
      </div>
      <div class="col date">
        <p>{{ formatDate(user.joiningDate) }}</p>
      </div>
    </li>
  </ul>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import ListHeader from "./ListHeader.vue";
import ListItem from "./ListItem.vue";

interface Raw {
  name: string;
  avatar: string;
  phone: string;
  employeeCode: string;
  designation: string;
  joiningDate: string;
  id: number | string;
}

const url = "https://60feae682574110017078723.mockapi.io/users";

export default defineComponent({
  name: "List",
  components: { ListHeader, ListItem },
  data() {
    return {
      usersRaw: null || (Object as PropType<Raw>),
    };
  },
  async mounted() {
    const response = await fetch(url);
    const data = await response.json();
    const stringData = JSON.stringify(data);
    //@ts-ignore
    this.usersRaw = JSON.parse(stringData);
  },
  methods: {
    formatDate(date: string) {
      enum monthEnum {
        "Jan" = 1,
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec",
      }
      let currentDate = new Date(date);
      const year = currentDate.getFullYear().toString();
      const month = currentDate.getMonth();
      const day = currentDate.getDate().toString();

      return `${monthEnum[month]} ${day}, ${year}`;
    },
  },
});
</script>

<style lang="scss" scoped>
ul.employee-list {
  padding: 0;
  margin: 0;

  li.item {
    display: flex;
    flex-flow: row wrap;
    justify-content: space-evenly;
    align-items: center;
    background-color: white;
    padding: 10px;
    box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
    border-radius: 5px;
    margin: 0.5rem 0;

    .col {
      display: flex;
      flex-flow: row nowrap;
      align-content: center;
      justify-content: center;
      align-items: center;

      p {
        margin: 0;
        color: slategray;
        font-weight: 500;
        font-size: smaller;
        text-align: center;
      }

      &.basic {
        flex-basis: 35%;

        div.userId,
        div.name {
          p {
            padding: 0.3rem 0.5rem;
            text-align: left;
          }
        }
        img {
          width: 50px;
          border-radius: 50%;
          padding: 0 0.5rem;
        }
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
}
</style>