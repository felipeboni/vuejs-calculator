<template>
  <div class="p-5 bg-calculator" style="max-width: 400px; margin: 50px auto">
    <div class="previous-calc me-2 pt-4">
      <transition name="slide">
        <div class="w-full text-end overflow-auto" v-if="animate">
          <span class="c-font">
            {{ calculusValue || 0 }}
          </span>
        </div>
      </transition>
    </div>

    <!-- Calculator Result -->
    <div
      class="w-full text-end text-white rounded me-2 overflow-auto"
      style="margin-top: -0.75rem"
    >
      <span class="c-font result">
        {{ calculatorValue || 0 }}
      </span>
    </div>

    <!-- Calculator buttons -->
    <div class="row justify-content-center">
      <div
        class="col-3 mb-1 px-1"
        v-for="n in calculatorElements"
        :key="n"
        :class="{ 'flex-fill': '0'.includes(n) }"
      >
        <div
          class="lead calculator-button text-white m-1"
          :class="{
            'bg-orange': ['×', '÷', '-', '+', '='].includes(n),
            'bg-light': ['C', '±', '%'].includes(n),
            'w-100 text-start ps-4': '0'.includes(n)
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
      operator: null,
      previousCalculatorValue: "",
      previousCalculatorValue: "",
      calculusValue: "",
      animate: false,
      animationDirection: "",
      animationPlayState: "paused",
    };
  },

  methods: {
    action(n) {
      /* Append value */
      if (!isNaN(n) || n === ".") {
        this.calculatorValue += n + "";
      }

      /* Clear value */
      if (n === "C") {
        this.calculatorValue = "";
        this.animate = false;
      }

      if (n === "%") {
        this.calculatorValue = this.calculatorValue / 100 + "";
      }

      if (["÷", "×", "-", "+"].includes(n)) {
        if (n === "÷") {
          n = "/";
        }

        if (n === "×") {
          n = "*";
        }

        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = "";

        this.animate = false;
      }
      
      if ("±" === n) {

        this.operator = n;
        this.previousCalculatorValue = -(this.calculatorValue);
        this.calculatorValue = -(this.calculatorValue);

        this.animate = false;
      }

      if (n === "=") {
        if (this.previousCalculatorValue && this.operator && this.calculatorValue) {
          this.animate = true;

          this.calculusValue =
            this.previousCalculatorValue + this.operator + this.calculatorValue;

          this.calculatorValue = eval(this.calculusValue);

          this.previousCalculatorValue = "";
          this.operator = null;
        }
      }
    },
  },
};
</script>

<style scoped>
.result {
  font-size: 64px;
  font-weight: lighter;
}

.calculator-button {
  background: #313131;
  font-size: 32px;
  font-weight: normal;
  line-height: 2.2em;
  width: 70px;
  height: 70px;
  cursor: pointer;
  border-radius: 999px;
  text-align: center;
  transition: all 200ms ease-out;
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

.calculator-button:hover {
  filter: brightness(125%);
}

.calculator-button.bg-orange:hover {
  filter: brightness(75%);
}

.previous-calc {
  color: #555;
  margin-right: 0.75rem !important;
  height: 50px;
}

/* Animations */
.slide-enter-active {
  animation: slide 700ms ease forwards;
}

.slide-leave-active {
  animation: slide 300ms ease forwards reverse;
}

@keyframes slide {
  from {
    transform: translateY(50%);
    opacity: 0;
  }
  to {
    transform: translateY(0%);
    opacity: 1;
  }
}

/* Hide scrollbar for Chrome, Safari and Opera */
*::-webkit-scrollbar {
  display: none !important;
}

/* Hide scrollbar for IE, Edge and Firefox */
* {
  -ms-overflow-style: none !important; /* IE and Edge */
  scrollbar-width: none !important; /* Firefox */
}
</style>
