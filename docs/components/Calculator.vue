<template lang='pug'>
div
  .card.bordered
    .card-body
      .flex.flex-col.gap-4
        .card.glass
          .card-body.text-right.text-4xl.font-mono
            | {{ displayValue }}
        .grid.grid-cols-4.gap-4
          button.btn(v-if="isAllClear" @click='allClear()') AC
          button.btn(v-else @click='clear()') C
          button.btn(@click='negate()') +/-
          button.btn(disabled='disabled') %
          button.btn(@click='divide()') ÷
          button.btn(@click="addNumeral('7')") 7
          button.btn(@click="addNumeral('8')") 8
          button.btn(@click="addNumeral('9')") 9
          button.btn(@click='multiply()') ×
          button.btn(@click="addNumeral('4')") 4
          button.btn(@click="addNumeral('5')") 5
          button.btn(@click="addNumeral('6')") 6
          button.btn(@click='minus()') -
          button.btn(@click="addNumeral('1')") 1
          button.btn(@click="addNumeral('2')") 2
          button.btn(@click="addNumeral('3')") 3
          button.btn(@click='plus()') +
          button.btn.col-span-2(@click="addNumeral('0')") 0
          button.btn(@click="addDecimal()") .
          button.btn(@click="equals()") =
</template>

<script>
export default {
  data () {
    return {
      storedValue: 0,
      displayValue: '0',
      currentExpression: '',
      newEntry: true
    }
  },
  computed: {
    isAllClear () {
      return (this.displayValue == '0' && this.newEntry == true)
    }
  },
  methods: {
    allClear () {
      this.storedValue = 0
      this.displayValue = '0'
      this.currentExpression = ''
      this.newEntry = true
    },
    clear () {
      this.displayValue = '0'
      this.newEntry = true
    },
    negate () {
      if (this.newEntry) {
        this.displayValue = '-0'
        this.newEntry = false
      } else if (this.displayValue.startsWith('-')) {
        this.displayValue = this.displayValue.slice(1)
      } else {
        this.displayValue = '-' + this.displayValue
      }
    },
    addNumeral (numeral) {
      if (this.newEntry) {
        this.displayValue = numeral
        this.newEntry = false
      } else if (this.displayValue.match(/^-?0$/)) {
        this.displayValue = this.displayValue.replace('0', numeral)
      } else {
        this.displayValue += numeral
      }
    },
    addDecimal () {
      if (this.newEntry) {
        this.displayValue = '0.'
        this.newEntry = false
      } else if (!this.displayValue.match(/\./)) {
        this.displayValue += '.'
      }
    },
    plus () {
      this.currentExpression += this.displayValue + ' + '
      this.newEntry = true
    },
    minus () {
      this.currentExpression += this.displayValue + ' - '
      this.newEntry = true
    },
    multiply () {
      this.currentExpression += this.displayValue + ' * '
      this.newEntry = true
    },
    divide () {
      this.currentExpression += this.displayValue + ' / '
      this.newEntry = true
    },
    equals () {
      this.currentExpression += this.displayValue
      this.displayValue = '' + eval(this.currentExpression)
      this.currentExpression = ''
      this.newEntry = true
    }
  }
}
</script>
