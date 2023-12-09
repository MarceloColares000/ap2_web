<template>
  <div class="container">
      <div class="row justify-content-center">
          <div class="col-xl-6 col-lg-12 col-md-9">
              <div class="card o-hidden border-0 shadow-lg my-5" data-aos="fade-up">
                  <div class="card-body p-0">
                      <div class="row">
                          <div class="col-lg-12">
                              <div class="p-5">
                                  <div class="text-center">
                                      <h1 class="h4 text-gray-900 mb-4">Olá! Que bom te ver aqui!</h1>
                                      <p>Fale um pouco sobre você.</p>
                                  </div>
                                  <form @submit.prevent="submit" class="user">
                                      <div class="form-group">
                                          <label class="text-base label-color" for="name">Nome:</label>
                                          <input type="text" class="form-control" :class="{'is-invalid': dados.nome === ''}" id="nome" v-model="dados.nome" required>
                                          <div class="invalid-feedback">Por favor, preencha seu nome.</div>
                                      </div>
                                      <div class="form-group">
                                          <label class="text-base label-color" for="email">Email:</label>
                                          <input type="email" class="form-control" :class="{'is-invalid': dados.email === ''}" id="email" v-model="dados.email" required>
                                          <div class="invalid-feedback">Por favor, insira um email válido.</div>
                                      </div>
                                      <div class="form-group">
                                          <label class="text-base label-color" for="idade">Idade:</label>
                                          <input type="number" class="form-control" :class="{'is-invalid': dados.idade < 0}" id="idade" v-model.number="dados.idade" required>
                                          <div class="invalid-feedback">Por favor, insira uma idade válida.</div>
                                      </div>
                                      <div class="form-group">
                                          <label class="text-base label-color" for="descricao">Descrição:</label>
                                          <textarea class="form-control" :class="{'is-invalid': dados.descricao === ''}" id="descricao" v-model="dados.descricao" required></textarea>
                                          <div class="invalid-feedback">Por favor, forneça uma breve descrição.</div>
                                      </div>
                                      <div class="form-group row">
                                        <button type="submit" class="btn btn-lg btn-block btn-primary mt-4 text-center">Cadastrar</button>
                                        <button type="reset" class="btn btn-lg btn-block btn-danger mt-4 text-center">Cancelar</button>
                                      </div>
                                  </form>
                                  <div class="data mt-4" v-if="mostrarDados">
                                      <h2 class="title">Dados Enviados:</h2>
                                      <ul class="list" v-for="(item, index) in listarDados" :key="index">
                                          <li><strong>Nome:</strong> {{ item.nome }}</li>
                                          <li><strong>Email:</strong> {{ item.email }}</li>
                                          <li><strong>Idade:</strong> {{ item.idade }}</li>
                                          <li><strong>Descrição:</strong> {{ item.descricao }}</li>
                                      </ul>
                                  </div>
                              </div>
                          </div>
                      </div>
                  </div>
              </div>
          </div>
      </div>
  </div>
</template>

  
<script>
    export default {
      data() {
        return {
          dados: {
            nome: '',
            email: '',
            idade: null,
            descricao: ''
          },
          mostrarDados: false,
          listarDados: [] 
        };
      },
      methods: {
        submit() {
          if (this.validarCampos()) {
            this.mostrarDados = true;
            this.adicionarLista();
            this.resetForm();
          } else {
            alert('Por favor, preencha todos os campos corretamente.');
          }
        },
        resetForm() {
          this.dados = {
            nome: '',
            email: '',
            idade: null,
            descricao: ''
          };
        },
        adicionarLista() {
          this.listarDados.push({
              nome: this.dados.nome,
              email: this.dados.email,
              idade: this.dados.idade,
              descricao: this.dados.descricao
          });
        },
        validarCampos() {
          return (
            this.dados.nome !== '' &&
            this.validarEmail(this.dados.email) &&
            this.dados.idade !== null &&
            this.dados.idade > 0 &&
            this.dados.descricao !== ''
          );
        },
        validarEmail(email) {
          const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
          return re.test(String(email).toLowerCase());
        }
      }
    };
</script>