<template>
    <div class="fixed top-0 w-full">
        <nav class="flex justify-between items-center px-4 py-2 backdrop-blur bg-white/30">
            <router-link
                to="/"
                class="block w-10 h-10 rounded-full overflow-hidden md:w-16 md:h-16"
            >
                <img
                    src="../assets/image/logoB.png"
                    alt="logo"
                    class="w-full object-cover md:w-full h-full duration-500 hover:scale-125"
                />
            </router-link>
            <div class="nav-item">
                <router-link
                    to="/about"
                    class="mx-5 pb-1 font-mono font-normal text-base md:text-xl text-zinc-600 duration-500 border-b-2 border-solid border-transparent hover:border-zinc-600"
                    >About</router-link
                >
                <router-link
                    to="/work"
                    class="mx-5 pb-1 font-mono font-normal text-base md:text-xl text-zinc-600 duration-500 border-b-2 border-solid border-transparent hover:border-zinc-600"
                    >Work</router-link
                >
                <router-link
                    to="/contact"
                    class="mx-5 pb-1 font-mono font-normal text-base md:text-xl text-zinc-600 duration-500 border-b-2 border-solid border-transparent hover:border-zinc-600"
                    >Contact</router-link
                >
            </div>
        </nav>
    </div>
</template>

<script></script>

<style lang="scss" scoped></style>
