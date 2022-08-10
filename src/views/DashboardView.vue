<template>
    <div>
        <Header/>

            <div class="container">
                <table class="table table-hover">
                <thead>
                    <tr>
                        <th scope="col">ID</th>
                        <th scope="col">Nombre</th>
                        <th scope="col">DNI</th>
                        <th scope="col">Telefono</th>
                        <th scope="col">Correo</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="paciente in Listapacientes" :key="paciente.PacienteId" v-on:click="editar(paciente.PacienteId)">
                        <th scope="row">{{paciente.PacienteId}}</th>
                        <td>{{ paciente.Nombre }}</td>
                        <td>{{ paciente.DNI }}</td>
                        <td>{{ paciente.Telefono }}</td>
                        <td>{{ paciente.Correo }}</td>
                    </tr>
                  
                </tbody>
                </table>  

            </div>

        <Footer/>
    </div>
</template>

<script>
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
import axios from 'axios';

export default {
    name: "DashboardView",
    data(){
        return{
            Listapacientes:null,
            pagina:1
        }
    },
    components: {
        Header,
        Footer
    },
    methods: {
        editar(id){
            //console.log(id)
            this.$router.push('/editar/'+ id);
        }
    },
    mounted:function(){
        let direccion = "https://api.solodata.es/pacientes?page=" + this.pagina;
        axios.get(direccion).then(data =>{
            //console.log(data)
            this.Listapacientes = data.data
        })
    }
}

</script>

<style lang="stylus" scoped>

</style>