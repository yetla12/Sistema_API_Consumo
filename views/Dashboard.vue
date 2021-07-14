<template>
    <div>
        <Header/>
            <div class="container izquierda">
                <table class="table table-hover">
                    <thead>
                        <tr>
                            <th scope="col">ID_ESTADO</th>
                            <th scope="col">NOMBRE_ESTADO</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="estado in Listaregistros" :key="estado.ID_ESTADO" v-on:click="editar(estado.ID_ESTADO)">
                            <th scope="row">{{ estado.ID_ESTADO }}</th>
                            <td>{{ estado.NOMBRE_ESTADO }}</td>
                        </tr>
                    </tbody>
                </table>
                <br>
                            <button class="btn btn-primary" v-on:click="nuevo()"> Nuevo Estado </button>
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
        editar(ID_ESTADO){
            this.$router.push('/editar/' + ID_ESTADO);
        },
        nuevo(){
            this.$router.push('/nuevo');
        }
    },
    mounted:function(){
        let direccion = "http://api-restful-php.com/estado?page=1" + this.pagina;
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