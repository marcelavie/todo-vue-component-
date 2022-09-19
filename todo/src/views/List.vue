<template>
  <div class='container mt-2'>
    <b-card-text>descrição</b-card-text>
    <div v-for="(task, index) in tasks" :key="index">
    <b-card :title="task.subject" class="'mb-2'">
      <b-card-text>{{ task.description }}</b-card-text>
    
      <b-button variant="outline-secondary" class="mr-2" @click="edit(index)">Editar</b-button>
      <b-button variant="outline-danger" class="mr-2" @click="remove(task, index)" >Excluir</b-button>
    </b-card>
  </div> 

  <b-modal ref="modalRemove" hide title="Excluir Tarefa">
  <div class="d-block text-center">Você tem certeza que quer excluir essa tarefa? {{ taskSelected.subject }}</div>
  <div class="mt-3 d-flex justify-content-center-end">
    <b-button variant="outline-secondary" class="mr-2" @click="hideModal">Cancelar</b-button>
    <b-button variant="outline-danger" class="mr-2" @click="confirmRemoveTask" >Excluir</b-button>

  </div>
</b-modal>
</div>

</template>

<script>
export default {
  name: 'List',

  data() {
    return {
      tasks: []
      }
  },
  
  created() {
      this.tasks = (localStorage.getItem('tasks')) ? JSON.parse(localStorage.getItem('tasks')) : [];
  },

  methods: {
    edit(index) {
      this.$router.push({ name: 'form', params: { index } });
    },
    remove(tasks, index) {
      this.taskSelected = tasks;
      this.taskSelected.index = index;
      this.$refs.modalRemove.show();

    },

    hideModal() {
      this.$refs.modalRemove.hide();
    },
    confirmRemoveTask() {

    }
  }



}


</script>

