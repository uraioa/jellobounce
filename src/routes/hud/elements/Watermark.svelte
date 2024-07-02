<div class="watermark">jello</div>
<div class="shaderfix"></div>

<style lang="scss">
    .watermark {
        //position: fixed;
        //top: 15px;
        //left: 15px;
        font-family: Borel;
        color: rgba(white, 0.9);
        font-size: 50px;
        z-index: 1;
        text-shadow: 0px 0px 15px rgba(black, 0.5);
    }

    .shaderfix {
        top: -15px;
        left: -15px;
        position: absolute;
        background-color: rgba(black, 0.1);
        width: 1920px;
        height: 1080px;
        z-index: -2;
        border-radius: 12px;
    }
</style>
