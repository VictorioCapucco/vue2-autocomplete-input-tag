<template>
  <div>
    {{ test }}
    <autocomplete
      v-model="test"
      :items="items"
      :returned="['id', 'color']"
      displayed="name"
      class="autocomplete-input"
    />
  </div>
</template>

<script>
  import autocomplete from "./components/autocomplete.vue";

  export default {
    name: "App",
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
      };
    },
  };
</script>
