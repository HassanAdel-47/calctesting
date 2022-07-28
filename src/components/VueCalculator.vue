<template>
  <div
    class="p-3"
    style="max-width: 400px; margin: 50px auto; background: #234"
  >
    <!--Calculator Result-->
    <div
      class="text-end w-full rounded m-1 p-3 lead font-weight-bold text-white text-white bg-vue-dark"
    >
      {{ CalculatorValue || 0 }}
    </div>
    <!-- Calculator Buttons -->
    <div class="row no-gutters">
      <div class="col-3" v-for="n in CalculatorElements" :key="n">
        <div
          class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          :class="{
            'bg-vue-green': ['C', '*', '/', '-', '+', '%', '='].includes(n),
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
  name: "VueCalculator",
  props: {
    msg: String,
  },
  data() {
    return {
      CalculatorValue: "",
      CalculatorElements: [
        "C",
        "*",
        "/",
        "-",
        7,
        8,
        9,
        "+",
        4,
        5,
        6,
        "%",
        1,
        2,
        3,
        "=",
        0,
        ".",
      ],
      operator: null,
      previouscalculatorValue: "",
    };
  },
  methods: {
    action(n) {
      // Append Value
      if (!isNaN(n) || n === ".") {
        this.CalculatorValue += n + "";
      }
      // Clear Value
      if (n === "C") {
        this.CalculatorValue = "";
      }
      // Percentage Value
      if (n === "%") {
        this.CalculatorValue = this.CalculatorValue / 100;
      }

      if (["/", "*", "+", "-"].includes(n)) {
        this.operator = n;
        this.previouscalculatorValue = this.CalculatorValue;
        this.CalculatorValue = "";
      }

      if (n === "=") {
        this.CalculatorValue = eval(
          this.previouscalculatorValue + this.operator + this.CalculatorValue
        );

        (this.previouscalculatorValue = ""), (this.operator = null);
      }
    },
  },
};
</script>

<style scoped>
.bg-vue-dark {
  background: #31475e;
}
.hover-class:hover {
  cursor: pointer;
  background: #3d5875;
}
.bg-vue-green {
  background: #3fb984;
}
</style>
