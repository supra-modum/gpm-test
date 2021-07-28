<template>
  <ul class="employee-list">
    <li class="item" v-for="user in usersRaw" :key="user.id">
      <div class="col basic">
        <div class="userId">
          <p>{{ user.id }}</p>
        </div>
        <div class="avatar">
          <img :src="user.avatar" alt="user avatar" />
        </div>
        <div class="name">
          <p class="name-paragraph">{{ user.name }}</p>
          <p class="email-paragraph">3mfhognm5@relay.firefox.com</p>
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
import { API_URL } from "../model/constants";
import { monthEnum } from "../model/date";

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
  name: "ListComponent",
  data() {
    return {
      usersRaw: null || (Object as PropType<Raw>),
    };
  },
  methods: {
    formatDate(date: string) {
      let currentDate = new Date(date);
      const year = currentDate.getFullYear().toString();
      const month = currentDate.getMonth();
      const day = currentDate.getDate().toString();

      return `${monthEnum[month]} ${day}, ${year}`;
    },
  },
  async mounted() {
    const response = await fetch(API_URL);
    const data = await response.json();
    const stringData = JSON.stringify(data);
    this.usersRaw = JSON.parse(stringData);
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
            &.name-paragraph {
              font-weight: 800;
            }
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
      &.date,
      &.designation {
        flex-basis: 15%;
      }
    }
  }
}

@media (max-width: 960px) {
  ul.employee-list {
    p {
      text-align: center;
      padding: 0.3rem 0.5rem;
    }

    li.item {
      display: flex;
      flex-flow: column nowrap;
      justify-content: center;
      align-items: center;
      padding: 1rem;

      .col {
        display: flex;
        flex-flow: column nowrap;
        align-content: center;
        justify-content: center;
        align-items: center;

        &.basic {
          flex-basis: 40%;

          div.name {
            p {
              text-align: center;
            }
          }

          div.userId {
            display: none;
          }
        }

        &.designation,
        &.phone {
          flex-basis: 20%;
        }

        &.date,
        &.code {
          display: none;
        }
      }
    }
  }
}
</style>