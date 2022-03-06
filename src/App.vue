<template>
  <div>
    {{ test }}
    <autocomplete v-model="test" :items="items" class="autocomplete-input" />
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
