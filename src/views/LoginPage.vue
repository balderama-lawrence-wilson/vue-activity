<template>
    <div>
      <h1>Login Page</h1>
      <form @submit.prevent="login">
        <input type="text" v-model="username" placeholder="Username">
        <input type="password" v-model="password" placeholder="Password">
        <button type="submit">Login</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        username: '',
        password: ''
      };
    },
    methods: {
      login() {
        if (this.username === 'user' && this.password === 'password') {
          localStorage.setItem('token', '12345')
          this.$router.push('/homecart');
        } else {
          alert('Invalid username or password');
        }
      }
    }
  }
  </script>
  
  <style scoped>
  input {
    display: block;
    margin: 10px auto;
    padding: 8px;
    width: 200px;
  }
  button {
    padding: 10px 20px;
    font-size: 16px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  </style>