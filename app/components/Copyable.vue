<script setup lang="ts">
const props = withDefaults(defineProps<{ content: string, enableClipboard?: boolean }>(), { enableClipboard: false })

const { copy, isSupported } = useClipboard()

function copyAddress() {
  if (props.enableClipboard && isSupported.value) {
    copy(props.content)
  }
}
</script>

<template>
  <p
    text-neutral-800 text-12 font-semibold whitespace-nowrap lh-none tracking-wide p-4 rounded-4
    :class="{ 'hover:cursor-pointer hover:bg-neutral-200': enableClipboard }" @click="copyAddress"
  >
    <slot>
      {{ content }}
    </slot>
  </p>
</template>
