<template>
    <div class="item">

        <div v-on:click="$emit('removeItem', item)" class="remove">
        <svg width="32" height="32">       
            <image style="filter: invert(100%) sepia(0%) saturate(7497%) hue-rotate(116deg) brightness(109%) contrast(98%);" xlink:href="https://upload.wikimedia.org/wikipedia/commons/9/9a/%D0%98%D0%BA%D0%BE%D0%BD%D0%BA%D0%B0_%D0%BC%D1%83%D1%81%D0%BE%D1%80%D0%BA%D0%B8.svg" width="32" height="32"/>    
        </svg>
        </div>
        <img :src=item.itemImgURL alt="Error">
        <div class="item-info">
            <h3>{{item.itemName}}</h3>
            <p>{{item.itemInfo}}</p>
            <h2>{{(item.itemPrice).toLocaleString()+"p"}}</h2>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        item: {
           type: Object,
           required: true 
        }
    },

}
</script>

<style lang="scss" scoped>

    $text-color: #3F3F3F;

    .item:hover .remove{
        display: block;
    }

    .item:hover {
        outline: $text-color solid 2px;
    }

    .remove:hover {
        outline: #965050 solid 2px;
    }

    .item {

        display: flex;
        flex-direction: column;
        position: relative;
        box-sizing: border-box;
        margin-left: 36px;
        margin-bottom: 16px;
        width: 332px;
        height: 423px;
        background: #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 4px;

        .remove {

            background: #FF8484;
            box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
            width: 32px;
            height: 32px;

            position: absolute;
            left: 316px;
            top: -16px;

            display: none;

        }

        img {

            width: 100%;
            height: 200px;
            border-radius: 4px;
            border-bottom-left-radius: 0px;
            border-bottom-right-radius: 0px;
        }

        .item-info {
            box-sizing: border-box;
            height: 223px;
            display: flex;
            flex-direction: column;
            justify-content: flex-start;
            padding-left: 16px;
            padding-right: 16px;
            padding-top: 16px;
            padding-bottom: 24px;

            p {
                font-family: 'Source Sans Pro';
                font-style: normal;
                font-weight: 400;
                font-size: 16px;
                line-height: 20px;
                color: $text-color;
            }

            h3 {
                margin: 0px;
                font-family: 'Source Sans Pro';
                font-style: normal;
                font-weight: 600;
                font-size: 20px;
                line-height: 25px;
                color: $text-color;
            }

            h2 {
                margin: 0px;
                margin-top: auto;
                font-family: 'Source Sans Pro';
                font-style: normal;
                font-weight: 600;
                font-size: 24px;
                line-height: 30px;
                color: $text-color;
            }
        }
    }

    @media (max-width: 740px) {
        .item {
            margin-left: 0px;
        }
    }
</style>