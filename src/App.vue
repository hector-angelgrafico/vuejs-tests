<script setup>
import { RouterLink, RouterView } from 'vue-router'
import  { defineAsyncComponent, onMounted, ref, reactive, watch, computed, defineProps, provide, inject } from "vue";
//Composition API
onMounted( () => {

  console.log("onmounted");

}) 

const texto = ref("wey"); //Variable reactiva composition API 
const counter = ref(0);  //Ref una única variable de datos primitivos

const nombre = ref("Hector");
const apellidos = ref("Nevado");

const objeto = reactive({contador: 0}) //Reactive para objetos

setInterval( () => counter.value++, 1000);
setInterval( () => objeto.contador++, 6000);

//Watch: Primero variable que quiero comprobar y recibo nuevo valor y antiguo
watch( () => objeto.contador, (newValue,oldValue) => { 

  console.log(newValue+" VS "+oldValue);

})

const fullName = computed( () => {

  //return nombre.value+" "+apellidos.value;
  return `${nombre.value} ${apellidos.value}`;

})

const props = defineProps({
  firstName: String,
  lastName: String,
})


const username = provide("username", "HectorYellow46");

const usernameinject = inject("username", username);

const btn = ref(null);

console.log(btn.value);

watch( () => btn.value, (valor) => { 

console.log(valor)

})

//this.$refs.btn
</script>

<template>
  <header>
    <button ref="btn">Clickeame!</button>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
    
    <div class="wrapper">
      {{usernameinject}}
      {{text}}
      {{texto}} <br/> 
      {{fullName}} Llevas logeado: {{counter}} segundos ( {{objeto.contador}} minutos) <br/><br/>
      <HelloWorld firstName="Hector" msg="¡Hola!" />
      <button @click="show = !show">Menú</button>
      <transition name="fade">
         <Menu v-if="show" /> <!-- O usar v-show -->
      </transition>
      
      <Modal />
    </div>
  </header>

  <RouterView />
</template>

<script>
  const HelloWorld = defineAsyncComponent( () => import('./components/HelloWorld.vue'));
  const Menu = defineAsyncComponent( () => import('./components/Menu.vue'));
  const Modal = defineAsyncComponent( () => import ('./components/Modal.vue') );

export default {

  data() {
    return {
     show: false,
     text: 'Bienvenido/a'
    }
  },
  beforeCreate() {
    console.log("beforeCreate", this.$data, this.$el);
  },
  created() {
    console.log("Created", this.$data, this.$el);
  },
  mounted() {
    console.log("Mounted", this.$data, this.$el);
  }

};
</script>
<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}

/*
.fade-enter => Elemento que entra
.fade-leave => Elemento que sale 

.fade-enter-to: Cuando termina la transición
.fade-enter-active => Cuando está sucendiendo la transición
.fade-enter:from => Cuando inicia la transición 
*/
.fade-enter-active,
.fade-leave-active {

 transition: opacity 0.3s ease;


}

.fade-leave-to, .fade-enter-from {
  opacity:0;
}
</style>
