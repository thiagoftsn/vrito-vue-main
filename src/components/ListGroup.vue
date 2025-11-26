<template>
    <div class="flex flex-col rounded-md border border-[#e0e6ed] dark:border-[#1b2e4b]">
        <div
            v-for="(item, index) in items"
            :key="index"
            :class="[
                'flex px-4 py-2.5',
                index !== items.length - 1 ? 'border-b border-[#e0e6ed] dark:border-[#1b2e4b]' : '',
                item.active
                    ? 'bg-primary text-white shadow-[0_1px_15px_1px_rgba(67,97,238,0.15)] hover:bg-[#eee] dark:hover:bg-[#eee]/10 hover:text-black dark:hover:text-white group'
                    : 'hover:bg-[#eee] dark:hover:bg-[#eee]/10',
                itemClass,
            ]"
            @click="$emit('itemClick', item, index)"
        >
            <!-- Image/Avatar Slot -->
            <div v-if="item.image || $slots.image" :class="imageContainerClass || 'ltr:mr-3 rtl:ml-3'">
                <slot name="image" :item="item" :index="index">
                    <img
                        v-if="item.image"
                        :src="item.image"
                        :alt="item.imageAlt || ''"
                        :class="imageClass || 'rounded-full w-12 h-12 object-cover'"
                    />
                </slot>
            </div>

            <!-- Icon Slot -->
            <div v-if="item.icon || $slots.icon" :class="iconContainerClass || 'ltr:mr-2 rtl:ml-2.5 mt-0.5 text-primary'">
                <slot name="icon" :item="item" :index="index">
                    <component v-if="item.icon" :is="item.icon" :class="iconClass" />
                </slot>
            </div>

            <!-- Content -->
            <div :class="contentClass || 'flex-1 font-semibold'">
                <slot :item="item" :index="index">
                    <h6 v-if="item.title" :class="titleClass || 'mb-1 text-base'">{{ item.title }}</h6>
                    <p v-if="item.subtitle" :class="subtitleClass || 'text-xs'">{{ item.subtitle }}</p>
                    <p v-if="item.description" :class="descriptionClass || 'text-xs'">{{ item.description }}</p>
                </slot>
            </div>

            <!-- Badge/Tag Slot -->
            <div v-if="item.badge || $slots.badge">
                <slot name="badge" :item="item" :index="index">
                    <span v-if="item.badge" :class="item.badgeClass || 'badge bg-primary'">{{ item.badge }}</span>
                </slot>
            </div>
        </div>
    </div>
</template>

<script lang="ts" setup>
interface ListGroupItem {
    title?: string;
    subtitle?: string;
    description?: string;
    image?: string;
    imageAlt?: string;
    icon?: any;
    badge?: string;
    badgeClass?: string;
    active?: boolean;
    [key: string]: any;
}

interface Props {
    items: ListGroupItem[];
    itemClass?: string;
    imageContainerClass?: string;
    imageClass?: string;
    iconContainerClass?: string;
    iconClass?: string;
    contentClass?: string;
    titleClass?: string;
    subtitleClass?: string;
    descriptionClass?: string;
}

withDefaults(defineProps<Props>(), {
    items: () => [],
    itemClass: '',
    imageContainerClass: '',
    imageClass: '',
    iconContainerClass: '',
    iconClass: '',
    contentClass: '',
    titleClass: '',
    subtitleClass: '',
    descriptionClass: '',
});

defineEmits<{
    itemClick: [item: ListGroupItem, index: number];
}>();
</script>
