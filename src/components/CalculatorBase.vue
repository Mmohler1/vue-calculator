<template>

    {{ calculatorItems }}

    <div class="container">
        <div class="row">
            <div class="col calc-btn btn" @click="addNode(operations.FIRST_PARENTHESIS)">&#40;</div>
            <div class="col calc-btn btn" @click="addNode(operations.LAST_PARENTHESIS)">&#41;</div>
            <div class="col calc-btn btn" @click="addNode(operations.PERCENT)">%</div>
            <div class="col calc-btn btn" @click="clearCalculator()">AC</div>
        </div>
        <div class="row">
            <div class="col calc-btn btn" @click="addNode('7')">7</div>
            <div class="col calc-btn btn" @click="addNode('8')">8</div>
            <div class="col calc-btn btn" @click="addNode('9')">9</div>
            <div class="col calc-btn btn" @click="addNode(operations.DIVIDE)">&#247;</div>
        </div>
        <div class="row">
            <div class="col calc-btn btn" @click="addNode('4')">4</div>
            <div class="col calc-btn btn" @click="addNode('5')">5</div>
            <div class="col calc-btn btn" @click="addNode('6')">6</div>
            <div class="col calc-btn btn" @click="addNode(operations.MULTIPLY)">&#10005;</div>
        </div>
        <div class="row">
            <div class="col calc-btn btn" @click="addNode('1')">1</div>
            <div class="col calc-btn btn" @click="addNode('2')">2</div>
            <div class="col calc-btn btn" @click="addNode('3')">3</div>
            <div class="col calc-btn btn" @click="addNode(operations.MINUS)">-</div>
        </div>
        <div class="row">
            <div class="col calc-btn btn" @click="addNode('0')">0</div>
            <div class="col calc-btn btn" @click="addNode('point')">.</div>
            <div class="col calc-btn btn" @click="calculate()">=</div>
            <div class="col calc-btn btn" @click="addNode(operations.PLUS)">+</div>
        </div>
    </div>

    <div> Display: {{ calculatorDisplay }}</div>

    <div> Result: {{ calculateResult }}</div>
</template>

<script setup lang="ts">
import { Ref, ref } from 'vue';

//Idea write out the calc in an array, like a node. Then create a method which counts it down.
enum operations {
  PLUS = "plus",
  MINUS = "minus",
  MULTIPLY = "multiply",
  DIVIDE = "divide",
  PERCENT = "percent",
  FIRST_PARENTHESIS = "firstP",
  LAST_PARENTHESIS  = "lastP"
}

const calculatorItems: Ref<string[]> = ref([]);
const calculatorDisplay: Ref<string> = ref("");
const calculateResult: Ref<number> = ref(0);



function addNode(node: string) {
    const lastNodeNumber = (calculatorItems.value.length - 1); 
    console.log("LastNodeNumber: ", lastNodeNumber)    
    if (lastNodeNumber >= 0) {
        if(!isNaN(Number(calculatorItems.value[lastNodeNumber])) && !isNaN(Number(node))) {
            let addNumber =  (Number(calculatorItems.value[lastNodeNumber]) == 0) ?
            node :
            calculatorItems.value[lastNodeNumber] + node;
            
            console.log("addNumber: ", addNumber)
            calculatorItems.value.pop(); 
            calculatorItems.value.push(addNumber);
        } else if(isNaN(Number(calculatorItems.value[lastNodeNumber])) && isNaN(Number(node))) {
            
        } else {
            calculatorItems.value.push(node);
        }
    } else {
        calculatorItems.value.push(node);
    }     
    displayCalculation() 
}

//Clears the 
function clearCalculator() {
    calculatorItems.value = [];
    calculatorDisplay.value = "";
}

function calculate() {
    console.log("todo")
}

function displayCalculation() {
    let display = "";
    for(const item of calculatorItems.value) {

        //Need to change this so I know what is an enum and what is a number
        if (isNaN(Number(item))) {
            let operation = "";
            if (item == operations.PLUS) {
                operation = " + "
            } else if (item == operations.PERCENT) {
                operation = " % "
            } else if (item == operations.MULTIPLY) {
                operation = " X "
            } else if (item == operations.MINUS) {
                operation = " - "
            } else if (item == operations.LAST_PARENTHESIS) {
                operation = " ) "
            } else if (item == operations.FIRST_PARENTHESIS) {
                operation = " ( "
            } else if (item == operations.DIVIDE) {
                operation = " / "
            }
            display = display + operation;
        } else {
            display = display + " " + item;
        }    
    }
    calculatorDisplay.value = display;
}

</script>






<style scoped>
.calc-container {
    background-color: blue;
}
.calc-base {
    background: lime;
}

.calc-btn {
    background-color: lime;
    padding: 10px;
    width: 50px;
    height: 50px;
    border: black solid 1px;
}
</style>