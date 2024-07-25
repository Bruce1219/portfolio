<template>
    <section
        class="w-full h-dvh bg-no-repeat bg-cover bg-center relative"
        @wheel="handleScroll"
        @touchstart="handleTouchStart"
        @touchmove="handleTouchMove"
    >
        <div
            v-for="(image, index) in images"
            :key="'bg-' + index"
            class="w-full h-full absolute top-0 left-0 bg-no-repeat bg-cover bg-center transition-all duration-1000 ease-in-out"
            :style="{
                backgroundImage: `url(${image.bgurl})`,
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
                            <img :src="image.src" :alt="'image-' + index" class="w-full h-full" />
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
        </div>
    </section>
    <!-- <img src="../assets/image/logoB.png" alt="" /> -->
</template>

<script>
import gsap from 'gsap'

export default {
    data() {
        return {
            currentImage: 0,
            images: [
                {
                    src: '@/assets/image/g4.png',
                    link: 'https://tibamef2e.com/cid101/g4/',
                    bgurl: '@/assets/image/g4bg.png',
                    name: '果籽 - 食農教育產銷平台',
                    info: '活動報名、活動紀錄 / 管理員、活動紀錄管理'
                },
                {
                    src: '@/assets/image/everything_burger.png',
                    link: 'https://bruce1219.github.io/everything-burger-rwd/',
                    bgurl: '@/assets/image/baner.png',
                    name: 'Everything Burger',
                    info: 'HTML/CSS、RWD切版、JS'
                }
            ],
            scrollAmount: 0,
            scrollThreshold: 300,
            touchStartY: 0,
            touchEndY: 0,
            touchThreshold: 50
        }
    },
    mounted() {
        this.initializeImages()
    },
    methods: {
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
            this.handleTouch()
        },
        handleTouch() {
            const touchDifference = this.touchStartY - this.touchEndY
            if (touchDifference > this.touchThreshold) {
                this.nextImage()
            } else if (touchDifference < -this.touchThreshold) {
                this.previousImage()
            }
            this.touchStartY = 0 // 重置觸摸起始位置
            this.touchEndY = 0 // 重置觸摸結束位置
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
                    clipPath: 'polygon(100% 0%, 100% 0%, 100% 100%, 100% 100%)',
                    duration: 1,
                    ease: 'power4.inOut'
                })
                gsap.to(nextImg, {
                    clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)',
                    duration: 1,
                    ease: 'power4.inOut'
                })
                gsap.to(currentBg, {
                    clipPath: 'polygon(100% 0%, 100% 0%, 100% 100%, 100% 100%)',
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
        }
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
