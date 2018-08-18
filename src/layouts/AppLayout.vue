<template>
  <v-app>
    <v-navigation-drawer
      
      :mini-variant="miniVariant"
      :clipped="clipped"
      v-model="drawer"
      enable-resize-watcher
      stateless
      floating
      class="red darken-4 white--text"
      width='220'
      app
    >
      <!--v-toolbar class="brown darken-4">
     

      </v-toolbar-->
          
      <v-list class="red darken-4 white--text">
        
        <v-list-tile value="true" @click=''>
          <v-list-tile-action>
            <v-icon color="white">home</v-icon>
          </v-list-tile-action>  
          <v-list-tile-content>
            <v-list-tile-title class="white--text">Inicio</v-list-tile-title>

          </v-list-tile-content>
        </v-list-tile>
        <template v-for="(submenu,j) in menu">
          <v-subheader :key="j" class="mt-3 black--text white--text">
            {{submenu.title}}
          </v-subheader>


          
          <v-list-tile
            value="true"
            v-for="(item, i) in submenu.items"
            :key="submenu.title+'-'+i"
            @click='' 
          >
            <v-list-tile-action>
              <v-icon  color="white">{{ item.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title class="white--text" v-text="item.title"></v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </template>

      </v-list>
              

    </v-navigation-drawer>
    <v-toolbar
      app
      :clipped-left="clipped"
            color="red white--text"

    >
       

      <v-toolbar-side-icon color="red" class="white--text" @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title v-text="title"></v-toolbar-title>

      <v-btn icon @click.stop="miniVariant = !miniVariant" class="red white--text">
        <v-icon v-html="miniVariant ? 'chevron_right' : 'chevron_left'"></v-icon>
      </v-btn>

      <v-spacer></v-spacer>

      <v-menu offset-y>

          <v-avatar size="36" class="mr-2"  slot='activator'>
            <img src="http://i.pravatar.cc/150?img=53" alt="">
          </v-avatar>
        <v-list>
          <v-list-tile @click=''>
            <v-icon class="mr-2">settings</v-icon>
            <v-list-tile-title>Configuraciones</v-list-tile-title>
          </v-list-tile>

          <v-list-tile @click=''>
            <v-icon class="mr-2">exit_to_app</v-icon>
            <v-list-tile-title>Salir</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-menu>

    </v-toolbar>
    <v-content>
      <router-view/>
    </v-content>
    <!--v-navigation-drawer
      temporary
      :right="right"
      v-model="rightDrawer"
      fixed
      app
    >
      <v-list>
        <v-list-tile @click="right = !right">
          <v-list-tile-action>
            <v-icon>compare_arrows</v-icon>
          </v-list-tile-action>
          <v-list-tile-title>Switch drawer (click me)</v-list-tile-title>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer-->
    <v-footer :fixed="fixed" app class="grey darken-4 white--text">
      <v-spacer></v-spacer>
      <span>Todos los derechos e izquierdos reservados &copy; 2018</span>
      <v-spacer></v-spacer>
    </v-footer>
  </v-app>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      clipped: true,
      drawer: true,
      fixed: false,
      menu: [
       
        {
          title: "Pizzeria",
          items:[{
            icon: 'list',
            title: 'Ordenes'
          }
          ]
        },
        {
          title: "Administración",
          items:[{
            icon: 'supervisor_account',
            title: 'Usuarios'
          },
          {
            icon: 'account_circle',
            title: 'Clientes'
          }

          ],
          
        },
        {
          title: "Gestión de pizzas",
          items:[{
            icon: 'pie_chart',
            title: 'Pizzas'
          },
          {
            icon: 'group_work',
            title: 'Toppings'
          }
          ]
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Pizza.js'
    }
  }
}
</script>
