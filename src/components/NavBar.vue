<template>
    <div class="navbar">
        <h1>Rick and Morty</h1>
    </div>
</template>

<script>
    export default{
        name: 'NavBar',
    }
</script>

<style scoped>
.navbar{
    display:block;
    width: 70%;
    margin: 0 auto;
    padding:16px 15%;
    border-bottom: solid 1px #ebebeb;
    margin-bottom: 40px;
}

h1{
    color: #6e6e6e
}
</style>