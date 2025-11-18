<script setup lang="ts">
import { ref } from 'vue';

defineProps<{
    src: string;
    alt?: string;
    className?: string;
}>();

const isLoading = ref(true);
const imageError = ref(false);

const handleLoad = () => {
    isLoading.value = false;
    imageError.value = false;
};

const handleError = () => {
    isLoading.value = false;
    imageError.value = true;
};
</script>

<template>
    <div class="lazy-image-wrapper">
        <img 
            :src="src" 
            :alt="alt || ''" 
            :class="className"
            @load="handleLoad"
            @error="handleError"
        />
        <div v-if="isLoading" class="loading-text">图片加载中...</div>
        <div v-if="imageError" class="error-text">图片加载失败</div>
    </div>
</template>

<style lang="css" scoped>
.lazy-image-wrapper {
    position: relative;
    width: 100%;
}

.loading-text,
.error-text {
    display: none;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 14px;
    color: #666;
    background-color: rgba(255, 255, 255, 0.9);
    padding: 8px 16px;
    border-radius: 4px;
    z-index: 1;
}

/* 只在移动端显示加载提示 */
@media (max-width: 600px) {
    .loading-text,
    .error-text {
        display: block;
    }
}

img {
    width: 100%;
    display: block;
}
</style>

