<template>
  <div id="app">
    <header>
      <h1>Slushies</h1>
    </header>
    <div class="wrapper">
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Volume (ml)</th>
            <th>Brix</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(ingredient, index) in ingredients" v-bind:key="ingredient.id">
            <td>
              <label v-bind:for="`name_${index}`">Name</label>
              <input
                placeholder="e.g. rum, lime, simple syrup etc"
                v-bind:id="`name_${index}`"
                type="text"
                v-model="ingredient.name"
              />
            </td>
            <td>
              <label v-bind:for="`volume_${index}`">Volume</label>
              <input
                v-bind:id="`volume_${index}`"
                type="number"
                v-model.number="ingredient.volume"
                v-on:change="getSugar(ingredient.id)"
                v-on:keyup="getSugar(ingredient.id)"
              />
            </td>
            <td>
              <label v-bind:for="`brix_${index}`">Brix</label>

              <input
                v-bind:id="`brix_${index}`"
                type="number"
                min="1"
                max="100"
                v-model.number="ingredient.brix"
                v-on:change="getSugar(ingredient.id)"
                v-on:keyup="getSugar(ingredient.id)"
              />
            </td>
          </tr>
        </tbody>
      </table>
      <div class="ctas">
        <button class="button" v-on:click="addIngredient()">Add ingredient</button>
        <button
          class="button"
          :disabled="this.ingredients.length < 2"
          v-on:click="removeIngredient()"
        >Remove ingredient</button>
      </div>
      <div class="result" v-if="getBrix() > -1">
        <h2>{{getBrix().toFixed(2)}}</h2>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      ingredients: [{ id: 0, name: "", volume: 0, brix: 0, sugar: 0 }],
      counter: 0
    };
  },
  methods: {
    getSugar(idx) {
      this.ingredients[idx].sugar =
        (this.ingredients[idx].brix / 100) * this.ingredients[idx].volume;
    },
    getBrix() {
      return (
        (100 *
          this.ingredients.reduce((a, { sugar }) => a + Number(sugar), 0)) /
        this.ingredients.reduce((a, { volume }) => a + Number(volume), 0)
      );
    },
    addIngredient() {
      this.counter++;
      this.ingredients.push({
        id: this.counter,
        name: "",
        volume: 0,
        brix: 0,
        sugar: 0
      });
    },
    removeIngredient() {
      this.counter--;
      this.ingredients.pop();
    }
  }
};
</script>

<style>
@import "https://meyerweb.com/eric/tools/css/reset/reset.css";
@import "https://fonts.googleapis.com/css?family=Bungee+Shade&display=swap";
* {
  box-sizing: border-box;
}
html,
body {
  min-height: 100vh;
  background: linear-gradient(
    to right,
    #f76c6c 0%,
    #f76c6c 50%,
    #a8d0e6 50%,
    #a8d0e6 100%
  );
}

body {
  padding-bottom: 2em;
}

header {
  margin-bottom: 1em;
  padding: 2em;
}

.wrapper {
  width: 88%;
  margin: 0 auto;
  max-width: 768px;
}

h1 {
  text-align: center;
  font-family: "Bungee Shade";
  font-size: 2em;
}

table {
  table-layout: fixed;
  width: 100%;
  margin-bottom: 1em;
}

thead {
  display: none;
}

tbody tr {
  background-color: rgba(0, 0, 0, 0.05);
  padding: 1em;
  display: flex;
  flex-direction: column;
  border-radius: 5px;
  margin-bottom: 1em;
}

tr:last-child {
  margin-bottom: 0;
}

td {
  display: flex;
  flex-direction: column;
  margin-bottom: 1em;
}

.ctas {
  text-align: center;
}

@media only screen and (min-width: 1100px) {
  h1 {
    font-size: 8em;
  }

  thead {
    display: block;
  }

  tbody tr {
    flex-direction: row;
    background-color: transparent;
    padding: 0;
  }

  td {
    flex: 1;
    margin-right: 1em;
  }

  td:last-child {
    margin-right: 0;
  }

  .ctas {
    text-align: left;
  }

  label {
    display: none;
  }
}
</style>