<template>
  <table>
    <thead>
      <tr>
        <th>Nombre</th>
        <th>Edad</th>
        <th>Email</th>
        <th>Contraseña</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(user, i) in users" :key="i">
        <td>{{ user.name }}</td>
        <td>{{ user.age }}</td>
        <td>{{ user.email }}</td>
        <td>{{ user.password }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
const { user } = defineProps(["user"]);
</script>

<style scoped>
table {
  border-radius: 10px;
  padding: 50px 20px;
  margin: 20px;
  background-color: white;
  border-collapse: collapse;
  vertical-align: middle;
  color: rgb(19, 19, 43);
}

td,
th {
  padding: 5px 10px;
  text-align: start;
  border: 1px solid rgb(19, 19, 43);
}

th {
  text-align: center;
  font-weight: bold;
}

.row {
  font-weight: bold;
  background-color: white;
  color: #2e354f;
  border: 1px solid #2e354f;
}
</style>
