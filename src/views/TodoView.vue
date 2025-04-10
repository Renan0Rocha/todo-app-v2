<template>
<div>
    <h1 class="text-3x1">Lista de Tarefas</h1>
    <button v-if="abrirForm" @click="abrirForm = true">Nova Tarefa</button>
    <div v-if="abrirForm">
      <form>
        <input type="text" v-model="descricao" placeholder="Digite a tarefa" />
        <button @click="adicionar">Adicionar</button>
      </form>
    </div>
    <table class="table">
      <thead>
        <tr>
          <th>#</th>
          <th>ID</th>
          <th>Descrição</th>
          <th>Feito?</th>
          <th>Ação</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in tarefas" :key="index">
          <td>{{ index }}</td>
          <td>{{ item.id }}</td>
          <td>{{ item.descricao }}</td>
          <td>{{ item.feito ? "Sim" : "Não" }}</td>
          <td>
            <button @click="item.feito = !item.feito">
              {{ item.feito ? "Desfazer" : "Finalizar" }}
            </button>
          </td>
        </tr>
      </tbody>
    </table>
</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {},
  data() {
    return {
      tarefas: [
        { id: 1, descricao: "Comprar leite", feito: false },
        { id: 2, descricao: "Estudar Vue.js", feito: false },
        { id: 3, descricao: "Fazer exercícios", feito: false }
      ],
      descricao: null,
      abrirForm: false,
    };
  },
  methods: {
    adicionar() {
      if (this.descricao != null)
      {
        const id = this.tarefas.length + 1;
        const novaTarefa = {
          id: id,
          descricao: this.descricao,
          feito: false
        };
        this.tarefas.push(novaTarefa);
        this.descricao = null;
        this.abrirForm = false;
      }
    },
    finalizar(id: number) {
      const tarefa = this.tarefas.find(t => t.id === id);
      if (tarefa) {
        tarefa.feito = !tarefa.feito;
      }
    },
    remover(id: number) {
      const novaLista = this.tarefas.filter(t => t.id !== id);
      this.tarefas = novaLista;
    }
  }
});
</script>

<style scoped>
.todo-view {
  font-family: Arial, sans-serif;
  padding: 20px;
}

h1 {
  color: #333;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  background: #f4f4f4;
  margin: 5px 0;
  padding: 10px;
  border-radius: 5px;
}
</style>
