<template lang='pug'>
.card.bordered
  .card-body
    MyCalculator
</template>

<script>
import MyCalculator from '@thombruce/calculator/src/components/Calculator.vue'

export default {
  components: {
    MyCalculator
  }
}
</script>
