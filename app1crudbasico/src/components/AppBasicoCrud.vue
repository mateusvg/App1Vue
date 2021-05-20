<template>
  <div class="container mt-2">
    <div class="card">
      <div class="card-header ">
        <h3>Crud Básico</h3>
        <div id="hora">Hora:{{ time }}</div>
      </div>

      <!--Criar um METODO handleSubmitForm-->
      <!--tudo que está neste contexto de form,
            deve passar por este METODO()handleSubmitForm sempre na ação de submeter um botão-->
      <form v-on:submit.prevent="handleSubmitForm()">
        <div class="formularioEmpregado">
          <!--Inicio Bloco NOME-->
          <div class="form-group p-3">
            <label class="font-weight-bold">Nome: </label>
            <input
              type="text"
              class="form-control"
              id="nome"
              placeholder="Nome"
              v-model="nome"
            />
          </div>
          <!--FIM Bloco NOME-->

          <!--Inicio Bloco COMENTARIO-->
          <div class="form-group p-3">
            <label class="font-weight-bold">Comentário: </label>
            <textarea
              class="form-control"
              cols="40"
              rows="5"
              placeholder="Comentários..."
              v-model="msm"
            >
            </textarea>
          </div>
          <!--FIM Bloco  COMENTARIO-->

          <!--BOTÃO ENVIAR-->
          <div class="d-flex justify-content-left">
            <button class="btn btn-success" v-on:click="adicionarComentario">
              + Cadastrar
            </button>
            <!--Criar um metodo On click e trabalhar a logica dentro de SCRIPT-->
          </div>
          <!--BOTÃO ENVIAR-->

          <!--BLOCO LISTAR-->
          <div>
            <div class="list-group">
              <!--ArrayIteracao e uma variável que recebe o valor do array de cada iteração-->
              <!--adiciona o index pois deve saber qual é a posição da iteração do array para excluir-->
              <div
                class="list-group-item"
                v-for="(ArrayIteracao, index) in comentarios"
                v-bind:key="ArrayIteracao"
              >
                <span class="coment_autor"
                  >Nome: {{ ArrayIteracao.nome }}
                  <p>Comentário:{{ ArrayIteracao.msm }}</p>
                  <p>Horário: {{ ArrayIteracao.tempo }}</p>
                </span>
                <div>
                  <!--Adiciona o index como parametros para saber a posição de iteração-->
                  <button
                    class="btn btn-danger"
                    v-on:click.prevent="removeComentarios(index)"
                  >
                    Excluir
                  </button>
                  <button
                    class="btn btn-primary"
                    v-on:click.prevent="atualizarComentarios(index)"
                  >
                    Atualizar
                  </button>
                </div>
              </div>
            </div>
          </div>
          <!--BLOCO LISTAR-->
        </div>
        <!--Tudo que está dentro da TAG FORM vai ser validado-->
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      comentarios: [],
      nome: "",
      msm: "",
      time: "",
    };
  },

  methods: {
    adicionarComentario() {
      alert("Adicionado"),
        this.comentarios.push({
          nome: this.nome,
          msm: this.msm,
          //para adicionar um horario fixo no momento do comentário
          tempo: this.time,
        });

      // adiciona o limpar no nome e no comentario apos enviar.
      (this.nome = ""), (this.msm = "");
    },

    removeComentarios(index) {
      alert("Removido comentário nº: " + index);
      // o 1 significa quantos array quero remover depois do meu array
      this.comentarios.splice(index, 1);
    },

    atualizarComentarios(index) {
      this.comentarios.splice(index);
      this.comentarios.push({
        nome: this.nome,
        msm: this.msm,
        tempo: this.time
      });
      (this.nome = ""), (this.msm = "");
    },

    updateTime() {
      this.time =
        new Date().getHours() +
        ":" +
        new Date().getMinutes() +
        ":" +
        new Date().getSeconds();
    },
  },

  mounted() {
    setInterval(this.updateTime, 1000);
  },
};
</script>

<style></style>
