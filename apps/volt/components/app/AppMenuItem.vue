<template>
    <li v-for="(menuitem, index) in menu" :key="`_root${index}`">
        <template v-if="menuitem.name === 'PrimeBlocks'">
            <a v-if="menuitem.href" :href="menuitem.href" target="_blank" rel="noopener noreferrer" class="cursor-pointer relative">
                <img v-if="layoutState.darkTheme" src="https://primefaces.org/cdn/primevue/images/primeblocks/primeblocks-menu-dark.jpg" class="w-full rounded-xl" />
                <img v-else src="https://primefaces.org/cdn/primevue/images/primeblocks/primeblocks-menu-light.jpg" class="w-full rounded-xl" />
                <span value="New" class="bg-yellow-400 text-black absolute end-2 top-3 text-xs font-bold rounded-md px-1 py-1 leading-none">NEW</span>
            </a>
        </template>
        <template v-else>
            <button v-if="menuitem.children && root" v-styleclass="{ selector: '@next', enterFromClass: 'hidden', enterActiveClass: 'animate-slidedown', leaveToClass: 'hidden', leaveActiveClass: 'animate-slideup' }" type="button">
                <span class="menu-icon">
                    <i :class="menuitem.icon"></i>
                </span>
                <span>{{ menuitem.name }}</span>
                <i class="menu-toggle-icon pi pi-angle-down"></i>
            </button>

            <a v-if="menuitem.href" :href="menuitem.href" target="_blank" rel="noopener noreferrer">
                <span v-if="menuitem.icon && root" class="menu-icon">
                    <i :class="menuitem.icon"></i>
                </span>
                <span>{{ menuitem.name }}</span>
                <Tag v-if="menuitem.badge" :value="menuitem.badge"></Tag>
            </a>

            <PrimeVueNuxtLink v-if="menuitem.to" :to="menuitem.to" :class="{ 'router-link-active': menuitem.to === $route.fullPath }">
                <span v-if="menuitem.icon && root" class="menu-icon">
                    <i :class="menuitem.icon"></i>
                </span>
                <span>{{ menuitem.name }}</span>
                <Tag v-if="menuitem.badge" :value="menuitem.badge"></Tag>
            </PrimeVueNuxtLink>

            <span v-if="!root && menuitem.children" class="menu-child-category">{{ menuitem.name }}</span>
            <div v-if="menuitem.children" :class="{ hidden: menuitem.children && root && isActiveRootmenuItem(menuitem) }">
                <ol>
                    <AppMenuItem :root="false" :menu="menuitem.children"></AppMenuItem>
                </ol>
            </div>
        </template>
    </li>
</template>

<script setup lang="ts">
import Tag from '@/volt/Tag.vue';
import { useRouter } from 'vue-router';

const props = defineProps({
    root: {
        type: Boolean,
        default: true
    },
    menu: {
        type: Object,
        default: null
    }
});

const router = useRouter();
const { layoutState } = useLayout();

const isActiveRootmenuItem = (menuitem: { children?: Array<{ to?: string; item?: any; children?: any }> }) => {
    return (
        menuitem.children &&
        !menuitem.children.some((item) => item.to === `/${(router.currentRoute.value?.name as string)?.replaceAll('-', '/')}` || (item.children && item.children.some((it: { to?: string }) => it.to === `/${router.currentRoute.value.name as string}`)))
    );
};
</script>
