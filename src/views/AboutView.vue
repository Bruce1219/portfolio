<template>
    <section class="w-full h-dvh flex justify-center cursor-default">
        <div
            class="w-full max-w-screen-2xl h-dvh flex flex-col md:flex-row items-center justify-center md:justify-evenly px-[5%]"
        >
            <div
                class="w-[250px] sm:w-[300px] md:w-[400px] h-[250px] sm:h-[300px] md:h-[400px] mx-2 rounded-full overflow-hidden duration-500"
            >
                <img src="../assets/image/me.jpg" alt="" class="w-full" />
            </div>
            <div
                class="w-[80%] sm:w-[50%] max-w-[350px] mt-10 font-mono font-normal text-sm md:text-base text-zinc-600 tracking-widest"
            >
                <div>
                    <h1 class="font-bold text-base md:text-2xl mb-[20px]">蔣瀚緯</h1>
                    <p class="mb-[10px]">
                        大學時主要專攻平面及美術設計，對美感及設計工具有一定的底子。因為對前端工程領域有興趣，目前正在精進自己在前端技術的能力，往前端工程師邁進。
                    </p>
                    <hr class="mb-[10px]" />
                    <h2 class="font-normal text-base md:text-xl mb-[10px]">技能</h2>
                    <div class="w-full flex flex-wrap gap-[5px]">
                        <div class="w-[50px] h-[50px] mb-3" v-for="item in skills" :key="item">
                            <img
                                :src="parsePic(item.img)"
                                alt=""
                                class="w-full h-full object-contain object-center"
                            />
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    data() {
        return {
            skills: [
                {
                    img: 'html.png'
                },
                {
                    img: 'css.png'
                },
                {
                    img: 'js.png'
                },
                {
                    img: 'vue.png'
                },
                {
                    img: 'scss.png'
                },
                {
                    img: 'tailwind.png'
                },
                {
                    img: 'github.png'
                },
                {
                    img: 'photoshop.png'
                },
                {
                    img: 'illustrator.png'
                },
                {
                    img: 'figma.png'
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
