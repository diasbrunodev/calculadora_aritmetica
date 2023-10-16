<script setup>
import { reactive } from 'vue';

const object = reactive({
    number1: '',
    number2: '',
    operator: '',
    result: '',
});

const calculate = () => {

    //não consigo colocar esse if para funcionar
    if (isNaN(object.number1) || isNaN(object.number2)) {
        object.result = 'Insira um número válido.';

    } else {
        if (object.operator === "add") {
            object.result = parseFloat(object.number1) + parseFloat(object.number2);

        } else if (object.operator === "subtraction") {
            object.result = parseFloat(object.number1) - parseFloat(object.number2);

        } else if (object.operator === "multiplication") {
            object.result = parseFloat(object.number1) * parseFloat(object.number2);

        } else if (object.operator === "division") {
            if (parseFloat(object.number2) === 0) {
                object.result = 'Não é possível dividir por zero';
            } else {
                object.result = parseFloat(object.number1) / parseFloat(object.number2);
            }
        }
    }
};

</script>

<template>
    <body>
        <div class="container">

            <h1>Calculadora Aritmética</h1>

            <div class="fields">

                <h2>Selecione a opção aritmética</h2>

                <select id="operator" @change="e => object.operator = e.target.value" @click="calculate">
                    <option value=""></option>
                    <option value="add">➕</option>
                    <option value="subtraction">➖</option>
                    <option value="multiplication">✖️</option>
                    <option value="division">➗</option>
                </select>

                <div v-if="object.number1 === '' || object.number2 === ''">
                    <p style="color: red;">Por favor, preencha todos os campos.</p>
                </div>

                <div class="input-class">

                    <input type="number" id="number1" v-model="object.number1" @input="calculate">

                    <input type="number" id="number2" v-model="object.number2" @input="calculate">

                    <!-- só exibe o resultado se for um número válido, fazendo
    que não apareça na tela NaN caso não tenha nenhum valor válido-->
                    <div id="result" v-if="!isNaN(object.result)">
                        {{ object.result }}
                    </div>

                </div>


            </div>

        </div>
    </body>
</template>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: sans-serif;
}

h1 {
    margin: 20px;
}

h2 {
    margin-bottom: 20px;
}

.container {
    width: 400px;
    background-color: gray;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: flex;
    flex-direction: column;
    text-align: center;
    border-radius: 10px;
}

select {
    width: 50px;
}

.input-class {
    width: 50%;
    margin: 0 auto 30px;
}

input {
    display: block;
    text-align: right;
    width: 100%;
}

input,
select {
    height: 40px;
    border-radius: 10px;
    border: none;
    margin: 10px auto;
}

#result {
    font-size: 2em;
    font-weight: bold;
}</style>
