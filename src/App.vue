<script setup>
import { reactive } from 'vue';

//document.querySelector('h1').innerHTML = nome
const nome = "humberto nacif"
const meuObj = {
  nome: 'humberto',
  gameFavorito: 'Elden Ring'
}

const enderecoDaImagemTFT = 'https://play-lh.googleusercontent.com/EtRQL2UMBjVl7i8mRfjo2HycCmFdNppZdWxOYbcw0EUrxMxj_wyHyrtj9WkF2MhVDwE';
const enderecoDaImagemAutoChess = 'https://play-lh.googleusercontent.com/7htzNK-amlNInRiO9xTZ_Rjc5WcThsLKgcoOSVaWqukhuOPar_P2POsJH0tx9G3g3gD3'

const botaoEstaDeabilitado = true

const gostaDeTFT = false
const gostaDeAutoChess = false

const estaAutorizado = false

//let contador = 0
const estado = reactive({
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
})

function dizOla(nome) {
  return `${nome} diz oi`;
}

function incrementar() {
  estado.contador ++;
}

function decrementar() {
  estado.contador--;
}

function alteraEmail(evento) {
  estado.email = evento.target.value;
}

function mostraSaldoFuturo() {
  const { saldo, transferindo } = estado 
  return saldo - transferindo;
}

function validaValorDeTransferência() {
  const { saldo, transferindo } = estado 
  return saldo <= transferindo;
}

</script>

<template>
  <h1>{{ dizOla('humberto') }}</h1>
  <img v-if="gostaDeTFT" :src="enderecoDaImagemTFT" alt="">
  <img v-else-if="gostaDeAutoChess" :src="enderecoDaImagemAutoChess" alt="">
  <h2 v-else>Não curte xadrez automático?</h2>

  <h1 v-if="estaAutorizado">Bem-vindo</h1>
  <h1 v-else>Não possui acesso</h1>

  <button :disabled="botaoEstaDeabilitado">enviar mensagem</button>

  <br />
  <hr />

  {{ estado.contador }}

  <button @click="incrementar()" type="button">+</button>
  <button @click="decrementar()" type="button">-</button>

  <br />
  <hr />

  {{ estado.email }}
  <input type="email" @keyup="alteraEmail">
  
  <br />
  <hr />

  Saldo: {{ estado.saldo }}<br />
  Transferindo: {{ estado.transferindo }}<br />
  Saldo depois da transferência: {{ mostraSaldoFuturo() }}<br />
  <input class="campo" :class="{ invalido: validaValorDeTransferência() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir">
  <button v-if="!validaValorDeTransferência()">Transferir</button>
  <span v-else>Valor maior que o saldo</span>

</template>

<style scoped>

img {
  max-width: 200px;
}

.invalido {
  outline-color: red;
  border-color: red;
}

.campo {
  background-color: cyan;
}

</style>
