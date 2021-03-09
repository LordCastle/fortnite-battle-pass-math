<template>
    <div id="app">
        <calculator />
    </div>
</template>

<script>
import Calculator from "./components/calculator.vue";

export default {
    name: "App",
    components: {
        // HelloWorld,
        Calculator
    }
};
</script>

<style lang="scss">
* {
    box-sizing: border-box;
}

body {
    background-color: #2a2a2a;
    color: #fff;
    margin: 0;
    padding: 0;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
}

strong {
    color: #ff0;
    font-size: 1.1rem;
}
</style>
