<template>
<div>
<v-tabs
        v-model="model"
        centered
        slider-color="yellow"
    >
        <v-tab href="#tab-1">Login</v-tab>
        <v-tab href="#tab-2">Signup</v-tab>
    </v-tabs>
    <v-tabs-items v-model="model">
      <v-tab-item
        value="tab-1"
      >
        <v-card flat>
            <login-form></login-form>
        </v-card>
      </v-tab-item>
      <v-tab-item
        value="tab-2"
      >
        <v-card flat>
            <register-form></register-form>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
</div>
</template>
    
<script>
  import LoginForm from '~/components/LoginForm';
  import RegisterForm from '~/components/RegisterForm';

  export default {
      data() {
          return {
              model: 'tab-1'
          }
      },
      components: {
          'login-form': LoginForm,
          'register-form': RegisterForm
      }
  }
</script>