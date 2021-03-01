<template>
<div class="calculator">

    <div class="display">
        
        <!-- Top Display -->
        <div class="calculation">
        <p class="right" v-if="showMain">{{right}}</p>
        <p>{{ operation || ''}}</p>
        <p class="left" v-if="showMain">{{left || 0}}</p>
        </div>
        
        <!-- Bottom Display -->
        <p class="secondary-muted" 
        v-if="showSecondary" :class="{'secondary-normal' : equalsStatus}"
        >{{secondary || '0'}}</p>


    </div>

    <div class="first-row">
        <div class="btn clear" @click="clear">C</div>
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

// Restart Calculator's Values
clear() {
// Clear Top Display (both parts)    
this.left = '';
this.right = '';

//Clear Bottom Display
this.secondary = '';
//Hide Bottom Display
this.showSecondary = false;
//Show Top Display
this.showMain = true;
//Clear Opearation type
this.operation = '';
//Clear Equals Status
this.equalsStatus = false; 
},


// Type numbers
type(e) {
 if(this.equalsStatus) { //If equals buttons has been clicked
 this.clear(); //Wipe out data
 }   
 if(this.operation === '') { // Until operation has been defined
 this.left += e.target.innerHTML; // Add numbers to left display
 }
 else { //When the operation has been declared
 this.right += e.target.innerHTML; // Add numbers to right display
 this.showSecondary = true; // Show bottom display when right display has values
 this.secondary = this.setOperation(parseInt(this.left), parseInt(this.right)); //Make calculations in the bottom display
 }
},



// Making sure dot is added only once
dot() {    
if(!this.left.includes('.')) { //If left display already has a dot forbid others
this.left += '.';
}
if(this.showSecondary && !this.right.includes('.')) { //If right display is shown and already has a dot forbid others
this.right += '.';
}
},

// Getting percentages of a current number
// parseFloat - recieves a string and returns decimal with a dot
percent() {
if(!this.left.includes('%')) {
this.left += '%';
this.showSecondary = true;
this.secondary = `${parseFloat(this.left) / 100}`; // Return back the string
} if(this.left === '0') {
this.left = '0';    
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
// this.secondary = this.setOperation(this.left, this.right); 
this.equalsStatus = true;
this.showMain = false;
this.operation = '';
this.left = this.secondary;
},





},

}
</script>

<style>

.calculator{
display: flex;
flex-direction: column;
width: 28vw;
margin: 20px auto;
font-size: 1.5rem;
}

.display{
display: flex;
flex-direction: column;    
background: rgb(31, 30, 30);
color: #fff;
height: 20vh;
font-size: 1.7rem;
padding-right: 1rem;
}

.calculation{
display: flex;
flex-direction: row-reverse;
}

.secondary-muted{
color: gray;
padding-left: 25vw;
}

.secondary-normal{
color: #fff;
padding-left: 25vw;
padding-bottom: 5px;
}

.first-row, .second-row, .third-row, .fourth-row, .fifth-row{
display: flex;
flex-direction: row;
}

.first-row .clear{
padding: 1em 4.8vw;      
}

.fifth-row .yellow-btn{
padding: 1em 4.8vw;    
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
