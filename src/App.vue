<template>
  <div id="app">
    <FormularioWeb @add-users="addUsers" />
    <TablaUsuarios :users="users" v-if="users.length > 0" />
  </div>
</template>

<script setup>
import FormularioWeb from "./components/FormularioWeb.vue";
import TablaUsuarios from "./components/TablaUsuarios.vue";

let users = [];

const addUsers = (user) => {
  users.push(user);
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  font-family: Arial, Helvetica, sans-serif;
}
#app,
body {
  width: 100vw;
  background-color: rgb(19, 19, 43);
  margin: 0;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
