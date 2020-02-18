<template>
  <div>
    <titulo :texto="`Aluno: ${aluno.nome}`" />
    <button>Editar</button>
    <table>
      <tbody>
        <tr>
          <td class="colPequeno">Matrícula:</td>
          <td>
            <label>{{ aluno.id }}</label>
          </td>
        </tr>
        <tr>
          <td>Nome:</td>
          <td>
            <label>{{ aluno.nome }}</label>
            <input v-model="aluno.nome" type="text" />
          </td>
        </tr>
        <tr>
          <td>Sobrenome:</td>
          <td>
            <label>{{ aluno.sobrenome }}</label>
            <input v-model="aluno.sobrenome" type="text" />
          </td>
        </tr>
        <tr>
          <td>Data Nascimento:</td>
          <td>
            <label>{{ aluno.dataNasc }}</label>
            <input v-model="aluno.dataNasc" type="text" />
          </td>
        </tr>
        <tr>
          <td>Professor:</td>
          <td>
            <label>{{ aluno.professor.nome }}</label>
            <select v-model="aluno.professor">
                <option v-for="(professor, index) in professores" 
                :key="index" v-bind:value="professor">
                    {{ professor.nome }}
                </option>
            </select>
          </td>
        </tr>
      </tbody>
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
      professores: [],
      aluno: {},
      idAluno: this.$route.params.id
    };
  },
  created() {
    this.$http
      .get("http://localhost:3000/alunos/" + this.idAluno)
      .then(res => res.json())
      .then(aluno => (this.aluno = aluno));

    this.$http
      .get("http://localhost:3000/professores")
      .then(res => res.json())
      .then(professores => this.professores = professores);
  },
  methods: {}
};
</script>

<style scoped></style>
