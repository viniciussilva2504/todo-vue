<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    { título: 'Estudar ES6', finalizada: false },
    { título: 'Estudar SASS', finalizada: false },
    { título: 'Ir para a academia', finalizada: true }
  ]
});

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada);
};

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada);
};

const getTarefasFiltradas = () => {
  switch (estado.filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
};

const cadastraTarefa = () => {
  if (estado.tarefaTemp.trim()) {
    estado.tarefas.push({
      título: estado.tarefaTemp.trim(),
      finalizada: false
    });
    estado.tarefaTemp = '';
  }
};
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario 
      :tarefa-temp="estado.tarefaTemp"
      :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value"
      :cadastra-tarefa="cadastraTarefa"
      :trocar-filtro="evento => estado.filtro = evento.target.value"
    />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div>
</template>
