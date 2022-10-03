<template>
  <div>
    <template v-if="error">{{ error }}</template>
    <template v-else-if="result < 0">Результат меньше нуля</template>
    <template v-else-if="result > 0">Результат больше нуля</template>
    <div class="main">
      <input type="text" v-model.number="op1">
      <input type="text" v-model.number="op2">
      <p class="result">{{ result }}</p>
    </div>
    <div class="keyboard">
      <button v-for="operation in operations" @click="calculateFunc(operation)" :key="operation">
        {{ operation}}
      </button>
    </div>
    <div class="keyboardNumbers">
      <input type="checkbox" v-model="selected" @checked="showKeyboard">
      <template v-if="selected === false">Показать клавиатуру</template>
      <template v-else>Скрыть клавиатуру</template>
      <div class="templateNumbers" v-if="selected === true">
        <button v-for="number in keyboardNumbers" :key="number" @click="throwNumber(number)">{{ number }}</button>
        <button @click="deleteNumber">Стереть</button>
        <div class="radioChoose">
          <input type="radio" id="op1" value="op1" v-model="activeOperand">
          <label for="op1">Первое значение</label>
          <input type="radio" id="op2" value="op2" v-model="activeOperand">
          <label for="op2">Второе значение</label>
        </div>
      </div>
    </div>
    <div class="logs">{{ logs }}</div>
  </div>
</template>

<script>

export default {
  name: 'CalcApp',
  data: () => ({
    op1: 0,
    op2: 0,
    result: 0,
    error: '',
    operations: ['Сложить', 'Отнять', 'Разделить', 'Умножить', 'Разделить целочисленно', 'Возвести в степень'],
    logs: {},
    selected: false,
    showKeyboard: false,
    keyboardNumbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0],
    activeOperand: 'op1'
  }),
  methods: {
    calculateFunc (operation) {
      this.error = ''
      switch (operation) {
        case 'Сложить': this.sum(); break
        case 'Отнять': this.sub(); break
        case 'Разделить': this.div(); break
        case 'Умножить': this.mult(); break
        case 'Разделить целочисленно': this.divFull(); break
        case 'Возвести в степень': this.pow(); break
      }
      const { op1, op2, result } = this
      // this.logs = { ...this.logs, [Date.now]: `${op1} ${operation} ${op2} = ${result}` }
      this.$set(this.logs, Date.now(), `${op1} ${operation} ${op2} = ${result}`)
    },
    sum () {
      const { op1, op2 } = this
      this.result = op1 + op2
    },
    div () {
      const { op1, op2 } = this
      if (op2 === 0) {
        this.error = 'На ноль делить нельзя'
      } else {
        this.result = op1 / op2
      }
    },
    sub () {
      const { op1, op2 } = this
      this.result = op1 - op2
    },
    mult () {
      const { op1, op2 } = this
      this.result = op1 * op2
    },
    divFull () {
      const { op1, op2 } = this
      if (op2 === 0) {
        this.error = 'На ноль делить нельзя'
      } else {
        this.result = Math.floor(op1 / op2)
      }
    },
    pow () {
      const { op1, op2 } = this
      this.result = Math.pow(op1, op2)
    },
    throwNumber (number) {
      const numberCollect = this[this.activeOperand]
      this[this.activeOperand] = Number(`${numberCollect}${number}`);
    },
    deleteNumber () {
      const numberCollect = this[this.activeOperand];

      this[this.activeOperand] = Math.trunc(numberCollect / 10);
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
