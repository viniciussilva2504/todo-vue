<script setup>
import {reactive} from 'vue';
const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      título: 'Estudar ES6',
      finalizada: false,
    },
    {
      título: 'Estudar SASS',
      finalizada: true,
    },
    {
      título: 'Ir para a academia',
      finalizada: true, 
    }
]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}
const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}
const getTarefasFiltradas = () => {
  const {filtro} = estado;
  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}
const cadastraTarefa = () => {
  const tarefaNova = {
    título: estado.tarefaTemp, 
    finalizada: false, 
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}
</script>

<template>
<div class="container">
  <header class="p-5 mb-4 bg-light ronded-3">
    <h1>Minhas Tarefas</h1>
    <p>
      Você possui {{getTarefasPendentes().length}} tarefas pendentes
    </p>
  </header>
</div>
<form @submit.prevent="cadastraTarefa">
  <div class="row">
    <div class="col">
      <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp=evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
    </div>
    <div class="col-md-2">
      <button type="submit" class="btn btn-primary">Cadastrar</button>
    </div>
    <div class="col-md-2">
      <select @change="evento => estado.filtro=evento.target" class="form-control">
        <option value="todas">Todas tarefas</option>
        <option value="pendentes">Pendentes</option>
        <option value="finalizadas">Finalizadas</option>
      </select>
    </div>
  </div>
</form>
<ul class="list-group mt-4">
  <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
    <input @changed="evento => tarefa.finalizada=evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.título" type="checkbox">
    <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.título">
      {{ tarefa.título }}
    </label>
  </li>
</ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
