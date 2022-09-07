<template>
    <div>
        <button @click="toggle">
            Ventana modal
        </button>
        <teleport to="body">
            <div v-show="show" class="modal">
                <button @click="toggle">X</button>
                <h1>Título</h1>
                <p>Contenido</p>
            </div>
        </teleport>
    </div>
</template>
<!--
Ciclo de vida de los componentes, así tambien se sus hooks las cuales son funciones que nos permiten definir acciones en cada etapa del ciclo de los componentes

beforeCreate.
created.
beforeMount.
mounted.
beforeUpdate.
updated.
beforeUnmount.
unmounted.
-->
<script>

    export default {

      data() {
        return {
            show:false
        }
      },
      methods: {
        toggle() {

            this.show = !this.show;

        }
      }

    };
</script>

<style scoped>
    .modal {
    width: 100%;
    position: absolute;
    z-index: 999;
    background: black;
    height: 100vh;
    top: 0px;
    color: white;
    display: grid;
    place-content: center;
}
</style>