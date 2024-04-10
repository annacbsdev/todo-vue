<script setup>
import { reactive } from "vue";
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'

const estado = reactive({
  filtro: "Todas" ,
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false
    },
    {
      titulo: 'Cozinhar',
      finalizada: false
    },
    {
      titulo: 'Lavar a louça',
      finalizada: true
    }, 
  ],
  tarefaNova: ''
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
  
}

const getTarefasFiltradas = () => {
  const { filtro } = estado

  switch(filtro){
    case 'pendentes':
      return getTarefasPendentes()
    case 'finalizadas':
      return getTarefasFinalizadas()
    default:
      return estado.tarefas
  }
}

const cadastraTarefa = ()=>{
  const tarefaNova = {
    titulo: estado.tarefaNova,
    finalizada: false
  }
  estado.tarefas.push(tarefaNova)
  estado.tarefaNova = ''
}


</script>

<template>
  <div class="container">

    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :tarefa-nova="estado.tarefaNova" :edita-tarefa-nova="evento => estado.tarefaNova = evento.target.value" :cadastra-tarefa="cadastraTarefa" 
    :trocar-filtro="evento=> estado.filtro = evento.target.value"  />
    <ListaDeTarefas :tarefas="getTarefasFiltradas( )"/>

  </div>

</template>

<style scoped>



</style>
