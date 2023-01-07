<template>
    <form class="form-container">

        <div class="item-container">
            <label for="name">Nome do produto:</label><br>
            <input v-model="name" v-bind:class="{ 'is-invalid': errors.name }" type="text" id="name"><br>
            <span v-if="errors.name" class="error">{{ errors.name[0] }}</span>
        </div>
        <div class="item-container">
            <label for="image">imagem:</label><br>
            <input v-model="image" v-bind:class="{ 'is-invalid': errors.image }" type="text" id="image"><br>
            <span v-if="errors.image" class="error">{{ errors.image[0] }}</span>
        </div>
        <div class="item-container">

            <label for="category">Categoria:</label><br>
            <input v-model="category" v-bind:class="{ 'is-invalid': errors.category }" type="text" id="category"><br>
            <span v-if="errors.category" class="error">{{ errors.category[0] }}</span>
        </div>
        <div class="item-container">

            <label for="unit">Unidade:</label><br>
            <input v-model="unit" v-bind:class="{ 'is-invalid': errors.unit }" type="text" id="unit"><br>
            <span v-if="errors.unit" class="error">{{ errors.unit[0] }}</span>
        </div>
        <div class="item-container">

            <label for="stocked">Em estoque:</label><br>
            <input v-model="stocked" v-bind:class="{ 'is-invalid': errors.stocked }" type="number" id="stocked"><br>
            <span v-if="errors.stocked" class="error">{{ errors.stocked[0] }}</span>
        </div>
        <div class="item-container">

            <label for="price">Preço:</label><br>
            <input v-model="price" v-bind:class="{ 'is-invalid': errors.price }" type="number" id="price"><br>
            <span v-if="errors.price" class="error">{{ errors.price[0] }}</span>
        </div>
        <div class="item-container">

            <label for="featured">Em destaque</label><br>
            <input v-model="featured" v-bind:class="{ 'is-invalid': errors.featured }" type="checkbox"
                id="featured"><br>
            <span v-if="errors.featured" class="error">{{ errors.featured[0] }}</span>
        </div>
        <div class="item-container">

            <label for="description">Descrição</label><br>
            <input v-model="description" v-bind:class="{ 'is-invalid': errors.description }" type="text"
                id="description" class="description"><br>
            <span v-if="errors.description" class="error">{{ errors.description[0] }}</span>
        </div>
        <div class="button-container">
            <button v-on:click.prevent="saveProduct">Salvar</button>
            <button v-on:click.prevent="cancel">Cancelar</button>
        </div>

    </form>


        
</template>


<style scoped>
.form-container {
    font-family: 'Roboto', sans-serif;
    display: grid;
    grid-template-columns: 0fr 1fr;
    justify-content: center;
    align-items: center;
    width: 50em;
    height: 36em;
    padding: 1em;
    padding-bottom: 10em;
    margin: 1em;
    margin-top: 5em;
    padding-left: 2em;
    margin-left: 20em;
    color: #182d4d;
    background-color: #ffffff;
    border: 2px solid #182d4d;
    border-radius: 10px;
    box-sizing: border-box;
}

.button-container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 6em;
    position: relative;
    bottom: 1em;
    left: 8rem;
    align-items: center;
}

.item-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 50%;
}

.img-container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
}


.imglink {
    display: flex;
    flex-direction: column;
    gap: 0em;
    width: 50%;
    padding-left: 3em;
}

.imgcheck {
    display: flex;
    flex-direction: column;
    gap: 0em;
    padding-right: 4em;
}


input {
    align-self: center;
    width: 100%;
    height: 1em;
    padding: 1.5em;
    margin-bottom: 0.5em;
    border: 2px solid #182d4d;
    border-radius: 4px;
    box-sizing: border-box;
}


.button-container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 6em;
    align-items: center;
}


button {
    background-color: #182d4d;
    border: 2px solid #ffffff;
    color: white;
    justify-content: center;
    padding: 2em 5em;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 0.8em;
    cursor: pointer;
    border-radius: 4px;
    transition: 0.5s ease-in-out;
}

button:hover {
    background-color: #ffffff;
    color: #182d4d;
    border: 2px solid #182d4d;
    transition: 0.5s ease-in-out;
    transform: scale(1.1);
}

button:nth-child(2) {
    background-color: #ffffff;
    color: #182d4d;
    border: 2px solid #182d4d;
}

button:nth-child(2):hover {
    background-color: #182d4d;
    color: #ffffff;
    border: 2px solid #ffffff;
    transition: 0.5s ease-in-out;
    transform: scale(1.15);
}

@media screen and (max-width: 800px) {
    .form-container {
        width: 100%;
        height: 100%;
        margin-left: 0%;
    }
}
</style>

<script>

import axios from 'axios'

export default {
  data() {
    return {
      name: '',
      image: '',
      description: '',
      category: '',
      unit: '',
      stocked: 0,
      price: 0,
      featured: false,
      errors: {},
      loading: false,
      products: []
    }
  },
  methods: {
    saveProduct() {
      this.loading = true;
      this.errors = {}
      // Validate input fields
      if (!this.name) {
        this.errors.name = ['Product name is required']
      }
      if (!this.image) {
        this.errors.image = ['Product image is required']
      }
      if (!this.description) {
        this.errors.description = ['Product description is required']
      }
      if (!this.category) {
        this.errors.category = ['Product category is required']
      }
      if (!this.unit) {
        this.errors.unit = ['Product unit is required']
      }
      if (this.stocked < 0) {
        this.errors.stocked = ['Number in stock must be greater than or equal to 0']
      }
      if (this.price < 0) {
        this.errors.price = ['Price must be greater than or equal to 0']
      }
      // Save product if input is valid
      if (Object.keys(this.errors).length === 0) {
        // Send request to save product
        axios.post('http://54.86.195.171:3000//api/v1/products', {
          name: this.name,
          image: this.image,
          description: this.description,
          category: this.category,
          unit: this.unit,
          stocked: this.stocked,
          price: this.price,
          featured: this.featured
        })
          .then(response => {
            this.loading = false
            this.$router.push({ name: 'Products' })
          })
          .catch(error => {
            this.loading = false
            if (error.response.status === 422) {
              this.errors = error.response.data.errors
            }
          })
      }
    },
    cancel() {
      this.$router.push({ name: 'Products' })
    }
  }
}
</script>
