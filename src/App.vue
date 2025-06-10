<script setup>

import {computed, reactive, ref} from 'vue';
 

const numbers = reactive(Array(75));
const numberInput = ref('');
const grid = computed(() => {
  
  return {
    B: numbers.slice(0, 15),
    I: numbers.slice(15, 30),
    N: numbers.slice(30, 45),
    G: numbers.slice(45, 60),
    O: numbers.slice(60, 75)
  };
});

const adicionar = () => {
  console.log('adicionar', numberInput.value);
  const num = parseInt(numberInput.value);
  if (isNaN(num) || num < 1 || num > 75) {
    alert('Por favor, insira um número válido entre 1 e 75.');
    numberInput.value = '';
    return;
  }
  numbers[num - 1] = num;

  numberInput.value = '';
};

const restart  = () =>{
  if (confirm('deseja reiniciar?', 'Sim', 'Não')){
    numbers.fill('');
  }
}
</script>

<template>
  <div id="app">
    <div class="header"></div>
    <div class="grid">
    <div class="numbers">
      <h1>B</h1>
      <div class="number" v-for="n in grid.B" :key="n">
        {{ n }}
      </div>
    </div>
    <div class="numbers">
      <h1>I</h1>
      <div class="number" v-for="n in grid.I" :key="n">
        {{ n }}
      </div>
    </div>
    <div class="numbers">
    <h1>N</h1>
    <div class="number" v-for="n in grid.N" :key="n">
      {{ n }}
    </div>
    </div>
    <div class="numbers">
    <h1>G</h1>
    <div class="number" v-for="n in grid.G" :key="n">
      {{ n }}
    </div>
    </div>
    <div class="numbers">
    <h1>O</h1>
    <div class="number" v-for="n in grid.O" :key="n">
      {{ n }}
    </div>
    </div>
  </div>
  
  <div class="footer">
    <button class="restart-btn" @click="restart">Reiniciar</button>
    
    <input type="text" v-model="numberInput" @keypress.enter="adicionar" placeholder="proximo número" />

    <button class="add-btn" @click="adicionar">Adicionar</button>
  </div>
  </div>
</template>

<style>
#app {
  display: flex;
  flex-direction: column;
  background-color: blanchedalmond;
 
  height: 100vh;
}
.grid{
  margin: 1rem;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  height: 100%;
  justify-content: space-around;

}
.header{
  height: 18vh;
}
h1 {
  font-size: 5vh;
  width: 4vw;
}

.add-btn, .restart-btn{
  border-radius: 10px;
  height: 2rem;
  width: 4rem;
}
.add-btn {
  background-color: rgba(16, 141, 22, 0.555);
}
.restart-btn{
  background-color: rgba(255, 0, 0, 0.314);
}

.numbers {
  display: flex;
  justify-content: center;
  height: 15px;
  align-items: center;
}

.footer{
  display: flex;
  padding: .2rem;
  margin-bottom: 2px;
  justify-content: end;
}
input {
  width: 6vw;
  margin: 0 .3rem;
}

.number {
  flex: 1 0 ;
  align-items: center;  
  justify-content: center;
  font-size: 5vw;
  text-align: center;
  
  background-color: #ffb7005b;
  border: 1px solid #fff;
  box-sizing:border-box
}
.last-number{
  background-color: #ffa6005b;
}
</style>
