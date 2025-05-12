<script setup>

const props = defineProps({
    image: {
        type: String,
        required: true,
    },
    imageHeight: {
        type: String,
        required: true
    },
    contentClass: {
        type: String,
        required: true
    }
})

const defaultImageStyle='absolute-center z-0 mt-2rem'
const imageStyle = defaultImageStyle + ' ' + props.imageHeight
</script>

<template>
    <div class="slidev-layout image-centered">
        <slot name="header" />
        <div class="grid place-content-center h-6/7">
            <img  :src="image" :class="imageStyle" />

            <div class="z-1">
                <ul :class="contentClass">
                    <slot name="content" />
                </ul>
            </div>
        </div>
    </div>
</template>