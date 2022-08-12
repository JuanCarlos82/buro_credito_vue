<template>
    <div>
        <Header/>

            <div class="container">
                <table class="table table-hover">
                <thead>
                    <tr>
                        <th scope="col">ID</th>
                        <th scope="col">Nombre</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="departamento in Listadepartamento" :key="departamento.id" v-on:click="editar(departamento.id)">
                        <th scope="row">{{departamento.id}}</th>
                        <td>{{ departamento.nombre }}</td>
                        
                    </tr>
                  
                </tbody>
                </table>  

            </div>

        
    </div>
</template>

<script>
import Header from '@/components/HeaderView.vue'
import axios from 'axios';

export default {
    name: "ListView",
    data(){
        return{
            Listadepartamento:null,
        }
    },
    components: {
        Header,
        //Footer
    },
    
    mounted:function(){
       
        let direccion = "http://localhost:8000/departamentos/list"
        axios.get(direccion, {
            headers : {'Authorization': 'bearer'+ localStorage.getItem('token') }
        }).then(data =>{
            console.log(data)
            this.Listadepartamento = data.data
        })
    }
}

</script>