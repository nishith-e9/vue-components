<template>
    <div>
        <div class="tabbar">
            <div id="navigation">
                <ul class="menu">
                    <li v-for="(route, key) in menu" :key="key" @click="toggleOffscreenMenu(false)">
                        <router-link v-if="!route.subItems" :to="route.path" active-class="active">
                            <div class="menu-item">
                                <Badge v-if="route.badgeOptions" v-bind="route.badgeOptions">
                                    <i class="material-icons">{{ route.icon }}</i>
                                </Badge>
                                <i v-else class="material-icons">{{ route.icon }}</i>
                                <span v-text="route.name" />
                            </div>
                        </router-link>
                    </li>
                    <li v-if="offscreenMenu.length > 0">
                        <a @click="toggleOffscreenMenu(true)">
                            <div class="menu-item">
                                <i class="material-icons">more_horiz</i>
                                <span>More</span>
                            </div>
                        </a>
                    </li>
                </ul>
            </div>
        </div>
        <div v-if="showOffscreenMenu" class="offscreen-navigation">
            <ul class="offscreen-menu">
                <li v-for="(route, key) in offscreenMenu" :key="key" @click="toggleOffscreenMenu(false)">
                    <router-link v-if="!route.subItems" :to="route.path" active-class="active">
                        <div class="menu-item">
                            <i class="material-icons icon-left">{{ route.icon }}</i>
                            <p>
                                <Badge v-if="route.badgeOptions" v-bind="route.badgeOptions">
                                    <span v-text="route.name" />
                                </Badge>
                                <span v-else v-text="route.name" />
                                <i class="material-icons icon-right">arrow_forward_ios</i>
                            </p>
                        </div>
                    </router-link>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import Badge from './Badge.vue';
export default {
    name: 'TabBar',
    components: {
        Badge
    },
    props: {
        menu: {
            type: Array,
            required: true
        },
        limit: {
            type: Number,
            default: 3
        }
    },
    data() {
        return {
            offscreenMenu: [],
            showOffscreenMenu: false
        };
    },
    mounted() {
        if (this.menu.length > this.limit) {
            this.offscreenMenu = this.menu.splice(this.limit, this.menu.length - this.limit);
        }
    },
    methods: {
        toggleOffscreenMenu(toggle) {
            this.showOffscreenMenu = toggle;
        }
    }
};
</script>
