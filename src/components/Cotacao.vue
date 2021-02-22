<template>
  <div id="wrapper">
    <h1 id="descicao">{{ empresa }}</h1>
    <h1 id="numero">{{ cotacao }}</h1>
    <div class="buttons_bloxk">
      <button class="btn-pesquisa" v-on:click="buscar('PETR4')">
        Petrobras
      </button>
      <button class="btn-pesquisa" v-on:click="buscar('VALE3')">Vale</button>
      <button class="btn-pesquisa" v-on:click="buscar('ITUB4')">
        Itaú Unibanco
      </button>
    </div>

    <div>
      <label>Clique em uma das empresas acima ou pesquise pelo nome: </label>
      <div class="input_block">
        <input
          id="input"
          name="search"
          v-model="inputValue"
          @change="buscar($event)"
          type="text"
        />
        <div class="icon_block">
          <button class="button_search" v-on:click="buscar('')">
            <SearchIcon />
          </button>
        </div>
      </div>
    </div>

    <h5>Projeto desenvolvido por Herlmanoel Fernandes</h5>
  </div>
</template>

<script>
import { SearchIcon } from "vue-feather-icons";
const axios = require("axios").create({
  baseURL: "http://127.0.0.1:5000",
  timeout: 10000,
  headers: { "X-Custom-Header": "foobar" },
});

export default {
  name: "Cotacao",
  components: {
    SearchIcon,
  },
  data() {
    return {
      cotacao: 0,
      inputValue: "",
      empresa: "",
    };
  },
  methods: {
    buscar(emp) {
      let valor;
      if (emp) {
        valor = emp;
      } else {
        valor = this.inputValue;
      }

      async function postData() {
        try {
          const { data } = await axios.post("buscar", {
            empresa: valor,
          });
          const { preco, name } = data;
          console.log(data);
          return { preco, name };
        } catch (error) {
          console.error(error);
        }
      }
      postData().then((result) => {
        this.cotacao = result.preco;
        this.empresa = result.name;
        console.log("AQUI", result);
      });
    },
  },
  mounted() {
    async function getData() {
      try {
        const { data } = await axios.get("buscar");
        const { preco, name } = data;
        console.log(data);
        return { preco, name };
      } catch (error) {
        console.error(error);
      }
    }
    getData().then((result) => {
      this.cotacao = result.preco;
      this.empresa = result.name;
    });
  },
};
</script>

<style scoped>
label {
  font-size: 0.8rem;
  color: rgba(0, 0, 0, 0.6);
}
.buttons_bloxk {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
}
.btn-pesquisa {
  display: flex;
  height: 2.6rem;
  align-items: center;
  justify-content: center;
  padding: 0.5rem;
  background: rgba(0, 0, 0, 0.2);
  border-radius: 0.5rem;
  cursor: pointer;
}
#wrapper {
  width: 500px;
  height: 500px;
  background-color: #fff;
  border-radius: 10px;
  padding: 3rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  box-shadow: 0px 4px 25px 1px rgba(0, 0, 0, 0.2);
}
.input_block {
  display: flex;
  height: 2.6rem;
  align-items: center;
  justify-content: center;
  padding: 0;
  margin-top: 0.5rem;
}
.button_search {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  outline: none;
  background: none;
  cursor: pointer;
}
.icon_block:hover,
.btn-pesquisa:hover {
  background: rgba(0, 0, 0, 0.3);
}
.icon_block {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 4rem;
  height: 100%;
  border: 1px solid #e6e6f0;
  background-color: rgba(0, 0, 0, 0.2);
  border-radius: 0 0.5rem 0.5rem 0;
}
#input {
  width: 100%;
  height: 100%;
  border-radius: 0.5rem 0rem 0rem 0.5rem;
  background: #e6e6f0;
  border: 1px solid #e6e6f0;
  outline: 0;
  padding: 0 1.6rem;
}
#descicao {
  font-weight: 300;
}
</style>
