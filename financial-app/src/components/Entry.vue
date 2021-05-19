<template>

<div>
    <label for="name">Nome:</label>
    <input id="cadastreName" name="name" type="text" v-model="data.name">
    <label for="value">Valor:</label>
    <input name="value" type="number" v-model="data.value">
    <select v-model="data.type">
        <option value="1">Entrada</option>
        <option value="2">Saída</option>
    </select>
    <button @click="cadastre">Cadastrar</button>
</div>
    
</template>


<script>
import {reactive, ref} from "vue";

export default {
    setup(props, context) {
        const data = reactive({
            name: "",
            value: "",
            type: 2
        });

        function cadastre(){
            context.emit("cadastre", {data:{name: data.name, value: data.value}, type: data.type});
            data.name = "";
            data.value = "";
            document.getElementById("cadastreName").focus();;
        }

        return{
            data,
            cadastre
        }
    },
}
</script>

<style lang="stylus" scoped>

</style>