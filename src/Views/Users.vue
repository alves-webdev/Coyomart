<template>
  <div class="container">
    <input
      class="searchbox"
      type="text"
      v-model="searchTerm"
      placeholder="Pesquisar usuários"
      @input="searchUsers"
    />
      <router-link to="/UserRegistration" class="addBtn">Adicionar usuários</router-link>
    <div class="table-wrapper">
      <table>
        <thead>
          <tr>
            <th class="text-left">Picture</th>
            <th class="text-left">Name</th>
            <th class="text-left">Address</th>
            <th class="text-left">User since</th>
            <th class="text-left">Email</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in filteredUsers" :key="user.id">
            <td>
              <img :src="user.picture" alt="Foto" width="50" />
            </td>
            <td>{{ user.name }}</td>
            <td>{{ user.address }}</td>
            <td>{{ user.created_at }}</td>
            <td>{{ user.email }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>

.container {
  position: relative;
  border-radius: 20px;
  width: 60em;
  height: 30em;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
  display: flex;
  flex-direction: column;
  background-color: rgb(236, 233, 233);
  text-align: center;
  justify-content: center;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  padding-top: 13%;
  margin-left: 20%;
  overflow-y: auto
}
.addBtn {
  position: absolute;
  top: 0;
  left: 0;
  width: 9em;
  height: 1.5em;
  padding: 0.6em;
  color: #000;
  z-index: 10;
  padding-left: 1em;
  background-color: #fff;
  border: 1px solid #929292;
  border-radius: 10px;
  text-decoration: none;
  text-align: center;
  font-size: 1em;
  transition: all 0.2s ease-in-out;
  margin-left: 1em;
  margin-top: 0.5em;
}

.addBtn:hover {
  background-color: #929292;
  color: #fff;
  transition: all 0.2s ease-in-out;
  transform: scale(1.1);
}

.searchbox {
  position: absolute;
  top: 0;
  right: 0;
  width: 20em;
  height: 2em;
  border: 1px solid #ccc;
  border-radius: 4px;
  background-color: #fff;
  padding: 0.6em;
  color: #000;
  z-index: 10;
  padding-left: 1em;
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

.table-wrapper {
  position: relative;
  height: 55em;
  margin-top: -4em;
  overflow-y: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
  position: sticky;
  top: 0;
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
  position: sticky; /* add this style */
  top: 0; /* add this style */
  color: rgb(0, 0, 0);
}
td {
  text-align: left;
  background-color: #fff;
  color: rgb(0, 0, 0);
}

</style>
<script>
import axios from 'axios'

export default {
  data() {
    return {
      users: [],
      searchTerm: ''
    }
  },
  computed: {
    filteredUsers() {
      return this.users.filter(user => user.name.toLowerCase().includes(this.searchTerm.toLowerCase()))
    }
  },
  mounted() {
    axios.get('http://54.86.195.171:3000//api/v1/users')
      .then(response => {
        this.users = response.data
      })
  },
  methods: {
    searchUsers() {
      // the filteredUsers computed property will automatically update based on the searchTerm
    }
  }
}
</script>