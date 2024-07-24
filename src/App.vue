<template>
    <RouterView />
</template>

<script>
import { RouterView } from 'vue-router'
import './assets/scss/_reset.scss'

export default {
    name: 'App',
    components: {
        RouterView
    }
}
</script>

<style lang="scss"></style>
