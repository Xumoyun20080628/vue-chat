<template>
    <div class="messagers__window-header">
        <img :src="avatars[src]" alt="" class="messagers__window-avatar">
        <div class="messagers__window-info">
            <h2 class="messagers__window-name">{{ name }}</h2>
            <p class="messagers__window-status">{{ status }}</p>
        </div>
    </div>
</template>

<script>

export default {
    name: 'WindowHeader',
    props: ['src', 'name', 'status'],

    data() {
        return {
            avatars: {
                alex: require('@/assets/img/alex.png'),
                evgen: require('@/assets/img/evgen.png'),
            }
        }
    }
}
</script>

<style>
.messagers__window-header {
    padding: 31px 20px;
    background: #323232;
    display: flex;
    align-items: center;
    gap: 10px;
}

.messagers__window-name {
    color: #FFF;
    font-size: 18px;
    font-weight: 500;
    line-height: 77%;
    margin-bottom: 2px;
}

.messagers__window-status {
    color: #FFF;
    font-size: 14px;
    font-weight: 300;
    line-height: 128%;
}
</style>