<template>
    <div id="app">
        <h1>Calculadora</h1>
        <Calculator></Calculator>
    </div>
</template>

<script>
    import Calculator from './main/Calculator'

    export default {
        components: { Calculator }
    }
</script>

<style>
    @font-face {
        font-family: "RobotoMono";
        src: url("./fonts/RobotoMono-Thin.ttf");
    }

    * {
        font-family: "RobotoMono", monospace;
    }

    body {
        margin: 0;
    }

    #app {
        display: flex;
        flex-direction: column;
        height: 100vh;
        justify-content: center;
        align-items: center;
        text-align: center;
        
        background: #355C7D;
        background: -webkit-linear-gradient(to right, #C06C84, #6C5B7B, #355C7D);
        background: linear-gradient(to right, #C06C84, #6C5B7B, #355C7D);

    }
</style>
