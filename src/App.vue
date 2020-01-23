<template>
  <div id="app">
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Volume</th>
          <th>ABV</th>
          <th>Brix</th>
          <th>Sugar</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><input id="name_0" type="text"></td>
          <td><input id="volume_0" type="number" v-model.number="volume_0"></td>
          <td><input id="abv_0" type="number" min="1" max="100" v-model.number="abv_0"></td>
          <td><input id="brix_0" type="number" min="1" max="100" v-model.number="brix_0"></td>
          <td><input id="sugar_0" type="number" min="1" max="100" v-bind:change="getSugar()"></td>
        </tr>
        <tr>
          <td><input id="name_1" type="text"></td>
          <td><input id="volume_1" type="number" v-model.number="volume_1"></td>
          <td><input id="abv_1" type="number" min="1" max="100" v-model.number="abv_1"></td>
          <td><input id="brix_1" type="number" min="1" max="100" v-model.number="brix_1"></td>
          <td><input id="sugar_1" type="number" min="1" max="100"></td>
        </tr>
        <tr>
          <td></td>
          <td>{{volume()}}</td>
          <td>{{abv()}}</td>
          <td>{{100 * sugar() / volume()}}</td>
          <td>{{sugar()}}</td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      volume_0: 0,
      abv_0: 0,
      brix_0: 0,
      sugar_0: 0,
      volume_1: 0,
      abv_1: 0,
      brix_1: 0,
      sugar_1: 0
  //     counter: 0,
  //     inputs: [{
  //       id: 'name_0',
  //       label: 'Name',
  //       value: ''
  //     },
  //     {
  //       id: 'abv_0',
  //       label: 'ABV',
  //       value: ''
  //     },
  //     {
  //       id: 'brix_0',
  //       label: 'Brix',
  //       value: ''
  //     }]
    }
  },
  methods: {
    volume() {
      return this.volume_0 + this.volume_1
    },
    abv() {
      return this.abv_0 + this.abv_1
    },
    brix() {
      return this.brix_0 + this.brix_1
    },
    sugar() {
      return this.sugar_0 + this.sugar_1
    },
    getSugar() {
      return ((100 / this.brix_0) * this.volume_0)
    }
    // addInput() {
    //   this.counter++
    //   this.inputs.push({
    //     id: `name_${this.counter}`,
    //     label: 'Name',
    //     value: ''
    //   },
    //   {
    //     id: `abv_${this.counter}`,
    //     label: 'ABV',
    //     value: ''
    //   },
    //   {
    //     id: `brix_${this.counter}`,
    //     label: 'Brix',
    //     value: ''
    //   });
    // }
  }
}
</script>

<style>
</style>
