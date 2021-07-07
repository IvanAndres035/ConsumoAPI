<template>
    <div>
        <Header/>
            <div class="container izquierda">

                <table class="table table-hover">
                    <thead>
                        <tr>
                            <th scope="col">ID_AREA</th>
                            <th scope="col">NOMBRE_AREA</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="area in Listaregistros" :key="area.ID_AREA" v-on:click="editar(area.ID_AREA)">
                            <th scope="row">{{ area.ID_AREA }}</th>
                            <td>{{ area.NOMBRE_AREA }}</td>
                        </tr>
                    </tbody>
                </table>
                <br>
                <button class="btn btn-primary" v-on:click="nueva()"> Nueva Area </button>
            </div>    
        <Footer/>  
    </div>    
</template>

<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';

export default{
    name: "Dashboard",
    data(){
        return{
            Listaregistros:null,
            pagina:1
        }
    },
    components: {
        Header,
        Footer
    },
    methods:{
        editar(ID_AREA){
            this.$router.push('/editar/' + ID_AREA);
        },
        nueva(){
            this.$router.push('/nuevo');
        }
    },
    mounted:function(){
        let direccion = "http://area-php.com/area?page=1" + this.pagina;
        axios.get(direccion).then( data =>{
            this.Listaregistros = data.data;
        });
    }
}
</script>

<style scoped>
    .izquierda{
        text-align: left;
    }

</style>