<script setup>
  import { useDarkMode } from '@slidev/client'
  import { onMounted, watchEffect } from 'vue'
  const { isDark } = useDarkMode()

  onMounted(() => {
    document.body.classList.add('g-root')
    if (isDark.value) {
      document.body.classList.add('g-root_theme_dark')
    } else {
      document.body.classList.add('g-root_theme_light')
    }
  })

  watchEffect(() => {
    if (isDark.value) {
      document.body.classList.remove('g-root_theme_light')
      document.body.classList.add('g-root_theme_dark')
    } else {
      document.body.classList.remove('g-root_theme_dark')
      document.body.classList.add('g-root_theme_light')
    }
  })
</script>