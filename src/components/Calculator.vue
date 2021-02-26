<template>
<div class="calculator">

    <div class="display">
        
        <!-- Top Display -->
        <div class="calculation">
        <p class="left" v-if="showMain">{{left || '0'}}</p>
        <p>{{ operation || ''}}</p>
        <p class="right" v-if="showMain">{{right}}</p>
        </div>
        
        <!-- Bottom Display -->
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
left: '',
right:'',
secondary: '',
showSecondary: false,
showMain: true,
operation: '', //Defining Type of Operation
equalsStatus: false,
}
},

methods: {

// Clear Fields
clear() {
this.left = '';
this.right = '';
this.secondary = '';
this.showSecondary = false;
this.showMain = true;
this.operation = '';
},


// Type numbers
type(e) {
if(this.operation === '') {
this.left += e.target.innerHTML;
} else {
 this.right += e.target.innerHTML; 
 this.showSecondary = true;
 this.secondary = this.setOperation(parseInt(this.left), parseInt(this.right));
}
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
if(!this.operation.includes(sign)){
this.operation = sign;
}
},

setOperation(a, b) {
if(this.operation == '+') {
return parseInt(a) + parseInt(b);   
} if(this.operation == '-') {
return parseInt(a) - parseInt(b);   
} if(this.operation == '÷') {
return parseInt(a) / parseInt(b);     
} if(this.operation == 'x') {
return parseInt(a) * parseInt(b);      
}
},

equals() {
this.secondary = this.setOperation(this.left, this.right); 
this.showMain = false;
this.operation = '';
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

.calculation{
display: flex;
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
