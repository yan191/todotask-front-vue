<template>
  <div class="TodasTarefas">
    <tarefa @tasked="reload" v-for="tarefa in tarefas" :id="tarefa.id" :titulo="tarefa.titulo" :status="tarefa.status" />
  </div>
</template>

<script>
import Tarefa from '@/components/Tarefa.vue'

export default {
  name: 'TodasTarefas',
  components: {
    Tarefa
  },
  props: {
  },
  data() {
    return {
      tarefas: [],
    }
  },
  mounted(){
    var vm = this;
    this.axios.get("http://localhost:8080/todotask/task")
      .then(function(data){
        vm.tarefas = data.data;
      });
  },
  methods: {
    reload: function(){
      this.$emit("tasked");
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .TodasTarefas {
    margin-top:20px;
  }
</style>
