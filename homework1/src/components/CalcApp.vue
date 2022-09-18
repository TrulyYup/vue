<template>
  <div>
    <div class="main">
      <input type="text" v-model.number="op1">
      <input type="text" v-model.number="op2">
      <p class="result">{{ result }}</p>
    </div>
    <div class="keyboard">
      <button @click="sum">Сложить</button>
      <button @click="sub">Отнять</button>
      <button @click="mult">Умножить</button>
      <button @click="div">Разделить</button>
      <button @click="divFull">Разделить целочисленно</button>
      <button @click="pow">Возвести в степень</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalcApp',
  data: () => ({
    op1: 0,
    op2: 0,
    result: 0
  }),
  methods: {
    sum () {
      this.result = this.op1 + this.op2
    },
    div () {
      this.result = this.op1 / this.op2
    },
    sub () {
      this.result = this.op1 - this.op2
    },
    mult () {
      this.result = this.op1 * this.op2
    },
    divFull () {
      this.result = Math.floor(this.op1 / this.op2)
    },
    pow () {
      this.result = Math.pow(this.op1, this.op2)
    }
  }
}
</script>

<style lang="scss">
.main {
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  max-width: 200px;

  & input {
    text-align: center;
  }

  & result {
    font-weight: bold;
  }
}

.keyboard {
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  max-width: 200px;

}
</style>
