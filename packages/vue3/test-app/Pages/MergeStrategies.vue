<script setup lang="ts">
import { router } from '@inertiajs/vue3'
import { ref } from 'vue'

const props = defineProps<{
  foo: {
    data: { id: number; name: string }[]
    page: number
    per_page: number
    meta: { label: string }
  }
  bar: number[]
  baz: number[]
}>()

const page = ref(props.foo.page)

const reloadIt = () => {
  router.reload({
    data: {
      page: page.value,
    },
    only: ['foo', 'baz'],
    onSuccess(visit) {
      page.value = visit.props.foo.page
    },
  })
}

const getFresh = () => {
  page.value = 0
  router.reload({
    reset: ['foo', 'baz'],
  })
}
</script>

<template>
  <div>bar count is {{ bar.length }}</div>
  <div>baz count is {{ baz.length }}</div>
  <div>foo.data count is {{ foo.data.length }}</div>
  <div>first foo.data name is {{ foo.data[0].name }}</div>
  <div>last foo.data name is {{ foo.data[foo.data.length - 1].name }}</div>
  <div>foo.companies count is {{ foo.companies.length }}</div>
  <div>first foo.companies name is {{ foo.companies[0].name }}</div>
  <div>last foo.companies name is {{ foo.companies[foo.companies.length - 1].name }}</div>
  <div>foo.teams count is {{ foo.teams.length }}</div>
  <div>first foo.teams name is {{ foo.teams[0].name }}</div>
  <div>last foo.teams name is {{ foo.teams[foo.teams.length - 1].name }}</div>
  <div>foo.page is {{ foo.page }}</div>
  <div>foo.per_page is {{ foo.per_page }}</div>
  <div>foo.meta.label is {{ foo.meta.label }}</div>
  <button @click="reloadIt">Reload</button>
  <button @click="getFresh">Get Fresh</button>
</template>
