<template>
  <div>
    <div class="bg-gray-900 bg-opacity-50 dark:bg-opacity-80 fixed inset-0 z-40" />
    <div
        tabindex="-1"
        class="overflow-y-auto overflow-x-hidden fixed top-0 right-0 left-0 z-50 w-full md:inset-0 h-modal md:h-full justify-center items-center flex"
    >
      <div class="relative p-4 w-full h-full md:h-auto" :class="`${modalSizeClasses[size]}`">
        <!-- Modal content -->
        <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
          <!-- Modal header -->
          <div class="p-4 rounded-t flex justify-between items-center" :class="$slots.header ? 'border-b border-gray-200 dark:border-gray-600' : ''">
            <slot name="header" />
            <button @click="closeModal" type="button" class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 ml-auto inline-flex items-center dark:hover:bg-gray-600 dark:hover:text-white">
              <slot name="close-icon">
                <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
              </slot>
            </button>
          </div>
          <!-- Modal body -->
          <div class="p-6" :class="$slots.header ? '' : 'pt-0'">
            <slot name="body" />
          </div>
          <!-- Modal footer -->
          <div v-if="$slots.footer" class="p-6 rounded-b border-gray-200 border-t dark:border-gray-600">
            <slot name="footer" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts" setup>
import type { PropType } from 'vue'
import type { ModalSize, ModalPosition } from './types'

defineProps({
  children: {
    type: Array,
    default() {
      return []
    },
  },
  popup: {
    type: Boolean,
    default: false,
  },
  position: {
    type: String as PropType<ModalPosition>,
    default: 'center',
  },
  size: {
    type: String as PropType<ModalSize>,
    default: '2xl',
  },
})
const emit = defineEmits(['close'])
const modalSizeClasses = {
  xs: 'max-w-xs',
  sm: 'max-w-sm',
  md: 'max-w-md',
  lg: 'max-w-lg',
  xl: 'max-w-xl',
  '2xl': 'max-w-2xl',
  '3xl': 'max-w-3xl',
  '4xl': 'max-w-4xl',
  '5xl': 'max-w-5xl',
  '6xl': 'max-w-6xl',
  '7xl': 'max-w-7xl',
}

function closeModal() {
  emit('close')
}
</script>
