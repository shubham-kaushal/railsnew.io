<template>
  <li
    class="hover:bg-yellow-100"
    :style="selectedItem === itemName ? 'background-color: #F7FAFC;' : ''"
    @click="updateRadioButtonState"
  >
    <div class="flex items-center px-4 py-2 sm:px-6">
      <div class="min-w-0 flex-1 flex items-center">
        <div class="flex-shrink-0">
          <slot></slot>
        </div>
        <div class="min-w-0 flex-1 px-4 md:grid md:gap-4 ">
          <div>
            <div class="text-sm leading-5 font-medium text-indigo-600 truncate">
              {{ itemName }}
            </div>
            <div
              class="mt-2 flex items-center text-sm leading-5 text-gray-500 max-w-lg truncate pr-10"
            >
              <span>{{ description }}</span>
            </div>
          </div>
          <div class="hidden md:block"></div>
        </div>
      </div>
      <div>
        <input
          :id="itemName"
          v-model="selectedItem"
          type="radio"
          :name="group"
          :value="itemName"
          :disabled="itemName === 'Minitest' || itemName === 'RSpec'"
          class="form-radio h-4 w-4 text-indigo-600 transition duration-150 ease-in-out"
        />
      </div>
    </div>
  </li>
</template>

<script>
import eventBus from '@/eventBus.js'

export default {
  props: {
    itemName: {
      type: String,
      default: ''
    },
    description: {
      type: String,
      default: ''
    },
    group: {
      type: String,
      default: ''
    },
    selectedItem: {
      type: String,
      default: ''
    }
  },
  methods: {
    updateRadioButtonState(event) {
      eventBus.$emit('radioButtonUpdated', this.itemName)
    }
  }
}
</script>
