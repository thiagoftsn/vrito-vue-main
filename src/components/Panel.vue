<template>
    <div class="panel" :class="panelClass">
        <!-- Header Section -->
        <div v-if="title || $slots.header || $slots.actions" class="flex items-center justify-between mb-5">
            <!-- Title/Header Slot -->
            <slot name="header">
                <h5 class="font-semibold text-lg dark:text-white-light">{{ title }}</h5>
            </slot>

            <!-- Actions Slot -->
            <slot name="actions"></slot>
        </div>

        <!-- Body Content -->
        <div :class="bodyClass">
            <slot></slot>
        </div>

        <!-- Footer Section (Optional) -->
        <div v-if="$slots.footer" :class="footerClass">
            <slot name="footer"></slot>
        </div>
    </div>
</template>

<script lang="ts" setup>
interface Props {
    title?: string;
    panelClass?: string;
    bodyClass?: string;
    footerClass?: string;
}

withDefaults(defineProps<Props>(), {
    title: '',
    panelClass: '',
    bodyClass: '',
    footerClass: '',
});
</script>
