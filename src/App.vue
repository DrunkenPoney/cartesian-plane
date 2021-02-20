<template>
  <!--<img alt="Vue logo" src="./assets/logo.png" />-->
  <div class="options-wrapper">
    <div>
      <label for="size">Size: </label>
      <input type="number" id="size" v-model="size" />
    </div>
    <div>
      <label for="steps">Steps: </label>
      <input type="number" id="steps" v-model="steps" />
    </div>
    <div>
      <label for="lblStep">Label Step: </label>
      <input type="number" id="lblStep" v-model="lblStep" />
    </div>
    <div>
      <label for="xValStep">X Value Step: </label>
      <input type="number" id="xValStep" v-model="xValStep" />
    </div>
    <div>
      <label for="yValStep">Y Value Step: </label>
      <input type="number" id="yValStep" v-model="yValStep" />
    </div>
  </div>
  <CartesianPlane :steps="steps"
    :size="size"
    :lblStep="lblStep"
    :xValStep="xValStep"
    :yValStep="yValStep" />
</template>

<script>
import CartesianPlane from "./components/CartesianPlane.vue";
export default {
  name: "App",
  components: {
    CartesianPlane
  },
  data() {
    return {
      steps: 20,
      size: 800,
      lblStep: 2,
      xValStep: 1,
      yValStep: 10
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.options-wrapper {
  display: flex;
  justify-content: space-around;
  align-items: stretch;
  flex-wrap: wrap;
  margin-bottom: 1em;
}

.options-wrapper > div {
  margin: 0.5em 0.25em;
}

[readonly], [readonly]:focus {
  background: #EEE;
  border: 1px solid #AAA;
  outline: none;
}

@media print {
  .options-wrapper {
    display: none;
  }
}
</style>
