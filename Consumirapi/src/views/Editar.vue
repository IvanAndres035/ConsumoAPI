<template>
    <div>
        <Header />
            <div class="container">
                <form action="" class="form-horizontal">
                    <div class="form-group left row">
                        <label for="" class="control-label col.sm-2">Nombre</label>
                        <div class="col-sm-10">
                            <input type="text" class="form-control" name="Nombre" id="Nombre" v-model="form.NOMBRE_AREA">
                        </div>
                        <div class="form-group">
                            <button type="button" class="btn btn-primary" v-on:click="editar()">Editar</button>
                            <button type="button" class="btn btn-danger margen" v-on:click="eliminar()">Eliminar</button>
                            <button type="button" class="btn btn-dark margen" v-on:click="salir()">Salir</button>
                        </div>
                    </div>
                </form>
            </div>
        <Footer />
    </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';

export default{
    name:"Editar",
    components:{
        Header, 
        Footer
    },
    data:function(){
        return{
            
            form:{
                "ID_AREA" : "",
                "NOMBRE_AREA" : ""
            }
        }
    },

    methods:{
        editar(){
            axios.put("http://area-php.com/area",this.form)
            .then( data =>{
                console.log(data);
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        eliminar(){
            var enviar = {
                "ID_AREA" : this.form.ID_AREA  
            };
            axios.delete("http://area-php.com/area", { headers : enviar})
            .then( datos =>{
                console.log(datos);
                this.$router.push("/dashboard");
             });
        }
    },

    mounted:function(){
        this.form.ID_AREA = this.$route.params.ID_AREA;
        axios.get("http://area-php.com/area?id="+ this.form.ID_AREA)
        
        .then( datos =>{
            this.form.NOMBRE_AREA = datos.data.NOMBRE_AREA;
            
            console.log(this.form);
        })
    }
}

</script>

<style scoped> 
.left{
    text-align: left;
}
</style>