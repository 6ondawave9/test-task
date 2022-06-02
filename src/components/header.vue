<template>
    <header>
        <h1>Добавление товара</h1>
        <select v-model="selected" v-on:change="$emit('sorting', selected)">
            <option value="" disabled>По умолчанию</option>
            <option>По наименованию</option>
            <option>По возрастанию цены</option>
            <option>По убыванию цены</option>
        </select>
    </header>
    </template>

    <script>
    export default {
        data() {
            return {
                selected: ''
            }
        }
    }
    </script>

<style scoped lang="scss">
    header {

        align-items: center;
        display: flex;

        h1 {
            font-family: 'Source Sans Pro';
            font-style: normal;
            font-weight: 600;
            font-size: 28px;
            line-height: 35px;
            color: #3F3F3F; 
        }

        select {
            font-family: 'Source Sans Pro';
            font-style: normal;
            font-weight: 400;
            font-size: 12px;
            line-height: 15px;
            color: #B4B4B4;
            text-align: center;

            margin-left: auto;
            width: 121.49px;
            height: 36px;
            border: none;
            background: #FFFEFB;
            box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
            border-radius: 4px;
        }
    }
</style>