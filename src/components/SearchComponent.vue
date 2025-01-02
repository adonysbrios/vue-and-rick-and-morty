<template>
    <section>
        <div class="separator">
            <div>
                <input class="inp" @input="(e) => name_ = e.target.value" id="search" type="text">
                <button class="btn" @click="change(name_)">Search</button>
            </div>
            <div>
                <button v-show="prev" @click="fetchC(prev)">
                    <img width="15" src="/Back.png" alt="">
                </button>
                <button v-show="next" @click="fetchC(next)">
                    <img width="15" src="/Forward.png" alt="">
                </button>
            </div>
        </div>
    </section>
</template>

<style scoped>

section{
        width: 70%;
        margin: 0 auto;
        padding: 5px 15%;
        margin-bottom: 10px;
        justify-content: end;
        display: flex;
    }

@media screen and (max-width: 500px) {

    section{
        width: 100%;
        box-sizing: border-box;
    }

}

    div{
        display: flex;
        margin: 10px 0;
        justify-content: end;
    }

    .separator{
        display: block;
    }

    input{
        border: 1px solid #ebebeb;
        border-radius: 8px;
        padding: 5px;
    }

    button {
        border: 1px solid #ebebeb;
        border-radius: 8px;
        background-color: #fff;
        color:#2e2e2e;
        padding: 10px;
        margin-left: 2px;
        margin-right: 2px;
    }

    .inp{
        border-top-right-radius: 0px;
        border-bottom-right-radius: 0px;
    }

    .btn{
        border-top-left-radius: 0px;
        border-bottom-left-radius: 0px;
        margin:0
    }
</style>

<script>
    export default{
        name:'SearchComponent',
        props: ['change', 'prev', 'next', 'fetchC'],
        data(){
            return {
                name_: ''
            }
        },
    }
</script>