<template>
  <div class="calculator">
    <div class="calculator__container">
      <div class="calculator__container__console">
        <p class="ellipsis">{{ this.number }}</p>
      </div>
      <div class="calculator__container__input">
        <button
          v-for="(tokens, index) in buttons"
          :key="index"
          :class="`${tokens.type}`"
          @click="clickButton(tokens)"
        >
          {{ tokens.token }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      buttons: [
      { token :'AC', type: 'operation' },
      { token : '←', type: 'operation'},
      { token : '+/-', type: 'operation'},
      { token : '/', type: 'operation'},
      { token : 7, type: 'number' },
      { token : 8, type: 'number' },
      { token : 9, type: 'number' },
      { token : '*', type: 'operation'},
      { token : 4, type: 'number' },
      { token : 5, type: 'number' },
      { token : 6, type: 'number' },
      { token : '-', type: 'operation'},
      { token :  1, type: 'number' },
      { token :  2, type: 'number' },
      { token :  3, type: 'number' },
      { token : '+', type: 'operation'},
      { token : '%', type: 'operation'},
      { token :  0, type: 'number' },
      { token : '.', type: 'operation'},
      { token : '=', type: 'operation'}],
      number: '0',
      hasNumber: false,
      hasfloat: 'false',
      calc: [],
    }
  },
  head() {
    return {
      title: '測試計算機',
    }
  },
  methods: {
    clickButton(tokens) {
      const temp = tokens.token
      const isNumber = typeof(temp) === 'number'

      if ( isNumber && !this.hasNumber ) {
        if ( temp === 0 && this.hasfloat === false && this.calc === [] )
          return
        this.number = String(tokens.token)
        this.hasNumber = true
      } else if ( isNumber  ) {
        if ( temp === 0 && this.number.length === 1 )
          return
        this.number = this.number.concat(String(temp))
      } else {
        switch (temp) {
          case 'AC':
            this.resetCal()
            break;
          case '←':
            if( this.number.length > 1)
              this.number = this.number.slice(0, -1)
            else
              this.resetCal()
            break;
          case '+/-':
            this.number = String(this.number*=-1)
            break;
          case '%':
            this.number = String(this.number/=100)
            break;
          case '.':
            if ( this.hasfloat === true )
              return
            this.number+='.'
            this.hasNumber = true
            this.hasfloat = true
            break;
          case '=':
            if ( !this.hasNumber )
              return
            this.calc.push(this.number)
            this.calculate()
            break;
          default:
            if ( !this.hasNumber )
              return
            this.hasNumber = true
            this.calc.push(this.number)
            this.calc.push(temp)
            this.hasNumber = false
            this.hasfloat = false
          break;
        }
      }
    },
    resetCal() {
      this.number = '0' 
      this.hasNumber = false
      this.hasfloat = false
      this.calc = []
    },
    calculate (temp) {
      this.number = String(eval(this.calc.join('')))
      this.calc = []
      if (this.isFloat(this.number))
        this.hasfloat = false
    },
    isFloat(n){
      return !(parseInt(n) < parseFloat(n))
    }
  }
}
</script>

<style lang="scss">
  body{
    overflow-y: hidden;
    overflow-x: hidden;
  }
  .calculator {
    text-align: center;
    padding-top: 10%;
    
    @media (max-width: 768px) {
      padding-top: 40%;
    }
    &__container {
      margin: 0 auto;
      width: 500px;
      height: 50%;
      @media (max-width: 768px) {
        padding-top: 0;
        width: 50%;
      }
      &__console {
        position: relative;
        background: #fff;
        height: 90px;
        font-size: 55px;
        text-align: right;
        border-radius: 40px 40px 0 0;
        border-bottom:1px solid #939699;
        @media (max-width: 768px) {
          border-radius: 20px 20px 0 0;
        }
        p {
          font-size: 28px;
          padding: 8%;
          overflow: hidden;
          white-space: nowrap;
          text-overflow: ellipsis;
          @media (max-width: 768px) {
            padding: 20% 2%;
          }
        }
      }
      &__input {
        display: flex;
        flex-wrap: wrap;
        button {
          width: 25%;
          height: 100px;
          border: 0;
          outline: none;
          background: #fff;
        }
        button:hover {
          background: lightgrey;
        }
        @media (max-width: 768px) {
          button {
            width: 25%;
            height: 50px;
          }
        }
      }
    }
  }
</style>