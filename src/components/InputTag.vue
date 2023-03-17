
<script setup>
    import { ref } from 'vue';

    const newTag = ref("");
    const currentValue = ref("");
    const tags = ref([]);

    const add = (valor) => {
        
        // que no se repita
        //const exist = tags.value.some(palabra => { palabra.value == valor });
        const exist = tags.value.indexOf(valor);

        //console.log(exist);

        if (valor !== '' && exist == -1) {

            tags.value.push(currentValue.value);
            currentValue.value = "";
        } else {
            //console.log("Vacío, o ya existe la etiqueta");
        }

    };

    /* newTag.value = "hola";  */   

    const handleKeyDown = (tecla) => {

        // que no se repita
        const exist = tags.value.indexOf(currentValue.value);

        //  borrar ultimo elemento si seguimos borrando en el input
        if (tecla.key === "Backspace" && currentValue.value == "") {
            tags.value.pop();
        }

        if (tecla.key === "Enter" && currentValue.value !== '' && exist == -1) {

            tags.value.push(currentValue.value);
            /* console.log(tags.value); */
            currentValue.value = "";
            
        } else {
            //console.log("Vacío, o ya existe la etiqueta");
        }
    };

    const conEnter = (valor) => {
        //console.log(valor);
    }

    const borrar = (id) => {
        tags.value.splice(id, 1);
        /* console.log(id);
        console.log(tags.value); */
    }

</script>

<template>

    <div class="input-tag">
        <div class="tags" >
            <div class="item" v-for="(tag, index) in tags" :key="index"> 
                {{ tag }} 
                <button @click="borrar(index)">X</button>
            </div>    
        </div>
        <form v-on:submit.prevent="conEnter('enviado por form')">
            <input type="text" name="newTag" id="newTag" :autofocus="true" v-model.trim="currentValue" @keydown="handleKeyDown">
            <button @click="add(currentValue)">agregar</button>
        </form>

    </div>

    <!-- <span>{{newTag}}</span> -->

</template>

<style scoped>

    .input-tag {
        display: inline-flex;
        /* border: solid 1px var(--verde); */
        width: 80%;
        margin: 0 auto;
    }

    .tags {
        display: flex;
        flex-wrap: wrap;
        gap: 5px;
        justify-content: center;
        align-items: center;
        padding: 5px;
    }

    .item {
        border: 1px var(--verde) solid;
        border-radius: 10px;
        padding: 10px;

        display: flex;
        justify-content: space-around;
        align-items: center;

        gap: 3px;
        transition: background-color .5s ease-in-out;
    }

    .item:hover {
        background-color: var(--verde);
        color: black;
        text-shadow: 0px 0px 3px white;
    }

    input[type="text"] {
        padding: 20px;

        border: none;
        border-radius: 10px;
        outline: none;
        width: 100%;
    }

    .item button {
        background: none;
        cursor: pointer;

        transition: background-color .5s ease-in-out;
    }
    .item button:hover {
        background-color: var(--verde);
    }

    form button {
        cursor: pointer;
        border: 1px solid var(--verde);
        margin: 0 auto;
        border-radius: 10px;
        padding: 3px;
        background-color: transparent;
        color: white;
    }

    form button:hover {
        box-shadow: 0px 2px 5px var(--verde);
    }

    form {
        width: 50%;
        display: flex;
        flex-direction: column;
        align-items: center;

        gap: 10px;
    }

</style>