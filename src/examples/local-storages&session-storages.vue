<template>
  <div>
    <input type="text" v-model="value"><br>
    <button @click="saveValue">Save</button>
    <hr>
    <span>{{newValue}}</span><br>
    <span>{{newValue2}}</span><br>
    <button @click="removeLocalData">Remove</button>
  </div>
</template>

<script>

export default {
  data(){
    return{
      value:'',
      newValue:'',
      newValue2:'',
      foo: {name: "vue", age: "34"}
    }
  },
  methods:{
    saveValue(){
      //local storagede json olarak veri kaydetmek için aşağıdaki yapı kullanılır.
      //localStorage.setItem('input-value', JSON.stringify(this.foo));
      //local storagede kaydedilen veriyi json olarak geri çağırmak için aşağıdaki yapı kullanılır.
      // JSON.parse(localStorage.getItem("input-value"));


      localStorage.setItem('input-value', this.value);
      sessionStorage.setItem('input-newValue', this.value);
      this.value = ''
    },
    removeLocalData(){
      localStorage.removeItem('input-value');
      // clear() ile local storagedeki tüm datalar silinir
      // localStorage.clear();
    }
  },
  mounted(){
    if (localStorage.getItem('input-value')){
      this.newValue = localStorage.getItem('input-value')
    }
    if (sessionStorage.getItem('input-newValue')){
      this.newValue2 = sessionStorage.getItem('input-newValue')
    }
  }
}
</script>