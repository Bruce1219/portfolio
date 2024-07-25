<template>
    <div class="pre-loader w-full h-dvh fixed top-0 z-10 cursor-default">
        <div class="loader w-full h-dvh absolute top-0 bg-black z-10"></div>
        <div class="loader-bg w-full h-dvh absolute top-0 bg-sky-600"></div>
        <div
            class="loader-content absolute top-2/4 left-1/2 -translate-x-2/4 -translate-y-1/2 w-[450px] z-10"
        >
            <div class="loader-txt">
                <p class="text-center text-xl font-mono font-normal text-white">Bruce Portfolio</p>
            </div>
            <div class="count">
                <p class="text-center text-base font-mono font-normal text-white">{{ count }}%</p>
            </div>
        </div>
    </div>
    <div class="w-full h-dvh flex justify-center items-center">
        <div class="w-10/12 cursor-default">
            <h1 class="title text-center text-[18vw] font-mono font-light text-zinc-600">BRUCE</h1>
            <h2 class="subtitle text-center text-[9vw] font-mono font-normal text-zinc-600">
                Portfolio
            </h2>
        </div>
    </div>
    <IndexFooter />
</template>
<script>
import IndexFooter from '@/components/IndexFooter.vue'
import gsap from 'gsap'

export default {
    components: {
        IndexFooter
    },
    data() {
        return {
            count: 0
        }
    },
    methods: {
        startLoader() {
            const updateCounter = () => {
                if (this.count < 100) {
                    let increment = Math.floor(Math.random() * 10) + 1
                    this.count = Math.min(this.count + increment, 100)

                    let delay = Math.floor(Math.random() * 200) + 50
                    setTimeout(updateCounter, delay)
                } else {
                    this.animateTimeline()
                }
            }
            updateCounter()
        },
        animateTimeline() {
            const tl = gsap.timeline()

            tl.to('.count', {
                opacity: 0,
                duration: 0.5
            })
                .to('.loader-txt', {
                    opacity: 0,
                    duration: 1
                })
                .to(
                    '.pre-loader',
                    {
                        scale: 0.6,
                        ease: 'power3.inOut',
                        duration: 1
                    },
                    '-=1'
                )
                .to(
                    '.loader',
                    {
                        scaleX: 0,
                        transformOrigin: 'right',
                        ease: 'power3.inOut',
                        duration: 1.5
                    },
                    '-=0.5'
                )
                .to(
                    '.loader-bg',
                    {
                        scaleX: 0,
                        transformOrigin: 'right',
                        ease: 'power3.inOut',
                        duration: 0.8
                    },
                    '-=1'
                )
                .from(
                    '.title',
                    {
                        y: 50,
                        opacity: 0,
                        duration: 0.5
                    },
                    '-=0.5'
                )
                .from(
                    '.subtitle',
                    {
                        y: 50,
                        opacity: 0,
                        duration: 0.5
                    },
                    '-=0.2'
                )
        }
    },
    mounted() {
        this.startLoader()
    }
}
</script>

<style></style>
