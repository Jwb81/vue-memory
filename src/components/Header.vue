<template>
    <div class="navbar">
        <ul>
            <!-- logo -->
            <li class='brand'>React Memorization</li>

            <!-- title -->
            <li>{{ message }}</li>

            <!-- scores -->
            <li>Score: {{ currentScore }} | Top Score: {{ topScore }}</li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'Header',
    props: {
        message: String,
        currentScore: Number,
        topScore: Number
    }
}
</script>



<style scoped>
.navbar {
    position: fixed;
    top: 0;
    z-index: 5;
    width: 100%;
    padding: 0;
    background-color: #5133a4;
    font-size: calc(10px + 14 * (100vw - 320px)/ 800);

    color: white;

    box-shadow: 0 10px 20px black;
}

ul {
    width: 100%;
    padding: 0;
    margin: 0;
}

.navbar li {
    display: inline-block;
    width: 33.3%;
    text-align: center;
    padding: 25px 0px;
    /* overflow-x: visible; */
}

.brand {
    font-weight: bold;
}

</style>
