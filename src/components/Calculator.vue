<template>
<div class="calculator">

    <div class="display">
        <p class="top" v-if="displayTop">{{top || '0'}}</p>
        <p class="bottom">{{bottom || '0'}}</p>
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
top: '',
bottom: '',
displayTop: false,
operation: '', //Defining Type of Operation
}
},

methods: {

// Clear Fields
clear() {
this.top = '';
this.bottom = ''
},

// Type numbers
type(e) {
this.bottom += e.target.innerHTML;
},

// Making sure dot is added only once
dot() {
if(!this.bottom.includes('.')) {
this.bottom += '.';
}
},

// Getting percentages of a current number
// parseFloat - recieves a string and returns decimal with a dot
percent() {
this.current = `${parseFloat(this.current) / 100}`; // Return back the string
},

makeOperation(e) {
let operationType = e.target.innerHTML.toString();
this.operation = operationType;

this.displayTop = true;
this.top = this.bottom + operationType;
},

equals() {
// 5+5=10=    
// 5+5=10=15= 
this.top += this.bottom + '='; // 5+5= 
this.bottom = parseInt(this.bottom) + parseInt(this.top);
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

.display .top{
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
