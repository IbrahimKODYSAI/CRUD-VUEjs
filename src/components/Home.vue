<template>
  <div>
    <h2>liste des produits de {{smartphone}}</h2>
    <form >
       <input 
        name="id"
        placeholder="id"
        type="text"
        v-model="phoneId"
      >
      <input 
        name="phoneName"
        placeholder="Phone name"
        type="text"
        v-model="phoneName"
      >
      <input 
        name="phoneType"
        placeholder="Phone Type"
        type="text"
        v-model="phoneType"
      >
      <input 
        name="phonePrice"
        placeholder="Phone price"
        type="number"
        v-model="phonePrice"
      >
      <input 
        name="phoneRating"
        placeholder="Phone rating"
        type="number"
        max="5"
        min="0"
        v-model="phoneRating"
      >
      <input 
        name="phoneWarranty"
        placeholder="Phone warranty"
        type="number"
        max="7"
        min="0"
        v-model="phoneWarranty"
      >
        <input type="checkbox" id="checkbox" v-model="phoneAvailable">
        <label for="checkbox">Available: {{ phoneAvailable ? 'yes' : 'no' }}</label>
      <button @click.prevent="addNewProduct">Add +</button>
    </form>
    <ul>
      <li v-for="(smartphone, index) in smartphonesDatas" :key="index">
        <form >
          <p>
            <span>Name :</span>
            {{smartphone.name}}
          </p>
          <input 
            name="phoneName"
            placeholder="Phone name"
            type="text"
            v-model="phoneName"
          >
          <p> <span>Type :</span>  {{smartphone.type}}</p>
          <input 
            name="phoneType"
            placeholder="Phone Type"
            type="text"
            v-model="phoneType"
          >
          <p> <span>Price :</span>  {{smartphone.price}} €</p>
          <input 
            name="phonePrice"
            placeholder="Phone price"
            type="number"
            v-model="phonePrice"
          >
          <p> <span>Rating :</span> {{smartphone.rating}}</p>
          <input 
            name="phoneRating"
            placeholder="Phone rating"
            type="number"
            max="5"
            min="0"
            v-model="phoneRating"
          >
          <p> <span>warranty :</span> {{smartphone.warranty_years}}</p>
          <input 
            name="phoneWarranty"
            placeholder="Phone warranty"
            type="number"
            max="7"
            min="0"
            v-model="phoneWarranty"
          >
          <p> <span>Available :</span>  {{smartphone.available ? 'Yes' : 'No' }}</p>
          <input type="checkbox" id="checkbox" v-model="phoneAvailable">
          <label for="checkbox">Available: {{ phoneAvailable ? 'yes' : 'no' }}</label>
          <button @click="updateProduct(smartphone._id)">Edit</button>
        </form>
        <button @click="deleteProduct(smartphone._id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Home',
  props: ['smartphone'],
  data() {
    return {
      phoneId: '',
      phoneName: '',
      phoneType: '',
      phonePrice: '',
      phoneRating: '',
      phoneWarranty: '',
      phoneAvailable: false,
      smartphonesDatas: null,
    }
  },
  mounted() {
    this.getAllProducts();
  },
  methods: {
    addNewProduct() {
      this.smartphonesDatas.push({
        "_id" : this.phoneId,
        "name" : this.phoneName, 
        "type" : this.phoneType, 
        "price" : this.phonePrice, 
        "rating" : this.phoneRating,
        "warranty_years" : this.phoneWarranty, 
        "available" : this.phoneAvailable
      })
      this.phoneId = '';
      this.phoneName = '';
      this.phoneType = '';
      this.phonePrice = '';
      this.phoneRating = '';
      this.phoneWarranty = '';
    },
    getAllProducts() {
      fetch('http://localhost:3000/api/product', {
          method: 'get',
          headers: {
            'content-type': 'application/json'
          }
        })
        .then((res) => {
          return res.json();
        })
        .then((data) => {
          this.smartphonesDatas = data;
        })
        .catch((err) => {
          return err;
        })
    },
    deleteProduct(id) {
      fetch(`http://localhost:3000/api/product/${id}`, {
        method: 'delete'
      })
      .then((res) => {
        res.json();
      })
      .catch((err) => {
        return err;
      })
      this.getAllProducts();
    },
    updateProduct(id) {
      fetch(`http://localhost:3000/api/product/${id}`, {
        method: 'put',
        body: JSON.stringify({
          name: this.phoneName,
          type: this.phoneType,
          price: this.phonePrice,
          rating: this.phoneRating,
          warranty_years: this.phoneWarranty,
          available: this.available
        }),
        headers: {
          'Content-type': 'application/json; charset=UTF-8'
        }
      })
      .then(response => response.json())
      .then(json => console.log(json))
      .catch(err => {
        console.error(err)
      })
      this.getAllProducts();
    }
  }
}
</script>


<style>
  ul {
    margin-top: 5rem;
    display: flex;
    justify-content: space-evenly;
    }

    li {
    box-shadow: 0 4px 12px 0px rgba(0,0,0,.25);
    border-radius: 5px;
    width: 300px;
    height: auto;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;

      }
    span{
      font-weight: bold;
    }
    p{
      margin-left: 1em;
      text-align: justify;
      }
    form {
      margin: auto;
      width: 300px;
      display: flex;
      flex-direction: column;
    }
</style>