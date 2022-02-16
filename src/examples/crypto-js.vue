<template>
  <div>
    <input type="text" v-model="value"><br>
    <button @click="saveData">Save</button>
  </div>
</template>

<script>

let CryptoJS = require("crypto-js");
export default {
  data(){
    return{
      value:''
    }
  },
  methods:{
    saveData(){
      //encrypt
      const variable = CryptoJS.AES.encrypt(this.value, 'secret key 123').toString();
      localStorage.setItem('userData', variable);
      console.log(variable);

      //decrypt
      let bytes = CryptoJS.AES.decrypt(variable, 'secret key 123');
      let originalText = bytes.toString(CryptoJS.enc.Utf8);
      console.log("-------------------------------------------")
      console.log(originalText); // 'my message'
    }
  }
}
</script>