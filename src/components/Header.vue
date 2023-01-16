<template>
    <header class="header">
        <span class="header-title">Weather App</span>
        <div class="header-logo-wrap">
            <img src="../assets/img/weather.png" alt="image:weather">
        </div>
    </header>
</template>

<script>
export default {
    name: 'Header'    
}
</script>

<style scoped>
.header {
    margin: 0px 0px 20px 0px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: #000;
}

.header-title {
    font-size: 1.3rem;
    font-weight: 60;
}

.header-logo-wrap {
    max-width: 60px;
    max-height: 60px;
    cursor: pointer;
}
.header-logo-wrap:hover {
    transform: rotate(360deg);
    transition: all 1s ease;
}
.header-logo-wrap img {
    width: 100%;
    height: 100%;
}
</style>