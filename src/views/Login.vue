<template>
    <v-app >
        <v-container>
            <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
                <v-card>
                <v-card-title class="primary white--text"><h1 class="text-md-center">Ingresar al sistema</h1></v-card-title>

                <v-card-text>
                    <v-container>
                        <v-layout row wrap align-center>
                            <v-flex class="text-xs-center">
                                <v-avatar size="150"  style="display: inline-block;">
                                    <img src="@/assets/user.svg" alt="">
                                </v-avatar>
                                
                            </v-flex>
                        </v-layout>
                    <form @submit.prevent="onSignup">
                        <v-layout row>
                        <v-flex xs12>
                            <v-text-field
                            name="email"
                            label="Correo"
                            id="email"
                            v-model="email"
                            type="email"
                            required></v-text-field>
                        </v-flex>
                        </v-layout>
                        <v-layout row>
                        <v-flex xs12>
                            <v-text-field
                            name="password"
                            label="Contraseña"
                            id="password"
                            v-model="password"
                            type="password"
                            required></v-text-field>
                        </v-flex>
                        </v-layout>

                        <v-layout row  wrap align-center>
                        <v-flex class="text-xs-center" xs12>
                            <v-btn type="submit"   color="success">Entrar</v-btn>
                        </v-flex>

                        
                        
                        </v-layout>
                        <p class="mb-3 text-center"><a href="">¿Olvidaste tu contraseña?</a></p>
                        <p class="mb-3 text-center"><a href="">Regístrate</a></p>
                    </form>
                    </v-container>
                </v-card-text>
                </v-card>
            </v-flex>
            </v-layout>
        </v-container>
    </v-app>
</template>

<script>
  export default {
    beforeCreate() {
      this.$store.commit('SET_LAYOUT', 'blank-layout')
    },
    data () {
      return {
        email: '',
        password: '',
        confirmPassword: ''
      }
    },
    computed: {
      comparePasswords () {
        return this.password !== this.confirmPassword ? 'Passwords do not match' : ''
      },
      user () {
        return this.$store.getters.user
      }
    },
    watch: {
      user (value) {
        if (value !== null && value !== undefined) {
          this.$router.push('/')
        }
      }
    },
    methods: {


      onSignup () {
          
        this.$store.dispatch('signUserUp', {email: this.email, password: this.password})
      }
    }
  }
</script>