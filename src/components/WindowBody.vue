<template>
    <main class="main">
        <TransitionGroup name="list">
            <div class="main__chatItem" v-for="(mess, index) in message" :key="index">
                <div class="main__chatItem-body" :class="{
                    send: mess.sendId == sendId,
                    get: mess.sendId != sendId,
                    photo: mess.photo?.length > 0 && mess.body.length == 0,
                    'photo-text': mess.photo?.length > 0 && mess.body.length > 0,
                }">
                    <span class="main__chatItem-time">{{ mess.time }}</span>
                    <div class="main__chatItem-text">
                        <img :src="mess.photo" v-if="mess.photo?.length > 0" alt="">
                        <p>{{ mess.body }}</p>
                    </div>
                </div>
            </div>
        </TransitionGroup>
    </main>
</template>

<script>

export default {
    name: 'WindowBody',

    props: {
        message: Array,
        sendId: Number
    }

}

</script>

<style>
*::-webkit-scrollbar {
    width: 4px;
    height: 6px;
}

*::-webkit-scrollbar-corner {
    background: transparent;
}

*::-webkit-scrollbar-thumb {
    background: rgba(0, 0, 0, 0.35);
    border-radius: 3px;
}

.main {
    overflow: auto;
    height: 632px;
}

.main__chatItem {
    display: flex;
    flex-direction: column;
    gap: 10px;
    padding: 10px;
}

.main__chatItem-body {
    display: flex;
    align-items: center;
    padding: 0 10px;
}

.main__chatItem-text {
    max-width: 80%;
    word-wrap: break-word;
    padding: 5px 10px;
    display: flex;
    flex-direction: column;
}

.main__chatItem-text img {
    width: 100%;
    border-radius: 13px;
}

.main__chatItem-body.photo .main__chatItem-text {
    border-radius: 15px;
    padding: 2px;
}

.main__chatItem-body.photo-text .main__chatItem-text {
    border-radius: 15px;
    padding: 2px 2px 0px;
}

.main__chatItem-body.photo-text p {
    padding: 5px 5px 6px;
}

.main__chatItem-body.send {
    justify-content: end;
}

.main__chatItem-body.send .main__chatItem-text {
    border-radius: 15px 15px 0px 15px;
    background: #D0DCFF;
    margin-left: 5px;
}

.main__chatItem-body.get {
    flex-direction: row-reverse;
    justify-content: start;
}

.main__chatItem-body.get .main__chatItem-text {
    border-radius: 15px 15px 15px 0px;
    background: #C4BFFF;
    margin-right: 5px;
}

.list-enter-active,
.list-leave-active {
    transition: 300ms linear;
}

.list-enter-from,
.list-leave-to {
    opacity: 0;
    transform: scale(0.9);
}
</style>