<script setup lang="ts">
import { SidebarGroup, SidebarGroupLabel, SidebarMenu, SidebarMenuButton, SidebarMenuItem } from '@/components/ui/sidebar';
import { type SharedData } from '@/types';
import { Link, usePage } from '@inertiajs/vue3';
import type { Component } from 'vue';
import { ref } from 'vue';

interface NavItem {
    title: string;
    url: string;
    icon: Component;
    children?: NavItem[]; // Add support for nested items
    isOpen?: boolean; // Add support for expand/collapse state
}

defineProps<{
    items: NavItem[];
}>();

const page = usePage<SharedData>();

// Function to toggle the expand/collapse state of an item
const toggleItem = (item: NavItem) => {
    if (item.children) {
        item.isOpen = !item.isOpen; // Toggle the isOpen property
    }
};
</script>

<template>
    <SidebarGroup class="px-2 py-0">
        <SidebarGroupLabel>Platform</SidebarGroupLabel>
        <SidebarMenu>
            <SidebarMenuItem v-for="item in items" :key="item.title">
                <SidebarMenuButton as-child :is-active="item.url === page.url" @click="toggleItem(item)">
                    <Link :href="item.url" class="flex items-center w-full">
                        <component :is="item.icon" class="w-4 h-4 mr-2" />
                        <span>{{ item.title }}</span>
                        <span v-if="item.children" class="ml-auto transform transition-transform" :class="{ 'rotate-90': item.isOpen }">▼</span>
                    </Link>
                </SidebarMenuButton>
                <Transition name="slide">
                    <div v-if="item.children && item.isOpen" class="pl-4">
                        <SidebarMenu>
                            <SidebarMenuItem v-for="child in item.children" :key="child.title">
                                <SidebarMenuButton as-child :is-active="child.url === page.url">
                                    <Link :href="child.url" class="flex items-center">
                                        <component :is="child.icon" class="w-4 h-4 mr-2" v-if="child.icon" />
                                        <span>{{ child.title }}</span>
                                    </Link>
                                </SidebarMenuButton>
                            </SidebarMenuItem>
                        </SidebarMenu>
                    </div>
                </Transition>
            </SidebarMenuItem>
        </SidebarMenu>
    </SidebarGroup>
</template>

<style scoped>
/* Animation for expanding/collapsing nested items */
.slide-enter-active,
.slide-leave-active {
    transition: all 0.3s ease;
}

.slide-enter-from,
.slide-leave-to {
    opacity: 0;
    transform: translateY(-10px);
}
</style>
