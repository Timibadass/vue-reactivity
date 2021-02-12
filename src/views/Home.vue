<template>
  <div class="home">
    <form @click.prevent="">
      <table>
        <tr>
          <th>Name</th>
          <th>Username</th>
          <th>email</th>
          <th>Edit Cars</th>
          <th>Cars</th>
          <th>Gender</th>
        </tr>
        <tr v-for="user in users" :key="user.id">
          <td>{{ user.name }}</td>
          <td>{{ user.username }}</td>
          <td>{{ user.email }}</td>
          <td>
            <input
              type="number"
              style="width: 20px;"
              name="cars"
              id="cars"
              v-model.number="user.cars.number"
            />
          </td>
          <td>
            <cars-number :gender="user.gender" :cars="user.cars" />
          </td>
          <td>{{ user.gender }}</td>
        </tr>
      </table>

      <p>Total number of cars: {{ getTotalCars }}</p>
    </form>
  </div>
</template>

<script>
  // @ is an alias to /src
  import carsNumber from "@/components/cars-number.vue";
  const axios = require("axios");
  import { ref } from "vue";
  export default {
    name: "Home",
    data() {
      return {};
    },
    setup() {
      let users = ref([]);
      // let user = reactive({});
      const getUsers = async () => {
        let { data } = await axios({
          url: "data.json",
        });

        users.value = data;
        return users;
      };
      // const getUserById = async () => {
      //   // user = await
      // };
      return {
        users,
        getUsers,
      };
    },
    components: {
      carsNumber,
    },
    created() {
      this.getUsers();
    },
    computed: {
      getTotalCars() {
        let users = this.users;
        let totalCars = users.reduce(function(sum, elem) {
          return sum + elem.cars.number;
        }, 0);
        return totalCars;
      },
    },
    methods: {},
  };
</script>
