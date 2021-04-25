<template>
  <div class="calculator">
    <div class="display">{{currentValue || '0'}}</div>
    <div @click="clear" class="button">A/C</div>
    <div @click="sign" class="button">+/-</div>
    <div @click="percent" class="button">%</div>
    <div @click="divide" class="button operator">÷</div>
    <div @click="append(7)" class="button">7</div>
    <div @click="append(8)" class="button">8</div>
    <div @click="append(9)" class="button">9</div>
    <div @click="multiply" class="button operator">x</div>
    <div @click="append(4)" class="button">4</div>
    <div @click="append(5)" class="button">5</div>
    <div @click="append(6)" class="button">6</div>
    <div @click="subtract" class="button operator">-</div>
    <div @click="append(1)" class="button">1</div>
    <div @click="append(2)" class="button">2</div>
    <div @click="append(3)" class="button">3</div>
    <div @click="add" class="button operator">+</div>
    <div @click="append(0)" class="button zero">0</div>
    <div @click="dot" class="button">.</div>
    <div @click="equal" class="button operator">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      currentValue: '',
      previousValue: null,
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.currentValue = '';
    },
    sign() {
      if(this.currentValue.charAt(0) !== '') {
        this.currentValue = this.currentValue.charAt(0) === '-' ? this.currentValue.slice(1) : `-${this.currentValue}`;
      }
    },
    percent() {
      this.currentValue = `${parseFloat(this.currentValue) / 100}`
    },
    append(number) {
      if(this.operatorClicked) {
        this.currentValue = '';
        this.operatorClicked = false;
      }
      this.currentValue = `${this.currentValue}${number}`;
    },
    dot() {
      if(this.currentValue.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPreviousValue() {
      this.previousValue = this.currentValue;
      this.operatorClicked = true;
    },
    add() {
      this.operator = (a,b) => a + b;
      this.setPreviousValue();
    },
    subtract() {
      this.operator = (a,b) => a - b;
      this.setPreviousValue();
    },
    multiply() {
      this.operator = (a,b) => a * b;
      this.setPreviousValue();
    },
    divide() {
      this.operator = (a,b) => a / b;
      this.setPreviousValue();
    },
    equal() {
      this.currentValue = `${this.operator(parseFloat(this.previousValue), parseFloat(this.currentValue))}`;
      this.previousValue = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  display: grid;
}

.display {
  grid-column: 1/5;
  background-color: #333;
  color: white;
}

.zero {
    grid-column: 1/3;
}

.button {
  background-color: #eee;
  border: 1px solid #999;
}

.operator {
  background-color: orange;
  color: white;
}
</style>
