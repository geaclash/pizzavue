<template>
    <v-app >
        <v-container>
            <v-layout row>
            <v-flex xs12 sm8 offset-sm2>
                <v-card>
                <v-card-title class="primary white--text"><h1 class="text-md-center">Regístrate</h1></v-card-title>

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

                            <v-flex xs2>
                                  <v-combobox
                                    v-model="register.document_type"
                                    :items="['V','G','E','J']"
                                    label="Tipo"
                                    ></v-combobox>


                            </v-flex>
                            <v-flex xs3 ml-3>
                                  <v-text-field
                                    label="Cédula"
                                    v-model="register.document_number"
                                    type="numeric"
                                    required></v-text-field>
                            </v-flex>
                        </v-layout>
                        <v-layout row>
                            <v-flex xs6>
                                <v-text-field
                                name="name"
                                label="Nombre"
                                id="name"
                                v-model="register.name"
                                type="text"
                                required></v-text-field>
                            </v-flex>
                            <v-flex xs6 ml-5>
                                <v-text-field
                                name="apellido"
                                label="Apellido"
                                id="apellido"
                                v-model="register.lastname"
                                type="text"
                                required></v-text-field>
                            </v-flex>
                        </v-layout>

                        <v-layout row>

                            <v-flex xs6 >
                                <v-text-field
                                name="email"
                                label="Correo"
                                id="email"
                                v-model="register.email"
                                type="email"
                                required></v-text-field>
                            </v-flex>
                            <v-flex xs6 ml-5>
                                <v-text-field
                                name="telefono"
                                label="Teléfono"
                                id="telefono"
                                v-model="register.phone"
                                type="text"
                                required></v-text-field>
                            </v-flex>
                        </v-layout>
                        <v-layout row>

                             <v-flex xs6 >
                                <v-menu
                                    ref="borndate"
                                    :close-on-content-click="false"
                                    v-model="register.borndate"
                                    :nudge-right="40"
                                    :return-value.sync="register.borndate"
                                    lazy
                                    transition="scale-transition"
                                    offset-y
                                    full-width
                                    min-width="290px">
                                    <v-text-field
                                    slot="activator"
                                    v-model="register.borndate"
                                    label="Fecha de Nacimiento"
                                    prepend-icon="event"
                                    readonly
                                    ></v-text-field>
                                    <v-date-picker v-model="register.borndate" @input="$refs.borndate.save(register.borndate)"></v-date-picker>

                                </v-menu>
                            </v-flex>
                            <v-flex xs6 ml-5>
                                  <v-combobox
                                    v-model="register.gender"
                                    :items="['Femenino','Masculino']"
                                    label="Género"
                                    ></v-combobox>
                            </v-flex>
                        </v-layout>                       

                        <v-layout wrap>
                            <v-flex xs12>
                                <v-textarea
                                        
                                        name=""
                                        v-model="register.address"
                                        label="Dirección"
                                        value=""
                                        ></v-textarea>
                            </v-flex>

                        </v-layout>
                                                       
                        <v-layout row>
                            <v-flex xs6>
                                <v-text-field
                                name="password"
                                label="Contraseña"
                                id="password"
                                v-model="register.password"
                                type="password"
                                required></v-text-field>
                            </v-flex>

                            <v-flex xs6 ml-5>
                                <v-text-field
                                name="confirm-password"
                                label="Confirmar contraseña"
                                id="password-confirm"
                                v-model="register.passwordconfirm"
                                type="password"
                                required></v-text-field>

                            </v-flex>
                        </v-layout>

                        <v-layout row  wrap align-center>
                            <v-flex class="text-xs-center" xs12>
                                <v-btn type="submit"   color="success">Registrarse</v-btn>
                            </v-flex>

                        </v-layout>
                        <p class="mb-3 text-center"><a href="">¿Ya tienes cuenta? Ingresar</a></p>
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
        register:{}
        //email: '',
        //password: '',
        //confirmPassword: ''
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