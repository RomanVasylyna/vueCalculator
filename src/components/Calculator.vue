<template>
<div class="calculator">

    <div class="display">
        <p class="current">{{current || '0'}}</p>
        <p class="next" v-if="showNext">{{next || '0'}}</p>
    </div>

    <div class="first-row">
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="percent">%</div>
    <div class="yellow-btn" @click="operation($event)">÷</div>
    </div>

    <div class="second-row">
    <div class="btn" @click="type($event)">7</div>
    <div class="btn" @click="type($event)">8</div>
    <div class="btn" @click="type($event)">9</div>
    <div class="yellow-btn" @click="operation($event)">x</div>
    </div>

    <div class="third-row">
    <div class="btn" @click="type($event)">4</div>
    <div class="btn" @click="type($event)">5</div>
    <div class="btn" @click="type($event)">6</div>
    <div class="yellow-btn" @click="operation($event)">-</div>
    </div>

    <div class="fourth-row">
    <div class="btn" @click="type($event)">1</div>
    <div class="btn" @click="type($event)">2</div>
    <div class="btn" @click="type($event)">3</div>
    <div class="yellow-btn" @click="operation($event)">+</div>
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
current: '',
next: '',
showNext: false,
operationType: '',
// equalStatus: false
}
},

methods: {

// Clear Fields
clear() {
this.current = '';
this.next = ''
},

// Type numbers
type(e) {
this.current += e.target.innerHTML;
},

// Making sure dot is added only once
dot() {
if(!this.current.includes('.')) {
this.current += '.';
}
},

// Getting percentages of a current number
// parseFloat - recieves a string and returns decimal with a dot
percent() {
this.current = `${parseFloat(this.current) / 100}`; // Return back the string
},

operation(e) {

// Defining Operation Type
const type = e.target.innerHTML.toString();

// Remove Operands Duplicates
this.removeDuplicates(type);


},

// Remove Operands Duplicates
removeDuplicates(type) {
if(!this.current.includes(type)) {
this.operationType = type;
this.next = this.current;
this.current += this.operationType;
}
},

calculate() {
this.showNext = true; // Show the display below
this.next = parseInt(this.current + this.next); // sdfsdf
},

equals() {
// this.equalStatus = true;

// Validation for operand existance
if(this.operationType !== '' && this.current.includes(this.operationType)) {
this.calculate();
}
}




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

.display .current{
font-size: 14px;
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