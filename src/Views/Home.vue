<template>
  <div class="container">
    <div class="box upper-box">
      <h1>PRODUTOS CADASTADOS</h1>
      <div class="dados">
        <img
          src="../assets/boxes.svg"
          contain
          height="100"
        />
        <h1
        style="font-size: 4em"
        >20</h1>
      </div>
    </div>
    <div class="box upper-box">
      <h1>NÚMERO DE CLIENTES</h1>
      <div class="dados">
        <img
          src="../assets/users.svg"
          class="my-3"
          contain
          height="100"
        />
        <h1
        style="font-size: 4em"
        >20</h1>
      </div>
    </div>
  </div>
    <div class="box lower-box">
      <div
      class="table-responsive"
      >
      <table>
        <thead>
          <tr>
            <th class="text-left">Image</th>
            <th class="text-left">Name</th>
            <th class="text-left">Category</th>
            <th class="text-left">UN</th>
            <th class="text-left">Stocked</th>
            <th class="text-left">Value</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="product in filteredProducts" :key="product.id">
            <td>
              <img :src="product.image" alt="Product image" width="50" />
            </td>
            <td>{{ product.name }}</td>
            <td>{{ product.category }}</td>
            <td>{{ product.unit }}</td>
            <td>{{ product.stocked }}</td>
            <td>{{ product.value }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    </div>
</template>

<style scoped>
.table-responsive {
  overflow-x: auto;
  overflow-y: auto;
  height: 100%;
  width: 100%;
}
.container {
  padding-left: 20%;
  display: flex;
  flex-direction: row;
  gap: 19px;
  align-items: center;
  justify-content: space-between;
  height: 100%;
}

.dados {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  gap: 10px;
  width: 100%;
  height: 10vh;
}
.dados img {
  width: 10vh;
  height: 10vh;
}

.box {
  width: 50vh;
  height: 25vh;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
  display: flex;
  flex-direction: column;
  gap: 0px;
  background-color: rgb(236, 233, 233);
  text-align: center;
  justify-content: center;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.box h1{
  font-size: 1.5em;
  color: #000;
  margin-top: 20px;
}

.box img {
  width: 15vh;
  height: 10vh;
}


.upper-box {
  margin-bottom: 10px;
  flex-direction: column;
  width: 33vw;
}

table {
  width: 100%;
  border-collapse: collapse;
  justify-content: center;
  align-items: center;
}

td,
th {
  border: 1px solid #ddd;
  padding: 0.4em;
  justify-content: center;
  align-items: center;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}

tr:hover {
  background-color: #ddd;
}

th {
  text-align: left;
  background-color: #929292;
  position: sticky;
  color: rgb(0, 0, 0);
}
td {
  text-align: left;
  background-color: #fff;
  color: rgb(0, 0, 0);
}


.lower-box {
  margin-left: 20%;
  width: 60vw;
  height: 42vh;
  overflow-y: auto
}
</style>
<script>
import axios from 'axios'

export default {
  data() {
    return {
      products: []
    }
  },
  computed: {
    filteredProducts() {
      return this.products.filter(product => product.featured)
    }
  },
  mounted() {
    axios.get('http://54.86.195.171:3000//api/v1/products')
      .then(response => {
        this.products = response.data
      })
  }
}
</script>