<template>
  <div>
    <h1>Attractions</h1>
    {{ item.name }}
    {{ item.detail }}
    <img :src="item.coverimage" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
const route = useRoute()
const id = ref('')
id.value = route.params.id

const item = ref('')
await fetch('https://www.melivecode.com/api/attractions/1')
  .then(res => res.json())
  .then((result) => {
    item.value = result.attraction
})

useHead({
  title: item.value.name,
  meta: [
    { name: item.value.name, content: item.value.detail },
    { hid: 'og-title', property: 'og:title', content: item.value.name },
    { hid: 'og:description', property: 'og:description', content: item.value.detail },
    { hid: 'og:image', property: 'og:image', content: item.value.coverimage },
  ]
})
</script>