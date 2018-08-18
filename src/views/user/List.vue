<template>
    <v-container class="pa-4" fluid grid-list-md>
        <v-flex xs12>
        <h1 class="display-1 mb-1">Gestión de Usuarios</h1>
      </v-flex>
    <v-toolbar flat color="white">
      <v-toolbar-title>Lista de Usuarios</v-toolbar-title>
      <v-divider
        class="mx-2"
        inset
        vertical
      ></v-divider>
      <v-spacer></v-spacer>
      <v-dialog v-model="dialog" max-width="500px">
        <v-btn slot="activator" color="red" dark class="mb-2">Agregar Usuario</v-btn>
        <v-card>
          <v-card-title>
            <span class="headline">{{ formTitle }}</span>
          </v-card-title>

          <v-card-text>
            <v-container grid-list-md>
              <v-layout wrap>
                <v-flex xs12 sm6 md4>
                  <v-text-field v-model="editedItem.name" label="Nombre"></v-text-field>
                </v-flex>
                <v-flex xs12 sm6 md4>
                  <v-text-field v-model="editedItem.email" label="Correo"></v-text-field>
                </v-flex>
                <v-flex xs12 sm6 md4>
                  <v-text-field v-model="editedItem.role" label="Rol"></v-text-field>
                </v-flex>
                <v-flex xs12 class="text-xs-center text-sm-center text-md-center text-lg-center">
					<v-text-field label="Seleccionar Imagen" @click='pickFile' v-model='editedItem.image' prepend-icon='attach_file'></v-text-field>
					<input
						type="file"
						style="display: none"
						ref="image"
						accept="image/*"
						@change="onFilePicked"
					>
              		<img :src="editedItem.imageUrl" height="150" v-if="editedItem.imageUrl"/>
                    <p class="text-xs-center" v-if="editedItem.image">{{editedItem.image}}</p>
				</v-flex>

              </v-layout>
            </v-container>
          </v-card-text>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" flat @click.native="close">Cancelar</v-btn>
            <v-btn color="blue darken-1" flat @click.native="save">Guardar</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-toolbar>
    <v-data-table
      :headers="headers"
      :items="users"
      hide-actions
      class="elevation-1"
    >
      <template slot="items" slot-scope="props">
        <td>{{ props.item.name }}</td>
        <td class="text-xs-left">{{ props.item.email }}</td>
        <td class="text-xs-left">{{ props.item.role }}</td>
        <td class="text-xs-left">
             <v-avatar
                :tile="true"
                :size="80"
                color="grey lighten-4"
                >
              <img :src="require('@/assets/pizza-1.jpg')" alt="imagen">
            </v-avatar>
        </td>
        
        <td class="justify-center layout px-0">
          <v-icon
            small
            class="mr-2"
            @click="editItem(props.item)"
          >
            edit
          </v-icon>
          <v-icon
            small
            @click="deleteItem(props.item)"
          >
            delete
          </v-icon>
        </td>
      </template>
      <template slot="no-data">
        <v-btn color="primary" @click="initialize">Reiniciar</v-btn>
      </template>
    </v-data-table>
    </v-container>
</template>




<script>
import UploadButton from '../../components/UploadButton.vue';

  export default {
    data: () => ({
      dialog: false,
      headers: [
        {
          text: 'Nombre',
          align: 'left',
          sortable: false,
          value: 'name'
        },
        {
          text: 'E-Mail',
          align: 'left',
          sortable: false,
          value: 'description'
        },       
        { text: 'Rol', value: 'price', align: 'left', },
        { text: 'Imagen', value: 'image', align: 'left', },
        { text: 'Acciones', value: 'name', sortable: false }
      ],
      users: [],
      editedIndex: -1,
      editedItem: {
        name: '',
        email: '',
        rol: 0,
        image: '',
		imageUrl: '',
		imageFile: ''
        //protein: 0
      },
      defaultItem: {
        name: '',
        email: 0,
        role: 0,
        image: '',
		imageUrl: '',
		imageFile: ''
      }
    }),

    components: {
       UploadButton
    },
    
    computed: {
      formTitle () {
        return this.editedIndex === -1 ? ' Nueva pizza' : 'Editar Pizza'
      }
    },

    watch: {
      dialog (val) {
        val || this.close()
      }
    },

    created () {
      this.initialize()
    },

    methods: {
      initialize () {
        this.users = [
                {   
                    name: 'Randy',
                    email: 'randygil@webcoding.cl',   
                    role: 'SuperAdmin',
                    image: '@/assets/pizza-1.jpg'

                },
                            ]
      },

    pickFile () {
        this.$refs.image.click ()
    },

    onFilePicked (e) {
        const files = e.target.files
        if(files[0] !== undefined) {
            this.editedItem.image = files[0].name
            if(this.editedItem.image.lastIndexOf('.') <= 0) {
                return
            }
            const fr = new FileReader ()
            fr.readAsDataURL(files[0])
            fr.addEventListener('load', () => {
                this.editedItem.imageUrl = fr.result
                this.editedItem.imageFile = files[0] // this is an image file that can be sent to server...
            })
        } else {
            this.editedItem.image = ''
            this.editedItem.imageFile = ''
            this.editedItem.imageUrl = ''
        }
    },
    

      editItem (item) {
        this.editedIndex = this.users.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        const index = this.users.indexOf(item)
        confirm('¿Estás seguro de querer eliminar esta pizza?') && this.users.splice(index, 1)
      },

      close () {
        this.dialog = false
        setTimeout(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        }, 300)
      },

      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.users[this.editedIndex], this.editedItem)
        } else {
          this.users.push(this.editedItem)
        }
        this.close()
      }
    }
  }
</script>

<style>

</style>
