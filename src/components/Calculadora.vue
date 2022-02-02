<template>
  <div class="container mt-3">
        <h1>Calculadora Leche Bebé</h1>
        <div class="form-floating mb-3">
                <input id="floatingInput" class="form-control" placeholder="Ingresar" type="number" name="peso" v-model="peso" min="2000" max="15000">
                
                <label for="floatingInput">Ingrese el peso del bebé (gramos)</label>

        </div>
                <button class="btn btn-success btn-lg" @click="calcularLeche">Calcular</button>
                <div v-if="leche>0" class="mt-4">
                    <h2>Cantidad a tomar: <span class="badge bg-success">{{leche}} ml</span></h2>
                    <table class="table table-success table-striped mt-4">
                         <thead>
                            <tr>
                            
                                <th scope="col">Medida</th>
                                <th scope="col">Medidas diarias</th>
                                <th scope="col">Total día</th>
                                <th scope="col">Faltante</th>

                            </tr>
                        </thead>
                            
                    <tbody>
                        <tr v-for="med in medidas" :key="med.medida">
                            <td>{{med.medida}}</td>
                            <td>{{med.cantidad}} medidas</td>
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
            this.leche = Math.floor(this.peso*74/450)
            this.calcularMedidas()
        },
        calcularMedidas(){
            const med60 = Math.floor(this.leche / 60)
            const med90 = Math.floor(this.leche / 90)
            const med120 = Math.floor(this.leche / 120)

            this.medidas = [
                {
                    medida:'60 ml',
                    cantidad: med60,
                    total:60*med60,
                    faltante: this.leche - 60*med60 
                },
                {
                    medida:'90 ml',
                    cantidad: med90,
                    total:90*med90,
                    faltante: this.leche - 90*med90  
                },
                {
                    medida:'120 ml',
                    cantidad: med120,
                    total:120*med120,
                    faltante: this.leche - 120*med120  
                }   
            ]
        }
    }
}
</script>

<style>

</style>