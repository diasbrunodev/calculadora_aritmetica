<script setup>
import { reactive } from 'vue';

const object = reactive({
    number1: '',
    number2: '',
    operator: '',
    result: '',
});

const calculate = () => {

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
    <div class="container">

        <header>
            <h1>Calculadora Aritmética</h1>
        </header>

        <div class="fields">

            <input type="number" id="number1" @input="e => object.number1 = e.target.value">

            <input type="number" id="number2" @input="e => object.number2 = e.target.value">

            <select id="operator" @change="e => object.operator = e.target.value" @click="calculate">
                <option value="add">+</option>
                <option value="subtraction">-</option>
                <option value="multiplication">*</option>
                <option value="division">:</option>
            </select>

            <div id="result">
                {{ object.result }}
            </div>

        </div>

    </div>
</template>

<style scoped></style>
