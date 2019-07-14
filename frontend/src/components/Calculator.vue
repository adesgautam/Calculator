<template>
  <div class="hello">
    <!-- <h1>{{ msg }}</h1> -->
    
    <div>
      <h1 class="title">Calculator</h1>
    </div>
    <hr>
    
    <div>
      <b-container fluid>
        <b-row class="text-center">
          <b-col cols="2" class="text-center"></b-col>
          <b-col cols="4" class="text-center">
          <form>
            
            <div class="field">
              <label class="label">First Number</label>
              <b-form-input name="num1" v-model="num1" v-validate="'required|digits'" class="input" type="text"></b-form-input>
            </div>

            <div class="field" style="margin-top:13px;">
              <label class="label">Second Number</label>
              <b-form-input name="num2" v-model="num2" class="input" v-validate="'required|digits'" type="text"></b-form-input>
            </div>
            
          </form>
          </b-col>

          <b-col cols="4" class="text-left">
            <div><label class="label">Addition: {{ add }}</label></div>
            <div><label class="label">Multiplication: {{ mul }}</label></div>
            <div><label class="label">Subtraction: {{ sub }}</label></div>
            <div><label class="label">Division: {{ div }}</label></div>
          </b-col>

        </b-row>
      </b-container>
    </div>

    &nbsp;
    <div>
      <b-button variant="primary" v-on:click="postreq()">Calculate</b-button>  
    </div>

    &nbsp;
    <hr>

  </div>
</template>

<script>

import axios from 'axios';
import Vue from 'vue'
import VeeValidate from 'vee-validate'

/* eslint-disable */
Vue.use(VeeValidate)

export default {
  name: 'Calculator',
  
  data: function() {
    return {
      add: "", multi: "", sub: "", div: "", 
      num1: "", num2: ""
    }
  },

  methods: {
    postreq: function() {
      var data = {"num1": parseFloat(this.num1), "num2": parseFloat(this.num2)}

      /*eslint-disable*/
      console.log(data) 
      /*eslint-enable*/

      axios({ method: "POST", url: "http://127.0.0.1:8090/calc", data: data, headers: {"content-type": "text/plain" } }).then(result => { 
          // this.response = result.data;
          this.add = result.data['add']
          this.mul = result.data['mul']
          this.sub = result.data['sub']
          this.div = result.data['div']

          /*eslint-disable*/
          console.log(result.data) 
          /*eslint-enable*/

        }).catch( error => {
            /*eslint-disable*/
            console.error(error);
            /*eslint-enable*/
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
