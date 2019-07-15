<template>
  <div id="container">
    <!--
    <img src="calcvuejs/src/assets/thor-helmet.jpeg">

    <div id="title">
      <p>Calcula</p>
      <img src="calcvuejs/src/assets/title.png">
    </div>
    -->
    <div class="calculette">
      <div class="screen">{{current || '0'}}</div>
      <div @click="clear" class="btn"> AC </div>
      <div @click="neg" class="btn"> +/- </div>
      <div @click="percent" class="btn"> % </div>
      <div @click="divide" class="btn operator">/</div>
      <div @click="append('7')" class="btn">7</div>
      <div @click="append('8')" class="btn">8</div>
      <div @click="append('9')" class="btn">9</div>
      <div @click="multiply" class="btn operator">X</div>
      <div @click="append('4')" class="btn">4</div>
      <div @click="append('5')" class="btn">5</div>
      <div @click="append('6')" class="btn">6</div>
      <div @click="minus" class="btn operator">-</div>
      <div @click="append('1')" class="btn">1</div>
      <div @click="append('2')" class="btn">2</div>
      <div @click="append('3')" class="btn">3</div>
      <div @click="add" class="btn operator">+</div>
      <div @click="append('0')" class="btn zero">0</div>
      <div @click="dot" class="btn">.</div>
      <div @click="equal" class="btn operator">=</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    clear() {
      this.current = '';
    },
    neg() {
      this.current = this.current.charAt(0) === '-'? this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    dot() {
      if(this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => b / a;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(parseFloat(this.current),parseFloat(this.previous))}`
      this.previous = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #container {
    background-color: blue;
    width: 70%;
    height: 500px;
  }
  .calculette {
    margin: 0 auto;
    width: 400px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
  }

  .screen {
    grid-column: 1/5;
    background-color: cyan;
  }

  .zero {
    grid-column: 1/3;
  }

  .btn {
    background-color: #eee;
    border: 1px solid #000;
  }
</style>
