<template>
  <div id="app">
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Volume</th>
          <th>Brix</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, index) in rows" v-bind:key="row.id">
          <td>
            <input v-bind:id="`name_${index}`" type="text" v-model="row.name" />
          </td>
          <td>
            <input
              v-bind:id="`volume_${index}`"
              type="number"
              v-model.number="row.volume"
              v-on:change="getSugar(row.id)"
            />
          </td>
          <td>
            <input
              v-bind:id="`brix_${index}`"
              type="number"
              min="1"
              max="100"
              v-model.number="row.brix"
              v-on:change="getSugar(row.id)"
            />
          </td>
        </tr>
        <tr>
          <td>
            <button v-on:click="addRow()">Add row</button>
          </td>
        </tr>
        <tr>
          <td v-if="getBrix() > -1">{{getBrix().toFixed(2)}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      rows: [{ id: 0, name: "", volume: 0, brix: 0, sugar: 0 }],
      counter: 0
    };
  },
  methods: {
    getSugar(idx) {
      this.rows[idx].sugar =
        (this.rows[idx].brix / 100) * this.rows[idx].volume;
    },
    getBrix() {
      return (
        (100 * this.rows.reduce((a, { sugar }) => a + Number(sugar), 0)) /
        this.rows.reduce((a, { volume }) => a + Number(volume), 0)
      );
    },
    addRow() {
      this.counter++;
      this.rows.push({ id: this.counter, name: "", volume: 0, brix: 0 });
    }
  }
};
</script>

<style>
html,
body {
  min-height: 100vh;
}
body {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
