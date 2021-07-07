<template>
    <div>
        <Header />
            <div class="container">
                <form action="" class="form-horizontal">
                    <div class="form-group left row">
                        <label for="" class="control-label col.sm-2">NOMBRE_AREA</label>
                        <div class="col-sm-10">
                            <input type="text" class="form-control" name="NOMBRE_AREA" id="NOMBRE_AREA" v-model="form.NOMBRE_AREA">
                        </div>
                        <div class="form-group">
                            <button type="button" class="btn btn-primary" v-on:click="guardar()">Guardar</button>
                            <button type="button" class="btn btn-dark margen" v-on:click="salir()">Salir</button>
                        </div>
                    </div>
                </form>
            </div>
        <Footer />
    </div>
</template>

<script>
import Header from '@/components/Header.vue/'
import Footer from '@/components/Footer.vue/'
import axios from 'axios'

export default{
    name:"Nuevo",
    data:function(){
        return{            
            form:{
                "ID_AREA" : "",
                "NOMBRE_AREA" : ""
                }
            }
        },

    components:{
        Header,
        Footer
    },
    methods:{
        guardar(){
            //this.form.token = localStorage.getItem("token");
            axios.post("http://area-php.com/area", this.form)
            .then( data =>{
                console.log(data);
                this.makeToast("Hecho","area creada", "success");
                this.$router.push("/dashboard");
            }).catch( e =>{
                console.log(e);
                this.makeToast("Error","Error Al Guardar", "error");
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        makeToast(titulo,texto,tipo) {
            this.toastCount++
            this.$bvToast.toast(texto, {
            title: titulo,
            variant: tipo,
            autoHideDelay: 5000,
            appendToast: true
            })
        }
    }
}

</script>

<style scoped>
.left{
    text-align: left;
}
</style>