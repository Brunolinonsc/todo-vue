<script setup>
  import { reactive } from "vue";
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaTarefa from './components/ListaTarefas.vue';


const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas:[
    {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
      titulo: 'Ir para a academia',
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
    titulo: estado.tarefaTemp,
    finalizadas: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}
</script>

<template>
  <div class="constainer">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Frmulario :tarefa-temp = "estado.tarefaTemp" :edita-tarefa-temp=" evento => estado.tarefaTemp= evento.target.value" :cadastra-tarefa = "cadastraTarefa" />
    <!-- <ListaTarefa /> -->
  </div>
  
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>
