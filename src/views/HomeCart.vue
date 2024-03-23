<template>
    <h1>Shopping Cart</h1>
    
    <div v-for="item in items" :key="item.id">
      <h3>{{ item.name }}</h3>
       ₱{{ item.price }} 
      <button @click="addToCart(item)">Add to Cart</button>
    </div>
    
    <h2>Cart</h2>
    <ul>
      <li v-for="(item, index) in cart" :key="item.id">
        {{ item.name }} | ₱{{ item.price }}
        <button @click="removeFromCart(index)">Remove</button> |
        <button @click="updateQuantity(index, 'decrease')">-</button>
        {{ item.quantity }}
        <button @click="updateQuantity(index, 'increase')">+</button>
      </li>
    </ul>
    
    <h3>Total: ₱{{ total }}</h3>





    <button @click="handleLogout">Logout</button>
</template>

<script>
    export default {
     data: () =>{
        return {
          items: [
            { id: 1, name: 'Twist-O', price: 10 },
            { id: 2, name: 'V-Cut', price: 20 },
            { id: 3, name: 'Piattos', price: 15 },
            { id: 4, name: 'Shampoo', price: 8 },
            { id: 5, name: 'Noodles', price: 16 },
            { id: 6, name: 'Soap', price: 18 },
            { id: 7, name: 'Potato Choips', price: 8 }
          ],
          cart: []
        }
      },
      methods: {
        addToCart(item) {
          const index = this.cart.findIndex(cartItem => cartItem.id === item.id);
          if (index !== -1) {
            this.cart[index].quantity++;
          } else {
            this.cart.push({...item, quantity: 1});
          }
        },
        removeFromCart(index) {
          this.cart.splice(index, 1);
        },
        updateQuantity(index, action) {
          if (action === 'increase') {
            this.cart[index].quantity++;
          } else if (action === 'decrease' && this.cart[index].quantity > 1) {
            this.cart[index].quantity--;
          }
        },
        handleLogout() {
            localStorage.removeItem('token')
            this.$router.push('/login')
        }
      },
      computed: {
        total() {
          return this.cart.reduce((total, item) => total + (item.price * item.quantity), 0);
        }
      }
    }
</script>

<style>
  body {
      font-family: 'Arial', sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f4f4f4;
    }
    #app {
      max-width: 800px;
      margin: 20px auto;
      padding: 20px;
      background-color: #fff;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }
    h1, h2, h3 {
      margin-top: 0;
      color: #333;
    }
    ul {
      list-style: none;
      padding: 0;
    }
    li {
      margin-bottom: 10px;
      border-bottom: 1px solid #ddd;
      padding-bottom: 10px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    button {
      padding: 8px 16px;
      cursor: pointer;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 4px;
      transition: background-color 0.3s ease;
    }
    button:hover {
      background-color: #45a049;
    }
    .item-container {
      border: 1px solid #ddd;
      border-radius: 8px;
      padding: 10px;
      margin-bottom: 20px;
      background-color: #f9f9f9;
    }
    .item-container h3 {
      margin-top: 0;
      color: #555;
    }
    .cart-total {
      font-size: 1.2rem;
      margin-top: 20px;
    }
</style>
