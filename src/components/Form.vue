<template>
    <div class="container">
        <h1 class="submitted-tittle">Fale sobre você:</h1>
      <form @submit.prevent="submit" class="form">
        <div class="form-group">
            <label class="label" for="nome">Nome Completo:</label>
            <input class="input-field" type="text" id="nome" v-model="dados.nome" required>
        </div>
    
        <div class="form-group">
            <label class="label" for="email">Endereço de E-mail:</label>
            <input class="input-field" type="email" id="email" v-model="dados.email" required>
        </div>
    
        <div class="form-group">
            <label class="label" for="idade">Idade:</label>
            <input class="input-field" type="number" id="idade" v-model.number="dados.idade" required>
        </div>
    
        <div class="form-group">
            <label class="label" for="descricao">Breve Descrição:</label>
            <textarea class="input-field" id="descricao" v-model="dados.descricao"></textarea>
        </div>
    
        <button type="submit" class="submit-btn">Enviar</button>
    </form>

    <div class="data" v-if="mostrarDados">
        <h2 class="title">Dados Enviados:</h2>
        <ul class="list" v-for="(item, index) in listarDados" :key="index">
            <li><strong>Nome:</strong> {{ item.nome }}</li>
            <li><strong>Email:</strong> {{ item.email }}</li> 
            <li><strong>Idade:</strong> {{ item.idade }}</li>
            <li><strong>Descrição:</strong> {{ item.descricao }}</li>
        </ul>
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

  <style>
  body{
    background-color: #fff;

  }
    h3 {
    margin: 40px 0 0;
    }
    ul {
    list-style-type: none;
    padding: 0;
    }
    li {
    margin: 0 10px;
    text-align: justify;
    }
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
  
  .form {
    width: 70%;
    margin-bottom: 20px;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  .label {
    display: block;
    font-weight: bold;
  }
  
  .input-field {
    width: 30%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 25px;
    transition: all 0.3s;
}

.input-field:hover {
    border: 1px solid #19745f;
    border-radius: 25px;
    transition: all 0.3s;
    box-shadow: 15px 10px 24px -15px black;
}
  
  .submit-btn {
    padding: 10px 20px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    transition: all 0.3s;
    cursor: pointer;
  }

  .submit-btn:hover {
    border: 1px solid #0a5cb4;
    transform: scale(1,1);
    transition: all 0.3s;
    box-shadow: 15px 10px 24px -15px black;
}
  
  .title {
    font-size: 24px;
    margin-bottom: 15px;
  }
  
  .list {
    list-style: none;
    padding: 0;
  }
  
  .submitted-item {
    margin-bottom: 10px;
  }
  
  </style>  