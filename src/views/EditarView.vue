<template>
    <div>
        <Header />
            <div class="container">
                <form action="" class="form-horizontal">
                    <div class="form-group left">
                        <label for="" class="control-label col-sm-2">Nombre</label>
                            <div class="col-sm-4">
                                <input type="text" class="form-control" name="nombre" id="nombre" v-model="form.nombre">
                            </div>
                            <br>
                        <label for="" class="control-label col-sm-2">DNI</label>
                            <div class="col-sm-4">
                                <input type="text" class="form-control" name="dni" id="dni" v-model="form.dni">
                            </div>
                            <br>
                        <label for="" class="control-label col-sm-2">Correo</label>
                            <div class="col-sm-4">
                                <input type="text" class="form-control" name="correo" id="correo" v-model="form.correo">
                            </div>
                            <br>
                        <label for="" class="control-label col-sm-2">Codigo Postal</label>
                            <div class="col-sm-4">
                                <input type="text" class="form-control" name="codigoPostal" id="codigoPostal" v-model="form.codigoPostal">
                            </div>
                            <br>
                        <label for="" class="control-label col-sm-2">Genero</label>
                            <div class="col-sm-4">
                                <input type="text" class="form-control" name="genero" id="genero" v-model="form.genero">
                            </div>
                            <br>
                        <label for="" class="control-label col-sm-2">Telefono</label>
                            <div class="col-sm-4">
                                <input type="text" class="form-control" name="telefono" id="telefono" v-model="form.telefono">
                            </div>
                            <br>
                        <label for="" class="control-label col-sm-2">Fecha de nacimiento</label>
                            <div class="col-sm-4">
                                <input type="text" class="form-control" name="fechaNacimiento" id="fechaNacimiento" v-model="form.fechaNacimiento">
                            </div>
                    </div>
                    <br><br>
                    <div  class="d-flex justify-content-around ">
                        <button type="button" class="btn btn-primary" v-on:click="editar()">Editar</button>
                        <button type="button" class="btn btn-danger">Eliminar</button>
                        <button type="button" class="btn btn-dark" v-on:click="salir()">Salir</button>
                    </div>

                </form>
            </div>   
        <Footer />
    </div>

</template>

<script>
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
import axios from 'axios';
export default {
    name:"EditarView",
    components: {
        Header,
        Footer
    },
    data:function(){
       return{
            //pacienteId:null,
            form:{
                "pacienteId"        : "",
                "nombre"            : "", 
                "dni"               : "", 
                "correo"            : "", 
                "codigoPostal"      : "",
                "genero"            : "",
                "telefono"          : "",
                "fechaNacimiento"   : "",
                "token"             : "" 
            }
       } 
    },
    methods: {
        editar(){
            axios.put("https://api.solodata.es/pacientes",this.form)
            .then( data =>{
                console.log(data)
            })
        },
        salir(){
            this.$router.push("/dashboard");
        }
    },
    mounted:function() {
        this.form.pacienteId = this.$route.params.id;
        //console.log(this.pacienteId);
        axios.get("https://api.solodata.es/pacientes?id="+ this.form.pacienteId)
        .then(datos => {
            //console.log(datos)
            this.form.nombre = datos.data[0].Nombre;
            this.form.dni = datos.data[0].DNI;
            this.form.correo = datos.data[0].Correo;
            this.form.codigoPostal = datos.data[0].CodigoPostal;
            this.form.genero = datos.data[0].Genero;
            this.form.Telefono = datos.data[0].Telefono;
            this.form.fechaNacimiento = datos.data[0].FechaNacimiento;
            this.form.token = localStorage.getItem("token");
            console.log(this.form);
        })

    },
}
</script>

<style scoped>
.left{
    text-align: left ;
}
</style>
