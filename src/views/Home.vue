<template>
<v-container class="pa-4" fluid grid-list-md>
    <v-layout wrap>
      <v-flex xs12>
        <h1 class="display-1 mb-1">Panel de administración</h1>
      </v-flex>
      <v-flex xs12 md6>
    
        <v-layout wrap>
          <v-flex xs6>
            <v-card height='100%' class="primary white--text text-xs-center">
              <v-card-text>
                <div class="display-1 mb-2">
                    15
                </div>
                Pedidos por usuario
              </v-card-text>

            </v-card>
          </v-flex>

          <v-flex xs6>
            <v-card height='100%' class="primary white--text text-xs-center">
              <v-card-text>
                <div class="display-1 mb-2">
                    15
                </div>
                Pedidos por usuario
              </v-card-text>

            </v-card>
          </v-flex>

          <v-flex xs6>
              <v-card height='100%' class="primary white--text text-xs-center">
                <v-card-text>
                  <div class="display-1 mb-2">
                      40
                  </div>
                  Pizzas hechas
                </v-card-text>

              </v-card>
          </v-flex>

          <v-flex xs6>
            <v-card height='100%' class="primary white--text text-xs-center">
              <v-card-text>
                <div class="display-1 mb-2">
                    15
                </div>
                Pedidos por usuario
              </v-card-text>

            </v-card>

          </v-flex>
        </v-layout>
      </v-flex>
      <v-flex md6>
        <v-card height='100%'>
          <v-card-title class="grey  darken-4 grey--text"><h3>Ordenes activas</h3></v-card-title>
          <v-data-table class="mt-1" :headers='ordenesActivasHeader'  :items='ordenesActivas'>
              <template slot='items' slot-scope='props'>
                <td>{{props.item.usuario}}</td>
                <td>{{props.item.direccion}}</td>
                <td>{{props.item.estatus}}</td>
              </template>

          </v-data-table>

        </v-card>

      </v-flex>
      </v-layout>
    </v-layout>

</v-container>
</template>

<script>
export default {
  data() {
    return {
      ordenesActivasHeader:[
          {
            text: 'Usuario',
            align: 'left',
            sortable: false,
            value: 'usuario'
          },
          { text: 'Direccion', value: 'direccion' },

          { text: 'Estatus', value: 'estatus' }
        ],
      ordenesActivas: [
        {
          usuario: 'randy',
          direccion: 'Universidad Rómulo Gallegos',
          estatus: 'Preparación'
        }
      ]
    }
  }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
