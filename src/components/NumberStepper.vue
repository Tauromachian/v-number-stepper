<template>
  <div>
    <label v-if="label" class="pl-0">
      {{ label }}
    </label>

    <div class="flex">
      <v-btn v-ripple icon color="primary" class="mt-0" @click="decreaseValue">
        <v-icon>
          mdi-minus
        </v-icon>
      </v-btn>

      <v-text-field
        v-if="showNumber"
        v-model.number="selection"
        :disabled="allowNumberEditing"
        single-line
        filled
        dense
        @blur="checkNumber"
      />

      <v-btn icon color="primary" class="mt-0" @click="increaseValue">
        <v-icon>
          mdi-plus
        </v-icon>
      </v-btn>
    </div>
  </div>
</template>

<script>
import { VBtn, VTextField, VIcon } from 'vuetify/lib';


export default {
  name: 'NumberStepper',
  components: {
    VBtn, VTextField, VIcon
  },

  props: {
    value: { type: [String, Number], default: 0 },
    label: { type: String, default: '' },
    showNumber: Boolean,
    allowNumberEditing: Boolean,
    min: {
      type: Number,
      default: 0
    },
    max: {
      type: Number,
      default: 10
    }
  },
  data () {
    return {
      selection: this.min
    }
  },
  computed: {
    selectionComputed () {
      if (this.notNumber(this.value)) {
        return this.min
      }
      if (this.value > this.max) {
        return this.max
      }
      if (this.value < this.min) {
        return this.min
      }
      return this.value
    }
  },
  watch: {
    selectionComputed (value) {
      this.selection = value
    },
    selection (value) {
      this.$emit('input', value)
    }
  },
  methods: {
    decreaseValue: function () {
      if (this.selection > this.min) {
        this.selection = this.selection - 1
      }
    },
    increaseValue: function () {
      if (this.selection < this.max) {
        this.selection = this.selection + 1
      }
    },
    notNumber (val) {
      return typeof val !== 'number'
    },
    checkNumber () {
      if (this.value > this.max) {
        this.selection = this.max
      }
      if (this.value < this.min) {
        this.selection = this.min
      }
      if (this.notNumber(this.selection)) {
        this.selection = this.min
      }
    }
  }
}
</script>

<style scoped>
    .flex{
        display:flex;
    }
</style>
