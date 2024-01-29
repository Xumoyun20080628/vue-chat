<template>
    <div class="footer">
        <textarea rows="1" placeholder="Написать сообщение..." class="footer__edit" v-model="message"></textarea>
        <button class="footer__btn" v-if="message.length == 0" @click="window = true">
            <img src="@src/assets/img/photo.svg" alt="">
        </button>
        <button class="footer__btn" @click="sendMess" v-else>
            <img src="@src/assets/img/send.svg" alt="">
        </button>
        <div class="footer__window" v-if="window" @click="window = false">
            <div class="window__body" @click.stop.prevent>
                <h2 class="window__title">Отправить картинку</h2>
                <div class="window__form">
                    <label>
                        <span>URL</span>
                        <input v-model="photo" placeholder="URL">
                    </label>
                    <label>
                        <span>Комментарий</span>
                        <textarea v-model="comment" placeholder="Комментарий"></textarea>
                    </label>
                </div>
                <div class="window__btns">
                    <button class="btn cancel" @click="window = false">Отмена</button>
                    <button class="btn send" @click="sendMessPhoto">Отправить</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'WindowFooter',

    props: {
        sendId: Number,
    },

    data() {
        return {
            message: '',
            photo: '',
            comment: '',
            window: false,
        }
    },

    methods: {
        sendMess() {
            const time = `${new Date().getHours()}:${new Date().getMinutes()}`
            if (this.message.length > 0) {
                const mess = {};
                mess.body = this.message.trim()
                mess.sendId = this.sendId
                mess.time = time
                this.$emit('new-mess', mess)
                this.message = ''
            }
        },
        sendMessPhoto() {
            const time = `${new Date().getHours()}:${new Date().getMinutes()}`
            if (this.photo.length > 0) {
                const mess = {};
                mess.body = this.comment.trim()
                mess.photo = this.photo.trim()
                mess.sendId = this.sendId
                mess.time = time
                this.$emit('new-mess', mess)
                this.message = this.photo = ''
                this.window = false
            }
        }
    }
}
</script>

<style>
.footer {
    padding: 20px;
    background: #323232;
    display: flex;
    align-items: center;
    width: 100%;
}

.footer__edit {
    flex-grow: 1;
    outline: none;
    color: #ffffff;
    background: transparent;
    border: none;
    resize: none;
    font-size: 16px;
    font-family: 'Roboto', sans-serif;
}

.footer__btn {
    width: 24px;
    height: 24px;
    cursor: pointer;
    background: transparent;
    outline: none;
    border: none;
}

.footer__window {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background: rgba(0, 0, 0, 0.35);
}

.window__body {
    width: 312px;
    padding: 24px;
    border-radius: 28px;
    background: #F2F7FF;
}

.window__title {
    color: #1C1B1F;
    font-size: 24px;
    font-weight: 400;
    line-height: 133%;
    margin-bottom: 16px;
}

.window__form {
    display: flex;
    flex-direction: column;
    gap: 16px;
}

.window__form label {
    position: relative;
}

.window__form span {
    color: #000;
    font-size: 12px;
    font-weight: 400;
    line-height: 133%;
    letter-spacing: 0.4px;
    position: absolute;
    top: 8px;
    left: 16px;
}

.window__form input,
.window__form textarea {
    border-radius: 4px 4px 0px 0px;
    background: #E2EDFF;
    border: none;
    border-bottom: 1px solid #1C1B1F;
    width: 100%;
    resize: none;
    outline: none;
    font-family: 'Roboto';
    display: flex;
    font-size: 16px;
    padding: 23px 16px 9px;
}

.window__form input::placeholder {
    color: #49454F;
    font-size: 16px;
    font-weight: 400;
    line-height: 150%;
    letter-spacing: 0.5px;
}

.window__btns {
    margin-top: 24px;
    display: flex;
    gap: 8px;
    justify-content: end;
}

.btn {
    padding: 10px 12px;
    text-align: center;
    font-family: 'Roboto';
    font-size: 14px;
    font-weight: 500;
    line-height: 143%;
    letter-spacing: 0.1px;
    text-transform: uppercase;
    border: none;
    background: transparent;
    outline: none;
    border-radius: 5px;
    cursor: pointer;
    transition: 200ms linear;
    user-select: none;
}

.btn.cancel {
    color: #CF1B1B;
}

.btn.cancel:hover {
    background: #ffdcdcda;
}

.btn.send {
    color: #6750A4;
}

.btn.send:hover {
    background: #ded5f9;
}
</style>