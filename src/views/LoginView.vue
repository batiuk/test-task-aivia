<template>
  <v-card class="mx-auto mt-8" max-width="500">
    <v-card-title class="text-center">Login</v-card-title>

    <v-card-text>
      <v-form>
        <v-text-field
          v-model.trim="fields.email"
          :error-messages="v$?.email?.$errors[0]?.$message"
          label="Email"
          type="email"
          required
        ></v-text-field>

        <v-text-field
          v-model.trim="fields.password"
          :error-messages="v$?.password?.$errors[0]?.$message"
          label="Password"
          type="password"
          required
        ></v-text-field>
      </v-form>
    </v-card-text>

    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn color="primary" @click="submitForm">Login</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script setup>
import {reactive, ref} from 'vue'
import {required, email, minLength} from '@vuelidate/validators'
import useVuelidate from "@vuelidate/core";
import router from "@/router";

const fields = reactive({
  email: '',
  password: '',
})
const rules = {
  email: {required, email},
  password: {required, minLength: minLength(6)},
}

const v$ = ref(useVuelidate(rules, fields))
async function submitForm() {
  const isValid = await v$.value.$validate()
  if (!isValid) {
    return
  }
  await router.push({path: '/game'})
}
</script>
