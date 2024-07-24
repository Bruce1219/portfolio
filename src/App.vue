<template>
    <NavBar />
    <RouterView />
</template>

<script>
import NavBar from '@/components/NavBar.vue'

import { RouterView } from 'vue-router'
import './assets/scss/_reset.scss'

export default {
    name: 'App',
    components: {
        NavBar,
        RouterView
    }
}
</script>

<style lang="scss"></style>
