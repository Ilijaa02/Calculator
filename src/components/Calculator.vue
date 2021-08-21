<template>
  <div class="p-3 app">
    <div
      class="
        w-100
        rounded
        p-2
        text-end
        lead
        text-white
        mb-2
        calc-body
      "
      style="font-family: consolas; font-size: 23px"
    >
      {{ calculatorValue || 0 }}
    </div>
    <div class="row">
      <div class="col-3" v-for="n in calculatorElements" :key="n">
        <div
          class="lead text-white text-center my-1 py-3 rounded button"
          :class="{
            'bg-green': ['C', '*', '/', '-', '+', '%', '='].includes(n),
          }"
          @click="action(n)"
        >
          {{ n }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      calculatorValue: "",
      calculatorElements: [
        "C",
        "*",
        "/",
        "-",
        "7",
        "8",
        "9",
        "+",
        "4",
        "5",
        "6",
        "%",
        "1",
        "2",
        "3",
        "=",
        "0",
        ".",
      ],
      operator: null,
      previousCalculatorValue: "",
    };
  },
  methods: {
    action(n) {
      if (!isNaN(n) || n === ".") {
        this.calculatorValue += n;
      }
      if (n === "C") {
        this.calculatorValue = "";
      }
      if (n === "%") {
        this.calculatorValue /= 100;
      }
      if (["/", "*", "-", "+"].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = "";
      }
      if (n === "=") {
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );

        this.previousCalculatorValue = "";
        this.operator = null;
      }
    },
  },
};
</script>

<style scoped>
.app {
  max-width: 370px;
  margin: 50px auto;
  background-color: rgb(133, 133, 133);
  border-radius: 10px;
  box-shadow: 10px 10px 30px rgb(0, 0, 0);
}
@media screen and (max-width: 370px) {
  .app {
    margin-left: 15px;
    margin-right: 15px;
    margin-top: 15px;
  }
  .button{
    padding: 5px !important;
  }
}
.calc-body, .button{
    background-color: rgb(153, 153, 153);
    border: 1px solid whitesmoke;
    font-size: 25px !important;
}
.button:hover {
  cursor: pointer;
  background: rgb(219, 219, 219) !important;
  color: black !important;
  border: 1px solid black;
  transform: scale(1.1);
}
.button {
  transition: 0.5s;
  width: 100%;
}
.bg-green {
  background-color: rgb(41, 41, 41) !important;
}
</style>