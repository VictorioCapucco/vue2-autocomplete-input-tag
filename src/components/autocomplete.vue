<template>
  <div>
    <input
      v-model="typed"
      v-bind="$attrs"
      @input="
        !openItems ? (openItems = true) : '',
          updateInput($event.target.value, false)
      "
      @focus="openItems = true"
      @blur="closeItems"
    />
    <div
      class="vue-autocomplete-input-tag-items"
      :style="`display: ${openItems ? 'grid' : 'none'};`"
    >
      <!-- Use @mousedown because @click occurs after @blur and make bugs -->
      <div
        v-for="(item, index) in filteredItems"
        :key="index"
        class="vue-autocomplete-input-tag-item"
        @mousedown="updateInput(item, true)"
      >
        {{ displayed != null ? item[displayed] : item }}
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    name: "Vue2AutocompleteInputTag",
    inheritAttrs: false,
    props: {
      items: {
        type: Array,
        default: () => {
          return [];
        },
      },
      permitArbitraryValues: {
        type: Boolean,
        default: false,
      },
      displayed: {
        type: String,
        default: null,
      },
      vue2: {
        type: Boolean,
        default: false,
      },
      returned: {
        default: null,
      },
      modelValue: {},
      value: {},
    },
    data() {
      return {
        openItems: false,
        typed: "",
      };
    },
    computed: {
      filteredItems() {
        if (this.displayed !== null)
          return this.items.filter((item) => {
            return item[this.displayed]
              .toString()
              .toLowerCase()
              .includes(this.typed.toLowerCase());
          });
        else
          return this.items.filter((item) => {
            return item
              .toString()
              .toLowerCase()
              .includes(this.typed.toLowerCase());
          });
      },
    },
    methods: {
      closeItems() {
        this.openItems = false;

        if (
          !this.permitArbitraryValues &&
          this.displayed === null &&
          this.returned === null
        ) {
          if (
            this.items.find((element) => this.modelValue === element) ===
            undefined
          )
            this.updateInput("", false);
        }
      },
      updateVModel(newValue) {
        this.$emit("input", newValue);
      },
      updateInput(value, clicked) {
        if (this.displayed !== null) {
          if (clicked) {
            this.typed = value[this.displayed];
            if (this.returned === null) this.updateVModel(value);
            else if (typeof this.returned === "string")
              this.updateVModel(value[this.returned]);
            else {
              const objectValue = {};
              for (let i = 0; i < this.returned.length; i++) {
                objectValue[this.returned[i]] = value[this.returned[i]];
              }
              this.updateVModel(objectValue);
            }
          } else this.updateVModel({ typed: this.typed });
        } else {
          this.updateVModel(value);
          this.typed = value;
        }
      },
    },
  };
</script>
