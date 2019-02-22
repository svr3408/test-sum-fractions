<template>
  <div class="fraction__wrapper">
    <div class="fraction">
      <input class="fraction__numerator" type="number" maxlength="2" min="1" max="99" size="2"
        v-bind:value="computedNumerator"
        v-on:input="$emit('changeNumerator', $event.target.value)">
      <div class="fraction__separator"></div>
      <input class="fraction__denominator" type="number" maxlength="2" min="1" max="99" size="2"
        v-bind:value="computedDenominator"
        v-on:input="$emit('changeDenominator', $event.target.value)">
    </div>
    <button v-show="index > 1" class="delete" v-on:click="$emit('eventDelete', index)"><span class="delete__sign" title="Удалить дробь">+</span></button>
  </div>

</template>

<script>
export default {
  name: 'Fraction',
  props: {
    numerator: String,
    denominator: String,
    index: Number,
  },
  computed: {
    computedNumerator: function () {
      return this.numerator;
    },
    computedDenominator: function () {
      return this.denominator;
    },
  },
}
</script>

<style scoped>
.fraction {
  width: 80px;
  margin: 10px;
  display: flex;
  flex-direction: column;
  align-items: center
}

.fraction__wrapper {
  display: flex;
  flex-direction: row;
  align-items: center;
  position: relative;
}

.fraction__wrapper:not(:last-of-type):after {
  content: '+';
  font-size: 3em;
}

.fraction__separator {
  margin-top: 1rem;
  margin-bottom: 1rem;
  width: 100%;
  border: 0;
  border-top: 1px solid rgba(0, 0, 0, 0.4);
}

.fraction__numerator,
.fraction__denominator {
  padding: 6px 12px;
  border-radius: 4px;
  width: 40px;
}

input:invalid {
  border-color: red;
}

.delete {
  position: absolute;
  top: -20px;
  left: 80px;
  border: 0;
  background: transparent;
}

.delete__sign {
  display: block;
  color: red;
  transform: rotate(45deg);
  font-size: 2em;
}
</style>
