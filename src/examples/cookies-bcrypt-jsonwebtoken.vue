<template>
  <div>
    <input type="text" v-model="userName">
    <button @click="setCookies">Set Cookie</button>
    <button @click="removeCookies">Remove Cookies</button>
    <button @click="bcryptToken">BCRYPT Cookies</button>
    <button @click="compareBcrypt">Compare BCRYPT</button>
    <button @click="tokenJwt">Jwt</button>
    <button @click="decodedToken">Decode Jwt</button>
  </div>
</template>

<script>
import bcrypt from "bcryptjs";
import jwt from "jsonwebtoken";
export default {
  data() {
    return {
      userName: '',
      hashValue: '',
      privateKey:'1233344',
      token:null
    }
  },
  methods: {
    setCookies() {
      this.$cookies.set("token", this.userName, Infinity)
    },
    removeCookies() {
      this.$cookies.remove("token");
    },
    bcryptToken() {
      const dataValue = this;
      bcrypt.genSalt(10, function (err, salt) {
        bcrypt.hash(dataValue.userName, salt, function (err, hash) {
          if (err) {
            console.log(err);
          } else {
            console.log(`HASH: ${hash}`);
            dataValue.hashValue = hash;
          }
        });
      });
    },
    compareBcrypt() {
      const dataValue = this;
      bcrypt.compare(dataValue.userName, dataValue.hashValue, function (err, res) {
        if (res){
          console.log("success ....");
        }
        else{
          console.log("not equal");
        }
      });
    },
    tokenJwt(){
      this.token = jwt.sign({ user: this.userName }, this.privateKey);
      console.log(this.token);
    },
    decodedToken(){
      const decoded = jwt.verify(this.token, this.privateKey);
      console.log(decoded) // bar
    }
  }
}
</script>