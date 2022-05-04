<template>
  <div>
    <form id="burger-form">
      <div class="input-container">
        <label for="name">Nome do Cliente</label>
        <input
          type="text"
          name="name"
          id="name"
          v-model="name"
          placeholder="Digite o seu Nome"
        />
      </div>
      <div class="input-container">
        <label for="bread">Escolha o seu Pão</label>
        <select name="bread" id="bread" v-model="bread">
          <option value="">Selecione o tipo do Pão</option>
          <option
            v-for="bread in breadData"
            :key="bread.id"
            :value="bread.tipo"
          >
            {{ bread.tipo }}
          </option>
        </select>
      </div>
      <div class="input-container">
        <label for="meat">Escolha a carne do seu Burger</label>
        <select name="meat" id="meat" v-model="meat">
          <option value="">Selecione o tipo de carne</option>
          <option v-for="meat in meatData" :key="meat.id" :value="meat.tipo">
            {{ meat.tipo }}
          </option>
        </select>
      </div>
      <div id="optional-container" class="input-container">
        <label id="optional-title" for="optionals"
          >Selecione os Opcionais</label
        >
        <div
          v-for="optional in optionalData"
          :key="optional.id"
          class="checkbox-container"
        >
          <input
            type="checkbox"
            name="optionals"
            v-model="optionals"
            :value="optional.tipo"
          />
          <span>{{ optional.tipo }}</span>
        </div>
      </div>
      <div class="input-container">
        <input type="submit" class="submit-btn" value="Criar meu Burger!" />
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "BurgerForm",
  data() {
    return {
      breadData: null,
      meatData: null,
      optionalData: null,
      name: null,
      bread: null,
      meat: null,
      optionals: [],
      status: "Solicitado",
      msg: null,
    };
  },
  methods: {
    async getIngredients() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.breadData = data.paes;
      this.meatData = data.carnes;
      this.optionalData = data.opcionais;
    },
  },
  mounted() {
    this.getIngredients();
  },
};
</script>

<style scoped>
#burger-form {
  margin: 0 auto;
  max-width: 400px;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  border-left: 4px solid #fcba03;
  color: #222;
  font-weight: bold;
  margin-bottom: 15px;
  padding: 5px 10px;
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}

#optional-container {
  flex-direction: row;
  flex-wrap: wrap;
}

#optional-title {
  width: 100%;
}

.checkbox-container {
  align-items: flex-start;
  display: flex;
  margin-bottom: 20px;
  width: 50%;
}

.checkbox-container span,
.checkbox-container input {
  width: auto;
}

.checkbox-container span {
  font-weight: bold;
  margin-left: 6px;
}

.submit-btn {
  background-color: #222;
  border: 2px solid #222;
  color: #fcba03;
  cursor: pointer;
  font-size: 16px;
  font-weight: bold;
  margin: 0 auto;
  padding: 10px;
  transition: 0.5s;
}

.submit-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
