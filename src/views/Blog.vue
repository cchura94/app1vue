<template>
    <div class="container">
        <div class="row">
            <div class="col-md-12">
                <h1>Blog</h1>
                <h2>{{ titulo }}</h2>
                <h3>{{ valor_seleccionado }}</h3>
                <button @click="cambiarTitulo()">Cambiar Titulo</button>
                {{ lista_categorias }}
                <select v-model="valor_seleccionado">
                    <option v-for="cat in lista_categorias" :key="cat">{{ cat }}</option>
                </select>
                <input type="text" v-model="titulo">
            </div>
        </div>
        <div class="row">
            <div class="col-md-4" v-for="(art, index) in lista_articulos" :key="index">
                <Tarjeta :datos="art"></Tarjeta>
            </div>
        </div>        
        
    </div>
</template>

<script>
import Tarjeta from '@/components/Tarjeta.vue'
import axios from 'axios'

export default {
    components: {
        Tarjeta
    },
    data(){
        return {
            titulo: "Mi pagina de Blog",
            lista_categorias: ["Javascript", "typescript", "PHP"],
            lista_articulos: [],
            valor_seleccionado: ''
        }
    },
    async created(){
        console.log("CREATED");
        const {data} = await axios.get('https://dev.to/api/articles?page=2');
        console.log(data)
        this.lista_articulos = data
    },
    mounted(){
        console.log("MOUNTED");
    },
    methods: {
        cambiarTitulo(){
            this.titulo = "Otro titulo";
        }
    }
    
}
</script>

<style>

</style>
