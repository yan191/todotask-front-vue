<template>
  <div class="NovaTarefa">
  
    <div class="mensagem" v-if="mensagem.length>0">
    {{mensagem}} <span @click="limparMensagem">limpar</span>
    </div>

    <input v-model="titulo" type="text" placeholder="Digite uma tarefa"/>

    <div class="NovaTarefaBtn" @click="addTask">add</div>
    
  </div>
</template>

<script>
export default {
  name: 'NovaTarefa',
  props: {
    msg: String
  },
  data() {
    return {
      titulo: '',
      mensagem: ''
    }
  },
  mounted(){
    
  },
  methods: {
    addTask:async function(){
      var tarefa = this.titulo;
      var vm = this;

      if(tarefa.length>0){

        await this.axios.post("http://localhost:8080/todotask/task",{titulo: tarefa, status: false})
        .then(function(data){

          if(data.status==200){
            vm.titulo = "";
            vm.mensagem = "Tarefa criada com sucesso! ";

            vm.$emit("tasked");
          }

        });

      }else{
        this.mensagem = "Digite uma tarefa para poder criar";
      }
    },
    limparMensagem: function(){
      this.mensagem = "";
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .NovaTarefa {
    width:500px;
    max-width:90em;
    margin:auto;
    margin-top:10px;
  }

  .NovaTarefa input {
    width:80%;
    display:inline;
    border:none;
    text-transform:uppercase;
    box-shadow:0px 0px 10px 0px #393d3f;
    padding:5px;
    border-top-left-radius:7.5px;
    border-bottom-left-radius:7.5px;
    text-align:center;
  }

  .NovaTarefaBtn{
    width:10%;
    display:inline;
    text-transform:uppercase;
    background-color:#393d3f;
    color:#fdfdff;
    padding:5px;
    border-top-right-radius:7.5px;
    border-bottom-right-radius:7.5px;
  }

  .NovaTarefaBtn:hover{
    cursor:pointer;
    color:#62929e;
  }

  .mensagem {
    color:#E6A23C;
    margin-bottom:5px;
  }
  .mensagem span{
    color:#62929e;
    margin-left:10px;
  }
  .mensagem span:hover{
    cursor:pointer;
  }
</style>
