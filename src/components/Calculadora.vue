<template>
  <div class="container mt-3">
        <h1>Calculadora Leche Bebé</h1>
        <div class="form-floating mb-3">
                <input id="floatingInput"  @keyup.enter.="calcularLeche" class="form-control" placeholder="Ingresar" type="number" name="peso" v-model.number="peso" min="2000" max="15000">
                
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
export default {
    name: 'Calculadora',
    data(){
        return{
            peso: 3000,
            leche: 0,
            medidas:[]
        }
    },
    methods:{
        calcularLeche(){
            if(this.peso<2000 || this.peso>15000){
                this.leche = 0
                return
            }
            this.leche = Math.round(this.peso*74/450)
            this.calcularMedidas()
        },
        calcularMedidas(){

            let salida=[]
            for (let ml = 30; ml <= 120; ml = ml + 10) {
                const cantidad = Math.round(this.leche/ml)

                if( cantidad<=12){

                    salida.push({
                        medida:`${ml} ml`,
                        cantidad,
                        total:ml*cantidad,
                        faltante: this.leche - ml*cantidad 
                    })
                }

            }  

            this.medidas = salida
        }
    }
}
</script>

<style>

</style>