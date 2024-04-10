<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas" :key="tarefa">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizada }" :for="tarefa.titulo" class="ms-3">{{ tarefa.titulo }}</label>
        </li>
    </ul>
</template>

<script setup>
const props = defineProps(['tarefas'])
</script>

<style>
.done{
  text-decoration: line-through;
}</style>