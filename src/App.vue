<template>
  <div id="app">
    <div>
      <p>{{ msg }}</p>
      <input type="text" id="age" v-model="age">歳
      <p class="valid-err">{{ validationErrMsg }}</p>
    </div>
    <div>
      <button class="button" v-on:click="check">確認</button>
    </div>
    <div>
      <p>{{ resultMsg }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      age: null,
      msg: 'あなたは何歳ですか？',
      validationErrMsg: '',
      resultMsg: ''
    }
  },
  methods: {
    check: function() {
      if (!this.validAge(this.age)) {
        this.validationErr();
        return;
      } else if (this.age < 0 || this.age > 130) {
        this.validationErr();
        return;
      }
      if (this.age >= 0 && this.age <= 19) {
        this.resultMsg = 'あなたは未成年です';
        this.validationErrMsg = '';
        return;
      } else if (this.age >= 20 && this.age <= 99) {
        this.resultMsg = 'あなたは成人です';
        this.validationErrMsg = '';
        return;
      }
      this.resultMsg = 'とても長生きです';
      this.validationErrMsg = ''; 
    },
    validAge(age) {
      if (age === null || age === undefined) return false;
      const re = /^[0-9]+$/;
      return re.test(age);
    },
    validationErr () {
      this.validationErrMsg = '0以上130以下の整数を入力してください';
      this.resultMsg = '';
      return;
    }
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
}

#age {
  width: 3rem;
  margin: 0.5rem;
}

.valid-err {
  color: red;
}

button {
  margin-bottom: 1rem;
}
</style>
