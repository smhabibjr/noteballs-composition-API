<template>
  <div class="auth">
    <div class="tabs is-centered">
      <ul>
        <li :class="{ 'is-active': !register }"><a @click.prevent="register = false">Log in</a></li>
        <li :class="{ 'is-active': register }"><a @click.prevent="register = true">Register</a></li>
      </ul>
    </div>

    <div class="card auth-form">
      <div class="card-content">
        <div class="title has-text-centered">
          {{ formTitle }}
        </div>
        <form @submit.prevent="onSubmit">
          <div class="field">
            <label class="label">Email</label>
            <div class="control">
              <input
                v-model="credentials.email"
                class="input"
                type="email"
                placeholder="e.g. alexsmith@gmail.com"
              />
            </div>
          </div>
          <div class="field">
            <label class="label">Password</label>
            <div class="control">
              <input
                v-model="credentials.password"
                class="input"
                type="password"
                placeholder="Enter a password"
              />
            </div>
          </div>

          <div class="field is-grouped is-grouped-right">
            <p class="control">
              <button class="button is-primary">{{ formTitle }}</button>
            </p>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, reactive, ref } from 'vue'
import { useStoreAuth } from '@/stores/storeAuth.js'

const storeAuth = useStoreAuth()

const register = ref(false)

const formTitle = computed(() => {
  return register.value ? 'Register' : 'Login'
})

const credentials = reactive({
  email: '',
  password: ''
})

const onSubmit = () => {
  if (!credentials.email || !credentials.password) {
    alert('hi ther')
  } else {
    if (register.value) {
      storeAuth.registerUser(credentials)
    } else {
      storeAuth.userLogin(credentials)
    }
  }
}
</script>

<style scoped>
.auth-form {
  max-width: 400px;
  margin: 0 auto;
}
</style>
