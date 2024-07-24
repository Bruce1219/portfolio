<template>
    <RouterView />
</template>

<script>
import { RouterView } from 'vue-router'
import './assets/scss/base/_reset.scss'

export default {
    name: 'App',
    components: {
        RouterView
    }
}
</script>

<style lang="scss"></style>
