<template>
<div class="calculator">

    <div class="display">
        <p class="main">{{main || '0'}}</p>
        <p class="secondary" v-if="showSecondary">{{secondary || '0'}}</p>
    </div>

    <div class="first-row">
        <div class="btn" @click="clear">C</div>
        <div class="btn" @click="percent">%</div>
        <div class="yellow-btn" @click="makeOperation($event)">÷</div>
    </div>

    <div class="second-row">
        <div class="btn" @click="type($event)">7</div>
        <div class="btn" @click="type($event)">8</div>
        <div class="btn" @click="type($event)">9</div>
        <div class="yellow-btn" @click="makeOperation($event)">x</div>
    </div>

    <div class="third-row">
        <div class="btn" @click="type($event)">4</div>
        <div class="btn" @click="type($event)">5</div>
        <div class="btn" @click="type($event)">6</div>
        <div class="yellow-btn" @click="makeOperation($event)">-</div>
    </div>

    <div class="fourth-row">
        <div class="btn" @click="type($event)">1</div>
        <div class="btn" @click="type($event)">2</div>
        <div class="btn" @click="type($event)">3</div>
        <div class="yellow-btn" @click="makeOperation($event)">+</div>
    </div>

    <div class="fifth-row">
        <div class="btn" @click="type($event)">0</div>
        <div class="btn" @click="dot">.</div>
        <div class="yellow-btn" @click="equals">=</div>
    </div>

</div>
</template>

<script>
export default {
name: 'Calculator',

data() {
return {
main: '',
secondary: '',
showSecondary: false,
operation: '', //Defining Type of Operation
equalsStatus: false,
}
},

methods: {

// Clear Fields
clear() {
this.main = '';
this.secondary = ''
},

// Type numbers
type(e) {
this.main += e.target.innerHTML;
let regex = this.main.match(/[0-9]+/g);
this.showSecondary = false;
this.secondary = this.getSum(regex);
console.log(regex);
// this.secondary = this.main;
},

getSum(arr) {
let sum = 0;
for(let i = 0; i < arr.length; i++) {
sum += arr[i];
}
return sum;
},

// Making sure dot is added only once
dot() {
if(!this.main.includes('.')) {
this.main += '.';
}
},

// Getting percentages of a current number
// parseFloat - recieves a string and returns decimal with a dot
percent() {
if(!this.main.includes('%')) {
this.main += '%';
this.showSecondary = true;
this.secondary = `${parseFloat(this.main) / 100}`; // Return back the string
}
},

makeOperation(e) {
let sign = e.target.innerHTML.toString();
// this.operation = sign;
if(!this.main.includes(sign)){
this.main += sign;
}
},


addition() {
},


equals() {
this.equalsStatus = true; // Meaning Equals Button was clicked
this.showSecondary = true; // Show Secondary Display
this.secondary = this.main;
},





},

}
</script>

<style>

.calculator{
display: flex;
flex-direction: column;
width: 30vw;
margin: 20px auto;
font-size: 1.5rem;
}

.display{
background: rgb(31, 30, 30);
color: #fff;
height: 20vh;
display: flex;
flex-direction: column;
}

.display{
font-size: 1.2rem;
}

.secondary{
color: gray;
}

.first-row, .second-row, .third-row, .fourth-row, .fifth-row{
display: flex;
flex-direction: row;
}

.btn{
background: rgb(240, 236, 236);
padding: 20px;
width: 20vw;
border: 1px solid rgb(80, 80, 80);
cursor: pointer;
}

.btn:hover{
background: #fff;
}

.yellow-btn{
background: orange;
color: #fff;
padding: 20px;
border: 1px solid rgb(80, 80, 80);
cursor: pointer;
width: 20vw;
}

</style>
