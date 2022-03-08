<template>
  <div class="p-5 bg-calculator" style="max-width: 400px; margin: 50px auto">
    <!-- Calculator Result -->
    <div class="w-full text-end text-white rounded me-2 pt-5">
      <span class="c-font result">
        {{ calculatorValue || 0 }}
      </span>
    </div>

    <!-- Calculator buttons -->
    <div class="row justify-content-center">
      <div class="col-3 mb-1 px-1" v-for="n in calculatorElements" :key="n"
      :class="{'flex-fill': '0'.includes(n)}"
      >
        <div
          class="lead calculator-button text-white m-1"
          :class="{'bg-orange': ['×','÷', '-', '+', '='].includes(n), 'bg-light': ['AC','±', '%'].includes(n), 'w-100 text-start ps-4': '0'.includes(n)}"
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
        "AC",
        "±",
        "%",
        "÷",
        7,
        8,
        9,
        "×",
        4,
        5,
        6,
        "-",
        1,
        2,
        3,
        "+",
        0,
        ".",
        "=",
      ],
    };
  },
};
</script>

<style scoped>
.result {
  font-size: 64px;
  font-weight: lighter;
}

.bg-calculator {
  background: #000;
  border-radius: 1.5rem;
}

.bg-orange {
  background: #f59806 !important;
  line-height: 1.75em !important;
  font-size: 38px !important;
}

.bg-light {
  background: #9e9e9e !important;
  color: #000 !important;
  line-height: 1.75em !important;
  font-size: 38px !important;
  font-weight: normal !important;
}

.bg-orange:hover {
  background: #bb7606 !important;
}

.calculator-button {
  background: #313131;
  font-size: 32px;
  font-weight: normal;
  line-height: 2.2em;
  width: 70px;
  height: 70px;
  cursor: pointer;
  transition: all 100ms ease-out;
  border-radius: 999px;
  text-align: center;
}

.calculator-button:hover {
  background: #494949;
}
</style>
