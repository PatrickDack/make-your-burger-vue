<template>
  <div id="burger-table">
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Pão:</div>
        <div>Carne:</div>
        <div>Opcionais:</div>
        <div>Ações:</div>
      </div>
    </div>
    <div id="burger-table-rows">
      <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
        <div class="order-number">{{ burger.id }}</div>
        <div>{{ burger.nome }}</div>
        <div>{{ burger.pao }}</div>
        <div>{{ burger.carne }}</div>
        <div>
          <ul>
            <li v-for="(optional, index) in burger.opcionais" :key="index">
              {{ optional }}
            </li>
          </ul>
        </div>
        <div>
          <select name="status" class="status">
            <option
              v-for="stat in status"
              :key="stat.id"
              value="stat.tipo"
              :selected="stat.tipo === burger.status"
            >
              {{ stat.tipo }}
            </option>
          </select>
          <button class="delete-btn" @click="deleteOrder(burger.id)">
            Cancelar
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DashBoard",
  data() {
    return {
      BASE_URL: "http://localhost:3000",
      burgers: null,
      burguerId: null,
      status: [],
    };
  },
  methods: {
    async getOrders() {
      const req = await fetch(`${this.BASE_URL}/burgers`);
      const data = await req.json();
      this.burgers = data;
    },
    async getStatus() {
      const req = await fetch(`${this.BASE_URL}/status`);
      const data = await req.json();

      this.status = data;

      return data;
    },
    async deleteOrder(id) {
      const req = await fetch(`${this.BASE_URL}/burgers/${id}`, {
        method: "DELETE",
      });

      const res = await req.json();

      this.getOrders();
    },
  },
  mounted() {
    this.getOrders();
    this.getStatus();
  },
};
</script>

<style scoped>
#burguer-table {
  margin: 0 auto;
  max-width: 1200px;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
}

#burger-table-heading {
  border-bottom: 3px solid #333;
  font-weight: bold;
  padding: 12px;
}

#burger-table-heading div,
.burger-table-row div {
  width: 19%;
}

.burger-table-row {
  border-bottom: 1px solid #ccc;
  padding: 12px;
  width: 100%;
}

#burger-table-heading .order-id,
.burger-table-row .order-number {
  width: 5%;
}

select {
  margin-right: 12px;
  padding: 12px 6px;
}

.delete-btn {
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

.delete-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
