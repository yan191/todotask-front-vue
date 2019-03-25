<template>
  <div class="index">
    <h1>GSW</h1>
    <h2>A ToDo app to learn.</h2>

    <nova-tarefa @tasked="reload" />
    <todas-tarefas @tasked="reload" :key="todasTarefasKey" />

  </div>
</template>

<script>
// @ is an alias to /src
import NovaTarefa from '@/components/NovaTarefa.vue'
import TodasTarefas from '@/components/TodasTarefas.vue'

export default {
  name: 'index',
  components: {
    NovaTarefa,
    TodasTarefas
  },
  data() {
    return {
      todasTarefasKey: 0,
    }
  },
  methods: {
    reload: function(){
      this.todasTarefasKey +=1;
    }
  }
}
</script>
<style scoped>
 h1 {
   font-size:100px;
   line-height:50%;
   color:#393d3f;
 }
 h2 {
   color:#393d3f;
 }
</style>
