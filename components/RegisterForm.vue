<template>
    <v-app id="inspire">
        <v-main class="fill-height"
            fluid>
        
            <v-row
            align="center"
            justify="center"
            >
            <v-col
                cols="12"
                sm="8"
                md="4"
            >
                <v-card class="elevation-12">
                <v-toolbar
                    color="primary"
                    dark
                    flat
                >
                    <v-toolbar-title>Register</v-toolbar-title>
                    <v-spacer></v-spacer>
                    
                </v-toolbar>
                <v-card-text>
                    <v-form>
                        <v-text-field
                        label="Name"
                        name="login"
                        prepend-icon="mdi-account"
                        type="text"
                        v-model="username"
                        :error-messages="errors.username && errors.username.msg"
                    ></v-text-field>
                    <v-text-field
                        label="Email"
                        name="email"
                        prepend-icon="mdi-message"
                        type="text"
                        v-model="email"
                        :error-messages="errors.email && errors.email.msg"
                    ></v-text-field>

                    <v-text-field
                        id="password"
                        label="Password"
                        name="password"
                        prepend-icon="mdi-lock"
                        type="password"
                        v-model="password"
                        :error-messages="errors.password && errors.password.msg"
                    ></v-text-field>
                    <v-text-field
                        id="password_c"
                        label="Password Confirmation"
                        name="password"
                        prepend-icon="mdi-lock"
                        type="password"
                        v-model="password_c"
                        :error-messages="errors.password_c && errors.password_c.msg"
                    ></v-text-field>
                    </v-form>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="primary" @click="submitInfo">Register</v-btn>
                </v-card-actions>
                </v-card>
            </v-col>
            </v-row>
        </v-main>
    </v-app>
</template>

<script>
    export default {
        name: 'register-form',
        data: () => ({
            email: '',
            password: '',
            password_c: '',
            username: '',
            errors: {}
        }),
        methods: {
            async submitInfo() {
                let {email, username, password, password_c} = this;
                let data = await this.$axios.post('/user/register', {email, username, password, password_c}).then((res) => {
                    let {data} = res.data;
                    
                    this.$auth.loginWith('local', {data: {...data, password}}).then(() => {
                        console.log('Successfuly login!');
                    });
                }).catch(err => {
                    this.errors = err.response.data.data.errors;
                });
            }
        }
    }
</script>