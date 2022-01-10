<template>
    <v-container>
        <v-img 
            src="../../assets/img/clientlogin.png" 
            lazy-src="../../assets/img/clientlogin.png"
            width="80%" 
            class="mx-auto"
        ></v-img>

        <v-card flat class="text-center">
            <h2>Client Login</h2>
            <p class="body-2 grey--text text--darken-2">Please enter the details below to continue.</p>
        </v-card>

        <v-card flat class="pa-5">
            <div>{{errors}}</div>
            <v-text-field
                label="Email"
                placeholder="Enter your email"
                outlined
                v-model="form.email"
            ></v-text-field>
            <v-text-field
                label="Password"
                placeholder="Password"
                :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
                :type="showPassword ? 'text' : 'password'"
                @click:append="showPassword = !showPassword"
                outlined
                v-model="form.password"
            ></v-text-field>

            <v-btn block x-large dark class="gradient-bg" @click="login">Login</v-btn>
        </v-card>

    </v-container>
</template>

<script>
import Client from "../../Apis/Client";

export default {
    data () {
        return {
            showPassword: false,
            form:{
                email: "",
                password: "",
                device_name: 'mobile'
            },
            errors:''
        }
    },
    methods:{
        login() {
            Client.login(this.form)
            .then((response) => {
                localStorage.setItem("token", response.data);
                this.$router.push({ name: "ClientDashboard" });
            })
            .catch((error) => {
            this.error = 'Wrong details';
                console.log(error.response);
            });
        },
}
}
</script>

<style>

</style>