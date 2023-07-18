<template>
  <form @submit.prevent.stop="submitForm" class="form">
    <label for="name">
      <span>Nombre Completo</span>
      <input name="name" id="name" type="text" v-model="state.name" />
    </label>
    <span v-if="v$.name.$error">
      {{ v$.name.$errors[0].$message }}
    </span>

    <label for="age">
      <span>Edad</span>
      <input id="age" name="age" type="number" v-model="state.age" />
      <span v-if="v$.age.$error">
        {{ v$.age.$errors[0].$message }}
      </span>
    </label>

    <label for="email">
      <span>Email</span>
      <input id="email" name="email" type="email" v-model="state.email" />
      <span v-if="v$.email.$error">
        {{ v$.email.$errors[0].$message }}
      </span>
    </label>

    <label for="password">
      <span>Contraseña</span>
      <input
        id="password"
        name="password"
        type="password"
        v-model="state.password"
      />
      <span v-if="v$.password.$error">
        {{ v$.name.$password[0].$message }}
      </span>
    </label>

    <button type="submit" class="button">Enviar</button>
  </form>
</template>

<script setup>
import { reactive, computed } from "vue";
import { useVuelidate } from "@vuelidate/core";
import {
  required,
  email,
  minLength,
  minValue,
  helpers,
} from "@vuelidate/validators";

const state = reactive({
  name: "",
  age: 0,
  email: "",
  password: "",
});

const rules = computed(() => {
  return {
    name: {
      required,
      minLength: helpers.withMessage(
        "Debe tenér como mínimo dos caracteres",
        minLength(2)
      ),
    },
    age: {
      required,
      minValue: helpers.withMessage("Debe ser mayor de edad", minValue(18)),
    },
    email: { required, email },
    password: {
      required,
      minLength: helpers.withMessage(
        "Debe tenér como mínimo seis caracteres",
        minLength(6)
      ),
    },
  };
});

const v$ = useVuelidate(rules, state);
const emit = defineEmits(["add-users"]);

const submitForm = async () => {
  console.log(v$);
  const result = await v$.value.$validate();
  if (result) {
    emit("add-users", { ...state });
    resetFormData();
    v$.$reset();
  }
};

const resetFormData = () => {
  Object.keys(state).forEach((key) => (state[key] = ""));
};
</script>

<style scoped>
.form {
  background-color: white;
  border-radius: 20px;
  padding: 50px 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
label {
  width: 100%;
  color: rgb(19, 19, 43);
  font-size: 15px;
  display: flex;
  flex-direction: column;
  height: 75px;
}
input {
  border: 2px solid rgb(19, 19, 43);
  padding: 8px 16px;
  background-color: white;
  border-radius: 10px;
  font-size: 16px;
  margin: 2px 0 2px 0;
  color: rgb(19, 19, 43);
}

input::placeholder {
  color: rgba(255, 255, 255, 0.5);
}
input:focus {
  outline: none !important;
  border: 2px solid rgb(93, 92, 124);
  color: rgb(19, 19, 43);
}

.error {
  color: red;
  font-size: 12px;
  margin-bottom: 5px;
}

.button {
  width: 100%;
  background-color: rgb(19, 19, 43);
  color: white;
  font-size: 16px;
  border: none;
  border-radius: 10px;
  padding: 5px 0;
}
</style>
