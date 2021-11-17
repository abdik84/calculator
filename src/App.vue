<template>
  <div id="app">
    <div class="container">
      <h3>Simple Calculator</h3>
      <div class="row" v-for="(input, i) in inputs" :key="i">
        <div class="col">
          <input type="number" v-model="input.value">
        </div>
        <div class="col">
          <input class="checkbox" type="checkbox" v-model="input.checked">
        </div>
      </div>
      <div class="row" style="margin-top: 10px;">
        <div class="col" v-for="button in buttons" :key="button">          
          <button @click="calculate(button)">
            {{ button }}
          </button>
        </div>
      </div>
      <div class="divider"/>
      <h3>Result: {{ result }}</h3>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      inputs: [
        { value: null, checked: false },
        { value: null, checked: false },
        { value: null, checked: false },
      ],
      buttons: ['+', '-', '*', '/'],
      result: null
    }
  },
  methods: {
    calculate(operator) {
      // reset result
      this.result = null
      // Validate checkbox
      if(this.inputs.filter(item => item.checked).length < 2) return alert("Please check at least 2 input!")

      let err = null
      let result = ''
      this.inputs.map(input => {
        // Make sure all input has value
        if(!input.value) return err = 'All input is required!'
        if(input.checked) result += result.length ? ` ${operator} ${input.value}` : input.value
      })

      if(err) return alert(err)

      this.result = eval(result) % 1 != 0 ? eval(result).toFixed(2) : eval(result)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.container {
  display: block;
  padding: 10px;
  border: 1px solid #cccccc;
  width: 250px;
}

.row {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-bottom: 10px;
}

.col {
  flex: 1 1 auto;
  margin: 5px;
}

input[type=number] {
  padding: 10px;
}

input[type=checkbox] {
  -ms-transform: scale(2); /* IE */
  -moz-transform: scale(2); /* FF */
  -webkit-transform: scale(2); /* Safari and Chrome */
  -o-transform: scale(2); /* Opera */
  transform: scale(2);
}

button {
  padding: 5px;
  width: 100%;
  border-radius: 8px;
}

.divider {
  border-bottom: 1px solid #cccccc;
  margin: 10px 0px;
}
</style>
