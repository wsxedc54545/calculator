<template>
  <div class="calculator">
    <div class="calculator__container">
      <div class="calculator__container__console">
        <p>{{ this.number }}</p>
      </div>
      <div class="calculator__container__input">
        <button
          v-for="(tokens, index) in buttons"
          :key="index"
          @click="clickButton(tokens)"
        >
          {{ tokens.token }}
        </button>
      </div>
    </div>
    <!-- <ul>
      <li v-for="item in arrayData">
        {{ item.name }} 有 {{ item.cash }} 元
        <button @click="storeMoney(item)">儲值</button>
      </li>
  </ul> -->
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      // buttons: ['1','1','1','1','1','1','1','1','1','1','1','1','1','1','1','1','1','1','1','1'],
      buttons: [
      { token :'AC'},
      { token : '←'},
      { token : '+/-'},
      { token : '÷'},
      { token : 7 },
      { token : 8 },
      { token : 9 },
      { token : 'X'},
      { token : 4 },
      { token : 5 },
      { token : 6 },
      { token : '-'},
      { token :  1 },
      { token :  2 },
      { token :  3 },
      { token : '+'},
      { token : '%'},
      { token :  0 },
      { token : '.'},
      { token : '='}],
      number: '0',
      hasNumber: false,
      // arrayData: [
      //   { name: '阿翔', age: 21, cash: 500 },
      //   { name: '小萱', age: 23, cash: 1000 },
      //   { name: '漂亮阿姨', age: 30, cash: 5000 }
      // ],
    }
  },
  methods: {
    clickButton(tokens) {
      const type = typeof(tokens.token)
      console.log(type);
      if ( type === 'number' && this.hasNumber) {
        this.number = this.number.concat(String(tokens.token))
      } else if ( type === 'number') {
        this.number = String(tokens.token)
        this.hasNumber = true
        // console.log();
      } else {
        console.log('gg');
      }
    },
    // storeMoney: function(item) {
    //     item.cash = item.cash + 500;
    //     console.log(item);
    // },
  }
}
</script>

<style lang="scss">
  .calculator {
    text-align: center;
    padding-top: 10%;
    &__container {
      margin: 0 auto;
      width: 450px;
      &__console {
        background: #7B7B7B;
        height: 90px;
        font-size: 55px;
        text-align: right;
        p {
          margin: 10px 10px 0;
          padding-top: 20px;
        }
      }
      &__input {
        display: flex;
        flex-wrap: wrap;
        // flex-direction: column;
        button {
          width: 25%;
          height: 100px;
        }
      }
    }
  }
</style>