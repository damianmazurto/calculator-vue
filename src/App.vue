<template>
  <div class="container">
    <div id="calculator">
      <input id="screen" type="text" v-model="message" />
      <div class="buttons">                        
        
        <div v-on:click="input('7')" class="button">7</div>
        <div v-on:click="input('8')" class="button">8</div>
        <div v-on:click="input('9')" class="button">9</div>
        <div v-on:click="operator('/')" class="button">/</div>
        <div v-on:click="input('4')" class="button">4</div>
        <div v-on:click="input('5')" class="button">5</div>
        <div v-on:click="input('6')" class="button">6</div>
        <div v-on:click="operator('*')" class="button">*</div>
        <div v-on:click="input('1')" class="button">1</div>
        <div v-on:click="input('2')" class="button">2</div>
        <div v-on:click="input('3')" class="button">3</div>
        <div v-on:click="operator('-')" class="button">-</div>
        <div v-on:click="equal" class="button">=</div>        
        <div v-on:click="input('0')" class="button">0</div>
        <div v-on:click="input('.')" class="button">.</div>
        <div v-on:click="operator('+')" class="button">+</div>
        
        <div v-on:click="clearAll" class="button">CE</div>
        <div v-on:click="clearInput" class="button">C</div>
        
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'calculator',
  data () {
      return {
      value: '',
      message: '0',
      equation: '',
      cal: ''
    }
  },
  methods: {
    input: function(num) {
      if(num == '.' && this.message.includes('.'))
        return;
      else if(this.message == '0'){
        this.message = num;
        this.value = num;
      }    
      else {
        this.value += num;
        this.message = this.value;
      } 
    },
    clearAll: function() {
      this.equation = '';
      this.message = '0';
      this.value = '';
    },
    clearInput: function() {
      this.message = '0';
      this.value = '';
    },
    operator: function(opt) {
      if(this.equation == '' && this.value == '' || this.value == '.')
        return;
      this.cal = opt;
      this.equation += this.value;
      this.message = eval(this.equation).toString();
      this.equation = this.message;
      this.equation += opt;
      this.value = '';
    },   
    equal: function() {
      if(this.equation == '')
        return;
      if(this.cal !== '')
        this.equation += this.message;
      this.message = eval(this.equation).toString();      
      this.value = '';
      this.cal = '';
      this.equation = this.message;
    }
  }
}

</script>

<style lang="scss">
.container {
  height: 50rem;
  display: flex;
  align-items: center;
  justify-content: center;
  
  #calculator {
    display: flex;
    flex-direction: column;
    width: 20rem;
    background-color: #7dc7e6;
    padding: 20px;
    #screen {
      padding-bottom: 1.5rem;
      font-size: 4.5rem;
      text-align: right;
      border: 2px solid #a6a6a7;
      border-radius:0;
    }
    .buttons {
      user-select: none;
      cursor: pointer;
      font-size: 1.5rem;
      display: flex;
      flex-wrap: wrap;

      .button {
        display: flex;
        flex-grow: 1;
        width: 50px;
        height: 50px;
        margin: 10px 15px;
        align-items: center;
        justify-content: center;
        text-align: center;
        border: #c1c2c2 2px solid;
        background-color: #dddddd;
        box-sizing: border-box;
      }
    
      .button:hover {
        filter: opacity(0.8);
      }
      .button:active {
        box-shadow: 2px 2px 5px #333 inset;
      }
    }
    
  }
}
</style>
