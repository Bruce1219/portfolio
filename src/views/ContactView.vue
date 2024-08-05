<template>
    <section class="w-full h-dvh flex justify-center items-center cursor-default">
        <div
            class="w-[95%] sm:w-[20%] sm:min-w-[300px] max-w-[280px] sm:max-w-[310px] flex flex-col items-center text-sm sm:text-base font-mono font-normal text-zinc-600 tracking-widest"
        >
            <div class="w-full mt-3 flex items-center">
                <span class="text-lg font-bold mr-2">蔣瀚緯</span>
                <span>Han-Wei Chiang</span>
            </div>
            <div class="w-full mt-3 flex items-center">
                <font-awesome-icon :icon="['fas', 'phone']" class="mr-2" />
                <a href="tel:+886-938592510">0938-592-510</a>
            </div>
            <div class="w-full mt-3 flex items-center">
                <font-awesome-icon :icon="['fas', 'envelope']" class="mr-2" />
                <a href="mailto:891219chiang@gmail.com">891219chiang@gmail.com</a>
            </div>
            <div class="w-full mt-3 flex items-center">
                <font-awesome-icon :icon="['fab', 'github']" class="mr-2" />
                <a href="https://github.com/Bruce1219" target="_blank"
                    >https://github.com/Bruce1219</a
                >
            </div>
        </div>
    </section>
</template>
