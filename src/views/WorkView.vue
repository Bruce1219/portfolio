<template>
    <section class="w-full h-dvh bg-no-repeat bg-cover bg-center relative cursor-default">
        <!-- 背景圖片 -->
        <div
            v-for="(image, index) in images"
            :key="'bg-' + index"
            class="w-full h-full absolute top-0 left-0 bg-no-repeat bg-cover bg-center"
            :style="{
                backgroundImage: `url(${parsePic(image.bgurl)})`,
                zIndex: images.length - index - 1
            }"
            :ref="
                (el) => {
                    if (el) bgRefs[index] = el
                }
            "
        ></div>
        <div class="w-full h-dvh absolute top-0 backdrop-blur bg-white/50 z-10">
            <!-- 圖片展示區域 -->
            <div
                class="w-4/5 md:w-2/4 aspect-video absolute top-2/4 left-1/2 -translate-x-2/4 -translate-y-1/2 rounded-lg overflow-hidden"
                @touchstart="handleDragStart"
                @touchmove="handleDragMove"
                @touchend="handleDragEnd"
            >
                <div
                    class="w-full h-full flex transition-transform duration-300 ease-out"
                    :style="{
                        transform: `translateX(${-currentImage * 100 + dragOffsetPercent}%)`
                    }"
                >
                    <div
                        v-for="(image, index) in images"
                        :key="'img-' + index"
                        class="w-full h-full flex-shrink-0"
                        :ref="
                            (el) => {
                                if (el) imgRefs[index] = el
                            }
                        "
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
                <!-- 圖片信息 -->
                <div
                    v-for="(image, index) in images"
                    :key="'info-' + index"
                    class="w-full flex flex-col items-center mt-5 font-mono font-normal text-zinc-600 tracking-widest info-text absolute"
                    :style="{
                        zIndex: images.length - index,
                        opacity: index === currentImage ? 1 : 0
                    }"
                >
                    <p class="font-bold text-sm md:text-lg">{{ image.name }}</p>
                    <p class="text-xs md:text-base">{{ image.info }}</p>
                </div>
            </div>
            <!-- 導航按鈕 -->
            <div class="absolute top-2/4 left-[3%] md:left-[20%]" v-if="currentImage > 0">
                <button @click="previousImage">
                    <font-awesome-icon
                        :icon="['fas', 'chevron-left']"
                        class="text-sky-600 text-base md:text-3xl"
                    />
                </button>
            </div>
            <div
                class="absolute top-2/4 right-[3%] md:right-[20%]"
                v-if="currentImage < images.length - 1"
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
            imgRefs: [],
            bgRefs: [],
            dragStartX: 0,
            dragOffset: 0,
            dragOffsetPercent: 0,
            isDragging: false,
            dragThreshold: 50,
            touchStartTime: 0
        }
    },
    methods: {
        parsePic(file) {
            return new URL(`../assets/image/${file}`, import.meta.url).href
        },
        initializeImages() {
            this.bgRefs.forEach((bg, index) => {
                if (index === 0) {
                    gsap.set(bg, { clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)' })
                } else {
                    gsap.set(bg, { clipPath: 'polygon(100% 0%, 100% 0%, 100% 100%, 100% 100%)' })
                }
            })
        },
        nextImage() {
            if (this.currentImage < this.images.length - 1) {
                this.transitionToImage(this.currentImage + 1)
            }
        },
        previousImage() {
            if (this.currentImage > 0) {
                this.transitionToImage(this.currentImage - 1)
            }
        },
        transitionToImage(newIndex) {
            const currentBg = this.bgRefs[this.currentImage]
            const nextBg = this.bgRefs[newIndex]

            if (newIndex > this.currentImage) {
                gsap.to(currentBg, {
                    clipPath: 'polygon(0% 0%, 0% 0%, 0% 100%, 0% 100%)',
                    duration: 1.5,
                    ease: 'power4.inOut'
                })
                gsap.to(nextBg, {
                    clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)',
                    duration: 1.5,
                    ease: 'power4.inOut'
                })
            } else {
                gsap.to(currentBg, {
                    clipPath: 'polygon(100% 0%, 100% 0%, 100% 100%, 100% 100%)',
                    duration: 1.5,
                    ease: 'power4.inOut'
                })
                gsap.to(nextBg, {
                    clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)',
                    duration: 1.5,
                    ease: 'power4.inOut'
                })
            }

            this.currentImage = newIndex
        },
        handleDragStart(event) {
            this.dragStartX = event.touches[0].clientX
            this.isDragging = true
            this.dragOffset = 0
            this.dragOffsetPercent = 0
            this.touchStartTime = new Date().getTime()
        },
        handleDragMove(event) {
            if (!this.isDragging) return
            const currentX = event.touches[0].clientX
            this.dragOffset = currentX - this.dragStartX
            const containerWidth = event.target.offsetWidth
            this.dragOffsetPercent = (this.dragOffset / containerWidth) * 100
        },
        handleDragEnd() {
            if (!this.isDragging) return
            const touchEndTime = new Date().getTime()
            const touchDuration = touchEndTime - this.touchStartTime

            if (Math.abs(this.dragOffset) > this.dragThreshold) {
                if (this.dragOffset > 0 && this.currentImage > 0) {
                    this.transitionToImage(this.currentImage - 1)
                } else if (this.dragOffset < 0 && this.currentImage < this.images.length - 1) {
                    this.transitionToImage(this.currentImage + 1)
                }
            } else if (touchDuration < 200 && Math.abs(this.dragOffset) < 10) {
                // 短暫輕觸，不做任何處理
            }

            this.isDragging = false
            this.dragOffset = 0
            this.dragOffsetPercent = 0
        }
    },
    mounted() {
        this.$nextTick(() => {
            this.initializeImages()
        })
    }
}
</script>

<style scoped>
[class^='bg-'] {
    clip-path: polygon(100% 0%, 100% 0%, 100% 100%, 100% 100%);
}
</style>
