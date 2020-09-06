<template>
  <div class="home">
    {{name}} {{lastName}}
    <h1> {{ fullName }} </h1>

    <h1> Carros </h1>
    <ul>
      <li
        v-for="car in cars"
        :key="car.id">
        {{car}}
      </li>
    </ul>

      <h1> Carros2 </h1>

    <ul class="cars2">
      <li v-for="car2 in filterBlackCar" :key="car2.id">
        {{car2}}
      </li>
    </ul>

  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  data() {
    return {
      name: 'james',
      lastName: 'bond',
      cars: [
        { id: 1, model: 'fusca', cor: 'black' },
        { id: 2, model: 'fusca', cor: 'white' },
        { id: 3, model: 'fusca', cor: 'blue' },
        { id: 4, model: 'fusca', cor: 'red' },
        { id: 5, model: 'gol', cor: 'blue' },
        { id: 6, model: 'gol', cor: 'white' },
        { id: 7, model: 'gol', cor: 'gray' },
        { id: 8, model: 'gol', cor: 'red' },
      ],
    };
  },
  computed: {
    fullName() {
      return `${this.name} ${this.lastName}`;
    },
    filterBlackCar() {
      const filterCar = this.cars.filter(({ cor }) => cor === 'red');
      return filterCar;
    },
  },
};
</script>

<style>
  .cars2 {
    background: green;
    color: black;
  }
</style>
