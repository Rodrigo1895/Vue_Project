<template>
  <div>
    <titulo texto="Professores"></titulo>

    <table>
      <thead>
        <th>Cód.</th>
        <th>Nome</th>
        <th>Alunos</th>
      </thead>
      <tbody v-if="professores.length">
        <tr v-for="(professor, index) in professores" :key="index">
          <td>{{ professor.id }}</td>          
          <router-link to="/alunos" tag="td" style="cursor: pointer">
            {{ professor.nome }} {{ professor.sobrenome }}
          </router-link>          
          <td>
            3
          </td>
        </tr>
      </tbody>
      <tfoot v-else>
        Nenhum professor encontrado
      </tfoot>
    </table>
  </div>
</template>

<script>
import Titulo from "../_shared/Titulo";

export default {
  components: {
    Titulo
  },
  data() {
    return {
      professores: []
    };
  },
   created() {
    this.$http
      .get("http://localhost:3000/professores")
      .then(res => res.json())
      .then(professores => (this.professores = professores));
  },
  props: {},
};
</script>

<style scoped></style>
