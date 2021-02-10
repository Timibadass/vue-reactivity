<template>
  <p>{{ cars.number }}</p>
</template>

<script>
  import { watch, toRefs, toRef } from "vue";
  export default {
    props: {
      cars: {
        type: Object,
        required: true,
      },
      gender: {
        type: String,
        required: true,
      },
    },
    setup(props) {
      let { cars } = toRefs(props);
      let gender = toRef(props, "gender");
      console.log(gender.value);

      watch(
        () => cars,
        (cars, prevCars) => {
          console.log("deep ", cars.value, prevCars.value);
        },
        { deep: true }
      );
    },
  };
</script>

<style></style>
