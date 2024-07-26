<template>
    <section
        class="w-full h-dvh bg-no-repeat bg-cover bg-center relative cursor-default"
        @wheel="handleScroll"
        @touchstart="handleTouchStart"
        @touchmove="handleTouchMove"
        @touchend="handleTouchEnd"
    >
        <div
            v-for="(image, index) in images"
            :key="'bg-' + index"
            class="w-full h-full absolute top-0 left-0 bg-no-repeat bg-cover bg-center transition-all duration-1000 ease-in-out"
            :style="{
                backgroundImage: `url(${parsePic(image.bgurl)})`,
                zIndex: images.length - index - 1
            }"
            :class="{ 'bg-active': index === currentImage }"
        ></div>
        <div class="w-full h-dvh absolute top-0 backdrop-blur bg-white/50 z-10">
            <div
                class="w-4/5 md:w-2/4 aspect-video absolute top-2/4 left-1/2 -translate-x-2/4 -translate-y-1/2"
            >
                <div class="w-full h-full flex flex-col overflow-hidden rounded-lg relative">
                    <div
                        v-for="(image, index) in images"
                        :key="'img-' + index"
                        class="w-full h-full img absolute top-0 left-0"
                        :style="{ zIndex: images.length - index }"
                    >
                        <a :href="image.link" target="_blank">
                            <img
                                :src="parsePic(image.src)"
                                :alt="'image-' + index"
                                class="w-full h-full"
                            />
                        </a>
                    </div>
                </div>
                <div
                    v-for="(image, index) in images"
                    :key="'info-' + index"
                    class="w-full flex flex-col items-center mt-5 font-mono font-normal text-zinc-600 tracking-widest info-text absolute delay-500"
                    :style="{
                        zIndex: images.length - index,
                        opacity: index === currentImage ? 1 : 0
                    }"
                >
                    <p class="font-bold text-sm md:text-lg">{{ image.name }}</p>
                    <p class="text-xs md:text-base">{{ image.info }}</p>
                </div>
            </div>
            <div class="absolute bottom-10 right-1/2 md:right-5 md:top-2/4 flex flex-col">
                <p
                    class="font-mono font-bold text-lg text-sky-600 tracking-widest rotate-90 hidden md:block"
                >
                    SCROLL
                </p>
                <font-awesome-icon
                    :icon="['fas', 'angles-down']"
                    class="mt-5 text-sky-600 text-xl down"
                />
            </div>
            <div class="absolute top-2/4 left-[3%] md:left-[20%]" v-if="currentImage != 0">
                <button @click="previousImage">
                    <font-awesome-icon
                        :icon="['fas', 'chevron-left']"
                        class="text-sky-600 text-base md:text-3xl"
                    />
                </button>
            </div>
            <div
                class="absolute top-2/4 right-[3%] md:right-[20%]"
                v-if="currentImage + 1 != images.length"
            >
                <button @click="nextImage">
                    <font-awesome-icon
                        :icon="['fas', 'chevron-right']"
                        class="text-sky-600 text-base md:text-3xl"
                    />
                </button>
            </div>
        </div>
    </section>
</template>

<script>
import gsap from 'gsap'
export default {
    data() {
        return {
            currentImage: 0,
            images: [
                {
                    src: 'g4.png',
                    link: 'https://tibamef2e.com/cid101/g4/',
                    bgurl: 'g4bg.png',
                    name: '果籽 - 食農教育產銷平台',
                    info: '活動報名、活動紀錄 / 管理員、活動紀錄管理'
                },
                {
                    src: 'everything_burger.png',
                    link: 'https://bruce1219.github.io/everything-burger-rwd/',
                    bgurl: 'baner.png',
                    name: 'Everything Burger',
                    info: 'HTML/CSS、RWD切版、JS'
                },
                {
                    src: 'johnwick2.png',
                    link: 'https://bruce1219.github.io/everything-burger-rwd/',
                    bgurl: 'greybg.png',
                    name: '平面設計',
                    info: 'Adobe illustrator、PhotoShop'
                }
            ],
            scrollAmount: 0,
            scrollThreshold: 350,
            touchStartY: 0,
            touchEndY: 0,
            touchThreshold: 20
        }
    },
    methods: {
        parsePic(file) {
            return new URL(`../assets/image/${file}`, import.meta.url).href
        }, //本地圖片
        initializeImages() {
            gsap.set('.img', { clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)' })
            gsap.set('.img:first-child', {
                clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)'
            })
            gsap.set('.bg-active', { clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)' })
        },
        handleScroll(event) {
            this.scrollAmount += event.deltaY
            if (this.scrollAmount >= this.scrollThreshold) {
                this.nextImage()
                this.scrollAmount = 0 // 重置滾動量
            } else if (this.scrollAmount <= -this.scrollThreshold) {
                this.previousImage()
                this.scrollAmount = 0 // 重置滾動量
            }
        },
        handleTouchStart(event) {
            this.touchStartY = event.touches[0].clientY
        },
        handleTouchMove(event) {
            this.touchEndY = event.touches[0].clientY
        },
        handleTouchEnd() {
            this.handleTouch()
        },
        handleTouch() {
            const touchDifference = this.touchStartY - this.touchEndY
            if (Math.abs(touchDifference) > this.touchThreshold) {
                if (touchDifference > 0) {
                    this.nextImage()
                } else {
                    this.previousImage()
                }
            }
            this.touchStartY = 0
            this.touchEndY = 0
        },
        nextImage() {
            if (this.currentImage < this.images.length - 1) {
                const currentImg = document.querySelector(
                    `.img:nth-child(${this.currentImage + 1})`
                )
                const nextImg = document.querySelector(`.img:nth-child(${this.currentImage + 2})`)
                const currentBg = document.querySelector(`.bg-active`)
                const nextBg = document.querySelector(
                    `[style*="z-index: ${this.images.length - this.currentImage - 2}"]`
                )

                gsap.to(currentImg, {
                    clipPath: 'polygon(0% 0%, 0% 0%, 0% 100%, 0% 100%)',
                    duration: 1,
                    ease: 'power4.inOut'
                })
                gsap.to(nextImg, {
                    clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)',
                    duration: 1,
                    ease: 'power4.inOut'
                })
                gsap.to(currentBg, {
                    clipPath: 'polygon(0% 0%, 0% 0%, 0% 100%, 0% 100%)',
                    duration: 0.5,
                    ease: 'power4.inOut'
                })
                gsap.to(nextBg, {
                    clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)',
                    duration: 0.5,
                    ease: 'power4.inOut'
                })

                this.currentImage++
            }
        },
        previousImage() {
            if (this.currentImage > 0) {
                const currentImg = document.querySelector(
                    `.img:nth-child(${this.currentImage + 1})`
                )
                const prevImg = document.querySelector(`.img:nth-child(${this.currentImage})`)
                const currentBg = document.querySelector(`.bg-active`)
                const prevBg = document.querySelector(
                    `[style*="z-index: ${this.images.length - this.currentImage}"]`
                )

                gsap.to(currentImg, {
                    clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)',
                    duration: 1,
                    ease: 'power4.inOut'
                })
                gsap.to(prevImg, {
                    clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)',
                    duration: 1,
                    ease: 'power4.inOut'
                })
                gsap.to(currentBg, {
                    clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)',
                    duration: 0.5,
                    ease: 'power4.inOut'
                })
                gsap.to(prevBg, {
                    clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)',
                    duration: 0.5,
                    ease: 'power4.inOut'
                })

                this.currentImage--
            }
        },
        downAnimation() {
            gsap.to('.down', {
                y: 8,
                duration: 2,
                ease: 'power1.inOut',
                repeat: -1
            })
        }
    },
    mounted() {
        this.initializeImages()
        this.downAnimation()
    }
}
</script>

<style scoped>
.img,
[class^='bg-'] {
    clip-path: polygon(0% 100%, 100% 100%, 100% 100%, 0% 100%);
}
.bg-active {
    clip-path: polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%);
}
</style>
