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
          <p class="email-paragraph">{{ user.email }}</p>
        </div>
      </div>
      <div class="col code">
        <p>{{ user.employeeCode }}</p>
      </div>
      <div class="col designation">
        <p>{{ user.designation }}</p>
      </div>
      <div class="col phone">
        <p>{{ formatPhone(user.phone) }}</p>
      </div>
      <div class="col date">
        <p>{{ formatDate(user.joiningDate) }}</p>
      </div>
      <div class="menu-more"></div>
    </li>
  </ul>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import { API_URL, PHONE_REGEX } from '../model/constants';
import { monthEnum } from '../model/date';

interface Raw {
  name: string;
  avatar: string;
  phone: string;
  employeeCode: string;
  designation: string;
  joiningDate: string;
  id: number;
  email: string;
}

export default defineComponent({
  name: 'ListComponent',
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
    formatPhone(phone: string) {
      const valid = PHONE_REGEX.test(phone);

      const replacer = (validPhone: string) => {
        const formatLetters = validPhone.replace(/\w/g, '');
        return formatLetters.replace(/\(*\)/g, '');
      };
      return valid ? phone : 'Please, check your phone number';
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
    margin: 14px 0;

    &:hover {
      box-shadow: rgba(149, 157, 165, 0.4) 0px 8px 24px;
      transition: box-shadow ease-in-out 0.8s;
    }

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
        display: flex;
        flex-flow: row nowrap;
        justify-content: flex-start;
        align-items: center;

        div.userId,
        div.name {
          p {
            padding: 0.3rem 0.5rem;
            text-align: left;
            &.name-paragraph {
              font-weight: 800;
            }
            &.email-paragraph {
              font-size: small;
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
  .menu-more::after {
    content: '\2807';
    color: slategray;
    font-size: 20px;
  }
}

@media (max-width: 960px) {
  ul.employee-list {
    display: flex;
    flex-flow: column nowrap;
    align-content: center;
    justify-content: center;
    align-items: center;

    li.item {
      display: flex;
      flex-flow: column nowrap;
      justify-content: center;
      align-items: center;
      margin: 20px 0;
      max-width: 400px;
      min-width: 280px;
      .col {
        display: flex;
        flex-flow: row nowrap;
        align-content: center;
        justify-content: center;
        align-items: center;

        p {
          margin: 0;
          padding: 10px;
        }

        &.basic {
          display: flex;
          flex-flow: column nowrap;
          justify-content: flex-start;
          align-items: center;

          div.userId {
            display: none;
          }
          div.name {
            p {
              text-align: center;
            }
          }
          img {
            width: 60px;
            padding: 10px;
          }
        }

        &.code {
          display: none;
        }
      }
    }
  }
  div.menu-more {
    display: none;
  }
}
</style>