<template>
    <div>{{contador}}</div>

    <button @click="incrementar">+1</button>
    <button @click="decrementar">-1</button>
</template>
<script>

import {ref} from 'vue'

export default {
    setup() {
        const contador = ref(0)
        const incrementar = ()=>{
            contador.value++
        }

        const decrementar = ()=>{
            contador.value--
        }

        return {
            contador,
            incrementar,
            decrementar
        }


    },
}
</script>