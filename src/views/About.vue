<template>
  <div class="about">
    <form>
    <label for="">Nome</label> <br>
    <input
      type="text"
      placeholder="Insira  nome"
      v-model="name"> <br><br><br>

    <label for="">E-mail</label> <br>
    <input
      type="email"
     placeholder="Insira seu e-mail"
      v-model="email"> <br><br><br>

    <label for="">Insira seu CEP</label> <br>
    <input
      type="text"
      placeholder="Insira seu Cep"
      v-model="cep"> <br><br><br>

     <textarea column="3"
      v-model="message"
      placeholder="Insira sua mensagem marota....">
     </textarea>

     <button
      type="submit"
      @click.prevent="sendData()">
      Enviar
      </button>
     </form>

    <div>
      <ul>
        <li>
            Name: {{dados.name}} | E-mail {{dados.email}}
            Endereço: {{dados.logradouro }} - {{dados.localidade}}
            Bairro: {{dados.bairro}}
            Cidade: {{dados.localidade}} - {{dados.uf}}
            CEP: {{dados.cep}}
        </li>
      </ul>
    </div>
  <hr>
  <input type="text" v-model="james"> <br>
  <input type="text" :value="samsung"> <br>
  <br> <br>
  {{ james }} <br><br>
  {{ samsung }}

  <div>
    <div v-for="filme in movies" :key="filme.id">
      <img :src="filme.Poster" alt="">
      <h1> {{filme.Title}} </h1>
      <h3> {{filme.Year}} </h3>
    </div>
  </div>

  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  data() {
    return {
      name: '',
      email: '',
      cep: '',
      message: '',
      endereco: {},
      dados: {},
      samsung: 'apple',
      james: 'jack sparrow',
      movies: [],
    };
  },
  watch: {
    cep(value) { // consultando a minha propriedade data
      if (value.length === 8) {
        this.buscarCep(value);
      }
    },
  },
  created() {
    this.getMovies();
  },
  methods: {
    buscarCep(value) {
      const url = `http://viacep.com.br/ws/${value}/json/`;
      fetch(url)
        .then((response) => response.json())
        .then((response) => {
          console.log(response);
          this.endereco = response;
        });
    },
    getMovies() {
      const url = 'http://www.omdbapi.com/?s=Harry&page=10&apikey=94e07ba9';
      fetch(url)
        .then((response) => response.json())
        .then((response) => {
          console.log(response);
          this.movies = response.Search;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    sendData() {
      const data = {
        name: this.name,
        email: this.email,
        cep: this.endereco,
        message: this.message,
      };
      this.dados = data;
    },
  },
};
</script>
