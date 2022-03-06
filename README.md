# [![npm](https://img.shields.io/npm/dt/vue2-autocomplete-input-tag.svg)]() [![npm](https://img.shields.io/npm/v/vue2-autocomplete-input-tag.svg)]() [![npm](https://img.shields.io/npm/l/vue2-autocomplete-input-tag.svg)]()

## vue2-autocomplete-input-tag

With this library you can search items in an array and select the desired value through an input. 
<br />
This library works with <b>vue 2</b>. If you use vue 3, you can use my another library exclusive to this
<br />
version:: https://www.npmjs.com/package/vue-autocomplete-input-tag

npm install vue2-autocomplete-input-tag

## Usage
```html
<template>
  <div>
     <autocomplete 
        v-model="test"
        :items="items"
     />
  </div>
</template>

<script>
  import autocomplete from 'vue2-autocomplete-input-tag'
  export default {
    name: "App",
    components: {
      autocomplete,
    },
    data() {
      return {
        test: "",
        items: [
          "Banana",
          "Strawberry",
          "Orange",
          "Lemon",
          "Pineapple",
          "Watermelon",
          "Melon",
        ],
      };
    },
  };
</script>
```

## Attrs
```
You can pass attributes to input, like disabled and class
```
```html
<template>
  <div>
     <autocomplete 
        v-model="test" 
        :items="items" 
        disabled
        class="my-custom-class"
     />
  </div>
</template>
```


## Props
```html
<template>
  <div>
     <autocomplete 
        v-model="test" 
        :items="items" 
        permitArbitraryValues
        :returned="['id', 'name']" 
        displayed="name"
     />
  </div>
</template>
<script>
  import autocomplete from 'vue2-autocomplete-input-tag'
  
  export default {
    components: {
      autocomplete,
    },
    data() {
      return {
        test: {},
        items: [
          { name: "Banana", id: 1, color: "Yellow" },
          { name: "Strawberry", id: 2, color: "Red" },
          { name: "Orange", id: 3, color: "Orange" },
          { name: "Lemon", id: 4, color: "Green" },
          { name: "Pineapple", id: 5, color: "Yellow" },
          { name: "Watermelon", id: 6, color: "Red" },
          { name: "Melon", id: 7, color: "Yellow" },
        ],
      }
     }
</script>
```
<ul>
<li><h4>permitArbitraryValues:</h4> If the user does not select some option and the input lose focus, this prop permit the digited value. It's a Boolean prop, and the default value is false.</li>

<li><h4>displayed:</h4> With this prop you can pass an array of objects in "items" prop, and inform the displayed field. It's a String prop, and the default value is null. If you pass an array of objects and don't inform this prop, the autocomplete will not work correctly. </li>
  
<li><h4>returned:</h4> With this prop you can inform the returned value, when use an array of objects. You can inform a single string (It will return just this field), an array of strings (with the fields you want to return) or nothing (It will return all the properties from the object). Only inform this prop if items prop is an array of objects. </li>
</ul>

### How can I style my autocomplete?
The input can be styled like a single input. To style the results you can use .vue2-autocomplete-input-tag-items and .vue2-autocomplete-input-tag-item classes. 

A single example:
```css
  input {
    width: 100%;
    border: 1px solid #ccc;
    color: #666;
    border-radius: 10px;
    outline: none;
    padding: 9px 14px;
    box-sizing: border-box;
    font-size: 14px;
  }
  .vue2-autocomplete-input-tag-items {
    border: 1px solid #ccc;
    max-height: 200px;
    margin-top: 8px;
    width: 100%;
    background-color: white;
    border-radius: 8px;
    overflow: auto;
  }
  .vue2-autocomplete-input-tag-item {
    padding: 6px 16px;
    color: #4a4a4a;
    max-width: 100%;
    cursor: pointer;
    text-align: left;
    font-size: 14px;
  }
  .vue2-autocomplete-input-tag-item:hover {
    background-color: #e8e8e8;
  }
```
![example-vue-autocomplete-input-tag](https://user-images.githubusercontent.com/65973246/156936691-ca0f1187-2aa9-4770-8612-8b5b2efa8534.png)



### How does the reactivity works?
If you pass an array of strings (first example) the return will be just a string with the typed value, and when you select some option will be the selected value. 

If you pass an array of objects (second example), when you type, the returned value will be an object with "typed" property. And when you select some option, will return what you inform in "returned" prop. The typed property is returned because you can use @input and refresh the array.

### References
"Como criar e publicar uma biblioteca (em Vue) no npm?" -> https://medium.com/tableless/como-criar-e-publicar-uma-biblioteca-em-vue-no-npm-2dff8271ca7d
