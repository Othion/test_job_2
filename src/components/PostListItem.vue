<template>
    <li class="post-item">
        <header class="post-item__header" @click="expandToggler">
            {{ post.title }}
        </header>

        <transition name="collapse">
            <div v-if="isCollapsed" class="post-item__content">
                {{ post.body }}
            </div>
        </transition>
    </li>
</template>

<script>
export default {
    props: {
        post: {
            type: Object,
            default: () => {}
        }
    },
    data () {
        return {
            isCollapsed: false
        }
    },
    methods: {
        expandToggler () {
            this.isCollapsed = !this.isCollapsed
        }
    }
}
</script>

<style lang="scss" scoped>
.post-item {
    padding: 14px;
    border-radius: 8px;
    cursor: pointer;
    transition: box-shadow .3s ease-in-out;
    box-shadow: 
        0px 0px 8px rgba(0, 0, 0, 0.08), 
        0px 2px 4px rgba(0, 0, 0, 0.1);

    &:hover {
        box-shadow: 
            0px 6px 12px rgba(0, 0, 0, 0.08),
            0px 0px 8px rgba(0, 0, 0, 0.08);
    }

    &__header {
        font-weight: bold;
        font-size: 20px;
        transition: color .3s ease;

        &:hover {
            color: #000;
        }
    }

    &__content {
        margin-top: 8px;
    }
}

.collapse {
    &-enter,
    &-leave-to {
        max-height: 0;
    }

    &-enter-to,
    &-leave {
        max-height: 200px;
    }

    &-enter,
    &-leave {
        &-active {
            overflow: hidden;
	        transition: max-height .5s linear;
        }
    }
}
</style>