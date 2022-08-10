<template>
    <div>
        <Header />
            <div class="container">
                <form action="" class="form-horizontal">
                    <div class="form-group left">
                        <label for="" class="control-label col-sm-2">Nombre</label>
                            <div class="col-sm-10">
                                <input type="text" class="form-control" name="nombre" id="nombre">
                            
                            </div>
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
            pacienteId:null,
            form:{
                "nombre"            : "", 
                "dni"               : "", 
                "correo"            :"", 
                "codigoPostal"      :"",
                "genero"            : "",
                "telefono"          : "",
                "fechaNacimiento"   : "",
                "token"             : "" 
            }
       } 
    },
    mounted:function() {
        this.pacienteId = this.$route.params.id;
        //console.log(this.pacienteId);
        axios.get("https://api.solodata.es/pacientes?id="+ this.pacienteId)
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
