<template>
<div>
    <div class="leftSide"></div>
    <div class="rightSide"></div>
    <a class="about"></a>
    <about-section />
</div>
</template>

<script>
import AboutSection from "./AboutSection"
export default {
    data: function() {
    return {
    }
    },
    methods: {

    },
    components: {
        AboutSection,
    }
}
</script>

<style>
    .leftSide {
        height: 2000px;
        width: 10%;
        position: fixed;
        left: 0;
        background-color: #070707;
        z-index: 100;
        position: fixed;
        margin-top: 0;
        overflow: hidden;
        top: 0;
    }
    .rightSide {
        height: 2000px;
        width: 10%;
        position: fixed;
        right: 0;
        background-color: #070707;
        z-index: 100;
        position: fixed;
        margin-top: 0;
        overflow: hidden;
        top: 0;
    }
    @media only screen and (max-width: 1000px) {
    .rightSide, .leftSide {
        display: none;
    }

}
</style>
