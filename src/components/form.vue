<template>
    <form @submit.prevent="onSubmit">
        <p>Наименование товара <span>&#149;</span></p>
        <input ref="name" v-on:input="validation" placeholder="Введите наименование товара" type="text" v-model="itemName">
        <p ref="warnName" class="warn hidden">Поле является обязательным</p>
        <p>Описание товара</p>
        <textarea v-on:input="validation" class="item-about-input" placeholder="Введите описание товара" type="text" v-model="itemInfo"></textarea>
        <p class="warn"></p>
        <p>Ссылка на изображение товара <span>&#149;</span></p>
        <input ref="url" v-on:input="validation" placeholder="Введите ссылку" type="text" v-model="itemImgURL">
        <p ref="warnUrl" class="warn hidden">Поле является обязательным</p>
        <p>Цена товара <span>&#149;</span></p>
        <input ref="price" v-on:input="validation" placeholder="Введите цену" type="number" v-model="itemPrice">
        <p ref="warnPrice" class="warn hidden">Поле является обязательным</p>
        <button ref="mainBtn" class="notactive" type="submit">Добавить товар</button>
    </form>
    <div class="success" ref="success">
        <h2>✓ Товар успешно добавлен</h2>
    </div>
</template>

<script>
export default {
    emits: [
        'added'
    ],
        data() {
            return {
                itemName: "",
                itemInfo: "",
                itemImgURL: "",
                itemPrice: "",
            }
        },
        methods: {
            onSubmit() {
                if (this.itemName.trim()&&this.itemImgURL.trim()&&this.itemPrice!='') {
                    const item = {
                        itemName: this.itemName,
                        itemInfo: this.itemInfo,
                        itemImgURL: this.itemImgURL,
                        itemPrice: this.itemPrice
                    }
                    this.$emit("added", item)
                    this.itemName = ''
                    this.itemInfo = ''
                    this.itemImgURL = ''
                    this.itemPrice = ''
                    this.$refs.mainBtn.classList.add('notactive')
                    this.$refs.mainBtn.classList.remove('active')
                    this.$refs.mainBtn.disabled = true
                    this.$refs.success.style.opacity = "100%"
                    setTimeout(() => this.$refs.success.style.opacity = "0%", 2000);
                }
            },
            validation() {

                if (this.$refs.name.value=="") {
                        this.$refs.name.classList.add('notvalid')
                        this.$refs.warnName.classList.remove('hidden')
                    } else {
                        this.$refs.name.classList.remove('notvalid')
                        this.$refs.warnName.classList.add('hidden')
                }
                if (this.$refs.url.value=="") {
                        this.$refs.url.classList.add('notvalid')
                        this.$refs.warnUrl.classList.remove('hidden')
                    } else {
                        this.$refs.url.classList.remove('notvalid')
                        this.$refs.warnUrl.classList.add('hidden')
                }
                if (this.$refs.price.value=="") {
                        this.$refs.warnPrice.classList.remove('hidden')
                        this.$refs.price.classList.add('notvalid')
                    } else {
                        this.$refs.price.classList.remove('notvalid')
                        this.$refs.warnPrice.classList.add('hidden')
                }

                if (this.itemName!=""&&this.itemPrice!=""&&this.itemImgURL!="") {
                    this.$refs.mainBtn.classList.remove('notactive')
                    this.$refs.mainBtn.classList.add('active')
                    this.$refs.mainBtn.disabled = false
                } else {
                    this.$refs.mainBtn.classList.add('notactive')
                    this.$refs.mainBtn.classList.remove('active')
                    this.$refs.mainBtn.disabled = true
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
form {
    box-sizing: border-box;
    flex-shrink: 0;
    display: flex;
    flex-direction: column;
    width: 332px;
    height: 440px;
    padding: 24px;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;

    p {
        font-family: 'Source Sans Pro';
        font-style: normal;
        font-weight: 400;
        font-size: 10px;
        line-height: 13px;
        letter-spacing: -0.02em;
        color: #49485E;
        margin-bottom: 4px;
        margin-top: 2px;

        span {
            color: #FF8484;
            vertical-align: text-top;
            font-size: 15px;
        }
    }

    .hidden {
        visibility: hidden;
    }

    .warn {
        font-family: 'Source Sans Pro';
        font-style: normal;
        font-weight: 400;
        font-size: 8px;
        line-height: 10px;
        letter-spacing: -0.02em;
        color: #FF8484;
        margin-bottom: 0px;
        margin-top: 4px;
    }

    %btn-input-padding {
        padding-top: 10px;
        padding-bottom: 10px;
    }

    .notvalid {
        border: 1px solid rgba(255, 132, 132, 1)
    }

    textarea {
        resize: none;
        overflow: hidden;
    }

    input:focus, textarea:focus {
        outline: #3F3F3F solid 2px;
    }

    input, textarea {

        @extend %btn-input-padding;
        padding-left: 16px;

        border: none;
        background: #FFFEFB;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;

        font-family: 'Source Sans Pro';
        font-style: normal;
        font-weight: 400;
        font-size: 12px;
        line-height: 15px;
    }

    .item-about-input {
        padding-bottom: 83px;
    }

    .active {
        color: #FFFFFF;
        background: #7BAE73;
    }

    .notactive {
        color: #B4B4B4;
        background: #EEEEEE;
    }

    button {
        @extend %btn-input-padding;

        padding-left: 95px;
        padding-right: 95px;
        margin-top: 10px;

        border: none;
        border-radius: 10px;

        font-family: 'Inter';
        font-style: normal;
        font-weight: 600;
        font-size: 12px;
        line-height: 15px;
        text-align: center;
        letter-spacing: -0.02em;
    }
}

    @media (max-width: 740px) {
        form {
            width: 100%;
            margin-bottom: 16px;
        }
    }

    .success {
        transition: all ease-in-out 0.2s;
        opacity: 0%;
        position: fixed;
        top: 90vh;
        padding: 7px;
        font-family: 'Inter';
        font-style: normal;
        font-weight: 600;
        font-size: 12px;
        line-height: 15px;
        text-align: center;
        letter-spacing: -0.02em;
        color: #FFFFFF;
        background: #7BAE73;
        border: none;
        border-radius: 10px;
    }

</style>