<template>
    <div>
        <Header />
            <div class="container">
                <form action="" class="form-horizontal">
                    <div class="form-group left row">
                        <label for="" class="control-label col.sm-2">Nombre</label>
                        <div class="col-sm-10">
                            <input type="text" class="form-control" name="NOMBRE_ESTADO" id="NOMBRE_ESTADO" v-model="form.NOMBRE_ESTADO">
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
                "ID_ESTADO" : "",
                "NOMBRE_ESTADO" : ""
            }
        }
    },

    methods:{
        editar(){
            axios.put("http://api-restful-php.com/estado",this.form)
            .then( data =>{
                console.log(data);
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        eliminar(){
            var enviar = {
                "ID_ESTADO" : this.form.ID_ESTADO  
            };
            axios.delete("http://api-restful-php.com/estado", { headers : enviar})
            .then( datos =>{
                console.log(datos);
                this.$router.push("/dashboard");
             });
        }
    },

    mounted:function(){
        this.form.ID_ESTADO = this.$route.params.ID_ESTADO;
        axios.get("http://api-restful-php.com/estado?id="+ this.form.ID_ESTADO)
        
        .then( datos =>{
            this.form.NOMBRE_ESTADO = datos.data.NOMBRE_ESTADO;
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