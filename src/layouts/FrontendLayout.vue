<template>
    <v-app >
        <v-toolbar class="primary white--text">
            <v-toolbar-title v-text="title"></v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn flat color="primary" class="white--text">Ingresar</v-btn>

        </v-toolbar>
        <v-content>
            <router-view></router-view>
            <v-footer class="blue darken-2">
                <v-layout row wrap align-center>
                <v-flex xs12>
                    <div class="white--text ml-3">
                    Made with
                    <v-icon class="red--text">favorite</v-icon>
                    by <a class="white--text" href="https://vuetifyjs.com" target="_blank">Vuetify</a>
                    and <a class="white--text" href="https://github.com/vwxyzjn">Costa Huang</a>
                    </div>
                </v-flex>
                </v-layout>
            </v-footer>
        </v-content>
    </v-app>
</template>

<style>
    

</style>





<script>
    import top from '@/components/frontend/top';
    import foot from '@/components/frontend/foot';
   
    export default {
         data() {
            return {
                title: 'Pizza.js'
            }
        },
        components: {
            foot: foot,
            top: top
        }
    }
</script>