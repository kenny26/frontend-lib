<template>
  <label
    class="i-checkbox"
    :class="classes"
  >
    <span
      class="i-checkbox-input"
      :class="inputCheckboxClasses"
    >
      <input
        type="checkbox"
        name="checkbox"
        :value="value"
        :checked="value"
        @input="onInput"
      />
      <ic-check class="i-checkbox-icon" />
    </span>

    <slot>
      <span>{{ label }}</span>
    </slot>
  </label>
</template>

<script>
import IcCheck from '@/icons/ic-check.vue';

export default {
  name: 'ICheckbox',
  components: {
    IcCheck,
  },
  props: {
    value: Boolean,
    label: {
      type: String,
      default: '',
    },
    inputCheckboxClasses: {
      type: String,
      default: '',
    },
    invalid: Boolean,
  },
  computed: {
    classes() {
      return {
        checked: this.value,
        invalid: this.invalid,
      };
    },
  },
  methods: {
    onInput() {
      this.$emit('input', this.value === false);
    },
  },
};
</script>

<style>
.i-checkbox {
  z-index: 1;

  @apply flex items-center cursor-pointer m-0 relative;

  .i-checkbox-input {
    @apply w-4 h-4 flex items-center justify-center;
    @apply border border-gray-900 rounded-sm mr-4 bg-white;

    .i-checkbox-icon {
      @apply opacity-0 text-white;
    }

    input[type="checkbox"] {
      @apply hidden;

      &:checked {
        + .i-checkbox-icon {
          @apply opacity-100;
        }
      }
    }

    &:before {
      content: '';
      position: absolute;
      width: 16px;
      height: 16px;
      border-radius: 50%;
      background-color: transparent;
      opacity: 0;
      z-index: -1;
      box-shadow: 0px 0px 0px 8px rgba(0, 0, 0, .6);
    }
  }

  &.checked .i-checkbox-input {
    @apply bg-gray-900;
  }
  &.invalid .i-checkbox-input {
    @apply border-red-400;
  }

  &:hover .i-checkbox-input:before {
    opacity: 0.2;
  }
}
</style>
