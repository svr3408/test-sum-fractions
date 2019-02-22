<template>
  <div id="app">
    <div class="fractions">
      <template v-for="(fraction, index) in fractions">
        <Fraction
          v-bind:numerator="fraction.numerator"
          v-bind:denominator="fraction.denominator"
          v-bind:index="index"
          @changeNumerator="val => fraction.numerator = val"
          @changeDenominator="val => fraction.denominator = val"
          @eventDelete="val => fractions.splice( val, 1 )"
          :key="fraction.id"
        />
      </template>
      <span class="result">= {{summ}}</span>
    </div>
    <div v-show="alert !== ''" class="alert">{{alert}}</div>
    <button v-on:click="addElement()" class="button">add new element</button>
  </div>
</template>

<script>
import Fraction from './components/Fraction.vue'

export default {
  name: 'app',
  data() {
    return {
      fractions: [
        { 'id': 1, 'numerator': '', 'denominator': '' },
        { 'id': 2, 'numerator': '', 'denominator': '' },
      ],
      alert: '',
    }
  },
  methods: {
    addElement: function () {
      if ( this.fractions.length < 5 ) {
        this.fractions.push( { 'id': this.fractions[ this.fractions.length - 1 ].id + 1, 'numerator': '', 'denominator': '' } );
      } else {
        this.alert = 'Максимальное количество дробей 5';
      }
    },
  },
  computed: {
    summ: function () {
      // eslint-disable-next-line
      this.alert = '';
      return this.fractions.reduce( (sum, current, index) => {
        if ( current.numerator === '' || current.denominator === '' ) {
          return sum;
        } else if ( ( current.numerator > 99 || current.numerator < 1 ) ||
          ( current.denominator > 99 || current.denominator < 1 )
        ) {
          // eslint-disable-next-line
          this.alert = 'Значение в дроби ' + (index + 1) + ' введены неверно. Значение должно быть от 1 до 99.';
          return sum;
        }

        return sum + ( current.numerator / current.denominator );
      }, 0);
    },
  },
  components: {
    Fraction
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

#app > * {
  margin-bottom: 15px;
}

.fractions {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.alert {
  color: red;
}

.button {
  padding: 15px;
  border-radius: 5px;
}

.result {
  text-align: left;
  width: 170px;
}
</style>
