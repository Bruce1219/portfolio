<template>
    <section class="w-full max-w-screen-2xl mx-auto pb-20">
        <div class="mt-24 ml-[3%]">
            <h1 class="font-mono font-bold text-2xl text-zinc-600 tracking-widest">平面設計</h1>
        </div>
        <div class="w-[95%] mt-5 mx-auto">
            <div class="grid grid-cols-1 sm:grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-5">
                <div class="w-full h-[400px] overflow-hidden" v-for="item in images" :key="item">
                    <img
                        :src="parsePic(item.img)"
                        alt=""
                        class="w-full h-full object-cover object-center hover:scale-125 duration-500"
                    />
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    data() {
        return {
            images: [
                {
                    img: 'p4.jpg'
                },
                {
                    img: 'p3.jpg'
                },
                {
                    img: 'p2.jpg'
                },
                {
                    img: 'p5.jpg'
                },
                {
                    img: 'p10.jpg'
                },
                {
                    img: 'p1.jpg'
                },
                {
                    img: 'p11.jpg'
                },
                {
                    img: 'p12.jpg'
                }
            ]
        }
    },
    methods: {
        parsePic(file) {
            return new URL(`../assets/image/${file}`, import.meta.url).href
        }
    }
}
</script>
