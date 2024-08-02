<template>
    <section class="w-full h-dvh flex justify-center cursor-default">
        <div
            class="w-full max-w-screen-2xl h-dvh flex flex-col md:flex-row items-center justify-center md:justify-evenly px-[5%]"
        >
            <div
                class="w-[150px] sm:w-[200px] md:w-[330px] lg:w-[350px] h-[150px] sm:h-[200px] md:h-[330px] lg:h-[350px] relative mt-8 sm:mt-10 md:mt-0"
            >
                <div
                    class="w-[150px] sm:w-[200px] md:w-[330px] lg:w-[350px] h-[150px] sm:h-[200px] md:h-[330px] lg:h-[350px] mx-2 rounded-full overflow-hidden duration-500 absolute top-0 z-30 border-solid border-[10px] border-[#EAEAEA] box-border"
                >
                    <img src="../assets/image/me2.jpg" alt="" class="w-full" />
                </div>
                <img
                    src="../assets/image/grey1.png"
                    alt=""
                    class="grey1 w-full absolute top-[-20px] left-[-10px] z-10"
                />
                <img src="../assets/image/grey2.png" alt="" class="grey2 w-full absolute top-4" />
                <img
                    src="../assets/image/grey4.png"
                    alt=""
                    class="grey4 w-full absolute right-[-10px] z-20 scale-110"
                />
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
import gsap from 'gsap'

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
        },
        grey1Ani() {
            gsap.to('.grey1', {
                rotation: 360,
                ease: 'none',
                duration: 7,
                repeat: -1
            })
        },
        grey2Ani() {
            gsap.to('.grey2', {
                rotation: 360,
                ease: 'none',
                duration: 6,
                repeat: -1
            })
        },
        grey4Ani() {
            let tl = gsap.timeline({ repeat: -1, repeatDelay: 0 })

            tl.to('.grey4', {
                scale: 1.2,
                rotation: 180,
                duration: 4,
                ease: 'none'
            }).to('.grey4', {
                scale: 1.1,
                rotation: 360,
                duration: 4,
                ease: 'none'
            })
        }
    },
    mounted() {
        // this.grey1Ani()
        // this.grey2Ani()
        this.grey4Ani()
    }
}
</script>
