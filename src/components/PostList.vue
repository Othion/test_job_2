<template>
    <ul class="post-list">
        <post-list-item
            v-for="item in postList"
            :key="item.id"
            :post="item"
        />
    </ul>
</template>

<script>
import PostListItem from './PostListItem'

export default {
    components: {
        PostListItem
    },
    props: {
        postList: {
            type: Array,
            default: () => []
        }
    }
}
</script>

<style lang="scss" scoped>
.post-list {
    list-style: none;
    margin: 0;
    padding: 0;
    display: grid;
    align-items: flex-start;
    grid-template-columns: repeat(auto-fit, 500px);
    grid-gap: 12px;
}
</style>