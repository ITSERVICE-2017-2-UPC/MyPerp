<template>
   <div>
      <div>
         <div class="sidebar-wrapper" v-bind:class="{'sidebar-lg': !isHidden, 'sidebar-sm': isHidden}">
            <div class="sidebar-container">
               <div class="sidebar-logo">
                  <span>Hormigón ERP</span>
               </div>
               <div class="divider"></div>
               <div v-for="item in MenuItems" v-bind:key="item.index">
                  <div class="sidebar-item" v-on:click="setActiveIndexId(item.index)">
                     <span>{{item.name}}</span>
                  </div>
                  <div v-for="subitem in item.paths" v-bind:key="subitem.index">
                     <div class="menu-item-list" v-bind:style="{ 'height': (item.index === activeIndex) ? '46px' : '0px' }">
                        <div class="menu-item" v-on:click="mainRedirect(subitem.path)">
                           {{subitem.name}}
                        </div>
                     </div>
                  </div>
               </div>
               <div class="sidebar-item" v-on:click="redirectLogout()">
                  <span>Cerrar Sesión</span>
               </div>
            </div>
         </div>
      </div>
   </div>
</template>

<script>
export default {
   data(){
      return {
         activeIndex: '',
         MenuItems: [
            {
               'index': 1,
               'name': 'Configuración',
               'paths': [
                  {
                     'name': 'Gestionar Usuarios',
                     'index': 1,
                     'path': '/config/admin/usuario'
                  },
                  {
                     'name': 'Gestionar Perfiles',
                     'index': 2,
                     'path': '/config/admin/perfil'
                  },
                  {
                     'name': 'Usuario',
                     'index': 3,
                     'path': '/config/usuario'
                  },
               ]               
            },
            {
               'index': 2,
               'name': 'Logística',
               'paths': [
                  {
                     'name': 'Compras',
                     'index': 1,
                     'path': '/logistica/compras'
                  },
                  {
                     'name': 'Inventario',
                     'index': 2,
                     'path': '/logistica/inventario'
                  },
                  {
                     'name': 'Productos',
                     'index': 3,
                     'path': '/logistica/productos'
                  },
                  {
                     'name': 'Categorias',
                     'index': 4,
                     'path': '/logistica/categorias'
                  },
                  {
                     'name': 'Marcas',
                     'index': 5,
                     'path': '/logistica/marcas'
                  },
                  {
                     'name': 'Proveedor',
                     'index': 6,
                     'path': '/logistica/proveedor'
                  },
                  {
                     'name': 'Locales',
                     'index': 7,
                     'path': '/logistica/locales'
                  }
               ]
            }
         ]
      }
   },
   props: {
      'isHidden': {
         default: false,
      }
   },
   methods: {
      mainRedirect: function(route_path){
         console.log(route_path);
         this.$router.push(route_path);
      },
      redirectLogout: function(){
         this.$http.post('/logout').then(function(){
            document.location.href = '/';
         })
         .cath(function(err){
            console.log(err);
         });
      },
      setActiveIndexId(indexID){
         this.activeIndex = indexID;
      }
   }
}
</script>