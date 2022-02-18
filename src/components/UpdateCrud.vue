<template>
    <div>
        <button v-on:click="modificar(id_estudiante)" >Modificar</button>
        <div v-show="evento">
            <!-- <form action=""> -->
                <table>
                    <tr>
                        <td>ID</td>
                        <td><span id="mod_id">{{ mod_id }}</span></td>
                    </tr>
                    <tr>
                        <td>Nombre(s)</td>
                        <td><input type="text"  id="mod_nombre" v-model="mod_nombre" /></td>
                     </tr>
                    <tr>
                        <td>Paterno</td>
                        <td><input type="text"  id="mod_paterno" v-model="mod_paterno"></td>
                     </tr>
                    <tr>
                        <td>Materno</td>
                         <td><input type="text"  id="mod_materno" v-model="mod_materno"></td>
                     </tr>
                    <tr>
                        <td>Género</td>
                        <td><input type="text"  id="mod_genero" v-model="mod_genero"></td>
                     </tr>
                    <tr>
                        <td>Nacionalidad</td>
                        <td><input type="text"  id="mod_nacionalidad" v-model="mod_nacionalidad"></td>
                    </tr>
                    <tr>
                        <td><button v-on:click="descartar(id_estudiante)">Descartar</button></td>
                        <td><button v-on:click="guardar(id_estudiante)">Guardar</button></td>
                    </tr>
                </table>
            <!-- </form> -->
        </div>
    </div>
    

</template>

<script>
import datosBD from "@/assets/datos.json";
import { stringify } from 'querystring';
export default {
    name: "Modificar",
    props:[
        "id_estudiante"
    ],
    data(){
        return{
            evento: false,
            mod_id: 0,
            mod_nombre: "",
            mod_paterno: "",
            mod_materno: "",
            mod_genero: "",
            mod_nacionalidad: "",
            registro: {}
        }
    },
    methods:{
        modificar: function(id){
            this.registro = datosBD.find( usuario => usuario.id === id );
            this.mod_id = this.registro.id;
            this.mod_nombre = this.registro.nombre;
            this.mod_paterno = this.registro.paterno;
            this.mod_materno = this.registro.materno;
            this.mod_genero = this.registro.genero;
            this.mod_nacionalidad = this.registro.nacionalidad;
            this.evento = true;

        },
        descartar: function(id){
            this.mod_id = id;
            this.mod_nombre = "";
            this.mod_paterno = "";
            this.mod_materno = "";
            this.mod_genero = "";
            this.mod_nacionalidad = "";
            this.evento = false;
        },
        guardar: function(id){

            this.registro = datosBD.find( usuario => usuario.id === id );
            this.registro.id = mod_id;
            this.registro.nombre = this.mod_nombre;
            this.registro.paterno = this.mod_paterno;
            this.registro.materno = this.mod_materno;
            this.registro.genero = this.mod_genero;
            this.registro.nacionalidad = this.mod_nacionalidad;
            datosBD = JSON.push(this.registro);
            fs = require('fs');
            file_name = '../assets/datos.json';
            file = require(file_name);

            fs.writeFileSync(file_name,stringify(datosBD))
            //datosBD.find( adicionar => adicionar.id === id )
            //alert(this.registro.nombre);
        }
        
    }
}
</script>
