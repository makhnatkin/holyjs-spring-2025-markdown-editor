<script setup>
const props = defineProps({
  wysiwyg: { type: Boolean, required: true },
  offset: { type: Array},
  customStyle: { type: Object, default: () => ({ opacity: 0.8 }) },
  size: { type: String, default: undefined },
})

const positionStyle = {
  top: props.offset?.[0] ?? (props.wysiwyg ? '1.75rem' : '1.25rem'),
  right: props.offset?.[1] ?? (props.wysiwyg ? '2.5rem' : '3rem'),
  ...props.customStyle,
}
</script>

<template>
  <template v-if="wysiwyg">
    <div
        class="fixed z-50 pointer-events-none flex items-center justify-center"
        :style="positionStyle"
    >
      <gravity-ui-text
          :class="`opacity-50`"
          :style="`width: ${size ?? '2.2rem'}; height: ${size ?? '2.2rem'}`"
      />
    </div>
  </template>
  <template v-else>
    <div
        class="fixed z-50 pointer-events-none flex items-center justify-center"
        :style="positionStyle"
    >
      <gravity-ui-logo-markdown

          :class="`opacity-50`"
          :style="`width: ${size ?? '3rem'}; height: ${size ?? '3rem'}`"
      />
    </div>
  </template>
</template>