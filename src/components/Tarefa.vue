<template>
  <div class="Tarefa">
    <input class="concluidoCheck" type="checkbox" v-model="concluido" @change="salvarTarefa"/>

    <div v-if="edit==false" class="titulo" v-bind:class="{ concluido: concluido }" @click="editar">{{titulo}}</div>

    <input class="tituloEdit" v-if="edit" type="text" v-model="tituloTask" placeholder="Digite um novo titulo para a tarefa"/>

    <div v-if="edit==false" class="delete" @click="excluirTarefa">excluir</div>

    <div v-if="edit" class="salvar" @click="salvarTarefa">salvar</div>

  </div>
</template>

<script>
export default {
  name: 'Tarefa',
  props: {
      id: Number,
      titulo: String,
      status: Boolean
  },
  data() {
    return {
        concluido: false,
        tituloTask: '',
        edit: false
    }
  },
  mounted(){
      this.concluido = this.status;
      this.tituloTask = this.titulo;
  },
  methods: {
      excluirTarefa: async function(){
          var vm = this;
          var id = this.id;

          await this.axios.delete("http://localhost:8080/todotask/task/"+id)
            .then(function(data){
                vm.$emit("tasked");
            });

      },
      salvarTarefa: function(){
          var id = this.id;
          var vm = this;
          var titulo = this.tituloTask;
          var status = this.concluido;
          this.axios.put("http://localhost:8080/todotask/task/"+id,{titulo: titulo, status: status})
            .then(function(data){
                vm.edit = false;
                vm.$emit('tasked');
            });
      },
      editar: function(){
          this.edit = true;
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

    .Tarefa {
        width:500px;
        max-width:90%;
        border:1px solid #393d3f;
        margin:auto;
        text-align:left;
        text-transform:uppercase;
        padding-top:5px;
        padding-bottom:5px;
        border-radius:5px;
        margin-top:5px;
        color:#393d3f;
    }

    .concluidoCheck{
        display:inline-block;
        width:10%;
    }
    .concluidoCheck:hover{
        cursor:pointer;
    }
    .titulo {
        width:75%;
        display:inline-block;
        text-align:center;
    }

    .tituloEdit {
        width:70%;
        display:inline-block;
        text-align:center;
        border:none;
        text-transform:uppercase;
        box-shadow:0px 0px 10px 0px #393d3f;
        border-radius:5px;
        margin-right:5px;
    }
    
    .delete {
        display:inline-block;
        width:10%;
        text-align:center;
        font-size:12.5px;
        color:#F56C6C;
    }

    .delete:hover{
        cursor:pointer;
        color:#393d3f;
    }

    .salvar {
        display:inline-block;
        width:10%;
        text-align:center;
        font-size:12.5px;
        color:#67C23A;
    }

    .salvar:hover{
        cursor:pointer;
        color:#393d3f;
    }

    .concluido {
        color:rgba(57, 61, 63, 0.5);
        text-decoration: line-through;
    }

</style>
