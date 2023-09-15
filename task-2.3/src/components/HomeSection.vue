<!-- 3. Reactivity Fundamentals -->
<script setup>
import { ref, computed, reactive, watch  } from 'vue';
import Looping from './Looping.vue';


// 1. Template Syntax
// a. Text Interpolation
const message = 'Hello world';
// b. Raw HTML
const htmlTag = '<span style="color: blue">HTML Text</span>';
// c. Attribute Bindings
const bindedID = ref('bindedID');
// d. JavaScript Expressions
// 2. Methods
const buttonBool = ref(true);
const buttonPress = () => {
  buttonBool.value = !buttonBool.value;
}

// 4. Computed Properties
const fruits = ref(['apples', 'pears', 'bananas']);
const numberOfFruits = computed(() => {
  return fruits.value.length;
})

// 5. Class and Style Bindings
// a. Binding HTML class
const isRed = ref(false);
const addClassToButton = () => {
  isRed.value = !isRed.value
}
// b. Binding Inline Styles
const colour = ref('orange');
const fontSize = ref(20);

// 6. List Rendering
// a. v-for with an Object
const person = reactive({
  name: 'John Doe',
  age: 45,
  job: 'Author'
})

// 7. Event Handling
// a. Inline Handlers
const count = ref(0);
// b. Event Handlers
const addFive = () => {
  count.value = count.value + 5;
}

// 8. Form Input Bindings
const name = ref('');
const checked = ref(false);
const selectedFruit = ref('Apple')
const duties = ref('');
const lazyMessage = ref('');
const age = ref(0);
const trimmedMessage = ref('');

// 9. Watchers
const watchCount = ref(0);
watch(watchCount, (newWatchCount) => {
  if(newWatchCount > 5){
    console.log('5!')
  }
})

// 10. Components
const emitCount = ref(0);

const addToWatchCount = () => {
  watchCount.value++;
}


</script>



<template>
<!-- 1. Template Syntax -->
<h2>Template Syntax</h2>
<!-- a. Text Inerpolation -->
<p>{{ message }}</p>
<!-- b. Raw HTML -->
<p>Outputting raw HTML: <span v-html="htmlTag"></span></p>
<!-- c. Attribute Bindings -->
<p v-bind:id="bindedID">Binding an ID</p>
<!-- d. JavaScript Expressions -->
<button @click="buttonPress">{{ buttonBool ? 'ON' : 'OFF' }}</button>

<!-- 4. Computed Properties -->
<p>{{ numberOfFruits }}</p>
<button @click="fruits.splice(0, 1)">Eat a fruit</button>

<!-- 5. Class Style and Bindings -->
<h2>Class Style and Bindings</h2>
<!-- a. Binding HTML class -->
<button @click="addClassToButton" :class="{ bindedClass: isRed}">Click to bind</button>
<!-- b. Binding Inline Styles -->
<p :style="{color: colour, fontSize: fontSize + 'px'}">Binding inline styles</p>


<!-- 6. List Rendering -->
<h2>List Rendering</h2>
<!-- a. v-for with an Object -->
<ul>
  <li v-for="value in person">{{ value }}</li>
</ul>
<!-- b. v-for with a Range -->
<ul>
  <li v-for="n in 5">Entry number: {{ n }}</li>
</ul>
<!-- c. v-for on <template> -->
<ul>
  <template v-for="fruit in fruits">
    <li>{{ fruit }}</li>
    <li>Vegetable</li>
  </template>
</ul>
<!-- d. v-for with v-if -->
<ul>
    <li v-for="fruit in fruits" v-if="buttonBool">{{ fruit }}</li>
</ul>
<!-- e. v-for with a Component -->
<Looping v-for="(fruit, index) in fruits" :fruit="fruit" :key="index" />

<!-- 7. Event Handling -->
<h2>Event Handling</h2>
<!-- a. Inline Handlers -->
<button @click="count++">Click to add 1 to the count</button>
<div>
  <p>The current count is: {{ count }}</p>
</div>
<!-- b. Method Handlers -->
<button @click="addFive">Add 5 to the count</button>

<!-- 8. Form Input Bindings  -->
<h2>Form Input Bindings</h2>
<!-- a. v-model with input type text, check box, radio, select and textarea -->
<h3>Text</h3>
<p>My name is: {{ name }}</p>
<input v-model="name" placeholder="enter your name" />
<p>My job duties are: {{ duties }}</p>
<textarea v-model="duties" placeholder="enter your job duties"></textarea>
<br>
<p v-if="checked">Checked!</p>
<input type="checkbox" id="checkbox" v-model="checked" />

<p>Fruit selected: {{ selectedFruit }}</p>
<input type="radio" id="apple" value="Apple" v-model="selectedFruit" />
<label for="apple">Apple</label>
<input type="radio" id="banana" value="Banana" v-model="selectedFruit" />
<label for="banana">Banana</label>
<!-- b  v-model modifiers [.lazy , .number, .trim]-->
<p>This is a lazy message: {{ lazyMessage }}</p>
<input v-model.lazy="lazyMessage" />
<p>This is your age + 10: {{ age + 10 }}</p>
<input v-model.number="age" />
<br>
<p>This is a trimmed message: {{ trimmedMessage }}</p>
<input v-model.trim="trimmedMessage" />
<br>

<!-- 9. Watchers -->
<button @click="addToWatchCount">Add 1 to count</button>

<!-- 10. Components -->
<h2>Components</h2>
<!-- a. Props -->
<Looping :fruit="fruits[0]"/>
<!-- b. Events -->
<p>Message from the component: {{ emitCount }}</p>
<Looping :fruit="fruits[0]" @emitAdd="emitCount += 1"/>
<!-- c. Slots -->
<Looping :fruit="fruits[0]">Apples are my favourite</Looping>
</template>

<style scoped>
#bindedID{
  color: red;
}

.bindedClass{
  background-color: red;
}
</style>
