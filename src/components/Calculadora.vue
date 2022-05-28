<template>
  <div class="container mt-3">
        <h1>Calculadora Leche Bebé</h1>
        <div class="form-floating mb-3">
                <input id="floatingInput"  @keyup.enter="calcularLeche" class="form-control" placeholder="Ingresar" type="number" name="peso" v-model.number="peso" min="2500" max="10000">
                
                <label for="floatingInput">Ingrese el peso del bebé (gramos)</label>

        </div>
                <button class="btn btn-success btn-lg" @click="calcularLeche">Calcular</button>
                <div v-if="leche>0" class="mt-4">
                    <h2>Cantidad a tomar: <span class="badge bg-success">{{leche}} ml</span></h2>
                    <table class="table table-success table-striped mt-4">
                         <thead>
                            <tr>
                            
                                <th scope="col">Medida</th>
                                <th scope="col">N° Mamaderas</th>
                                <th scope="col">Total día</th>
                                <th scope="col">Diferencia</th>

                            </tr>
                        </thead>
                            
                    <tbody>
                        <tr v-for="med in medidas" :key="med.medida">
                            <td>{{med.medida}}</td>
                            <td>{{med.cantidad}}</td>
                            <td>{{med.total}} ml</td>
                            <td>{{med.faltante}} ml</td>
                        </tr>
                    </tbody>
                   
                    </table>
                </div>

  </div>
  
</template>

<script>

import Swal from 'sweetalert2'

export default {
    name: 'Calculadora',
    data(){
        return{
            peso: 2500,
            leche: 0,
            medidas:[]
        }
    },
    methods:{
        calcularLeche(){
            if(this.peso<2500 || this.peso>10000){
                this.leche = 0
                 Swal.fire({
                    icon: 'error',
                    title: 'Oops...',
                    text: 'El peso debe estar entre 2500 y 10000 gr'
                    })
                return
            }
            this.leche = Math.round(this.peso*74/450)
            this.calcularMedidas()
        },
        calcularMedidas(){

            let salida=[];

            const medidas=[30,50,60,80,90,110,120,150,180,200,250,500];

            medidas.forEach(ml => {
                

                const cantidad = Math.round(this.leche/ml)

                if(cantidad<=10 && cantidad>1){
                    salida.push({
                        medida:`${ml} ml`,
                        cantidad,
                        total:ml*cantidad,
                        faltante: this.leche - ml*cantidad 
                    })
                }
            });
            this.medidas = salida
        }
    }
}
</script>

<style>

</style>