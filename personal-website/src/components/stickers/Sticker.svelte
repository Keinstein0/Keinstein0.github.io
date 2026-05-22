<script lang="js">
    let {
        pinImage,
        postItImage,
        postItScale = 60,
        children,
        fontSizeMultiplier = 1
    } = $props();
</script>

<div class="container" style="--postit-width: {postItScale}%; --post-it-texture: url({postItImage.src})">
    <img src={pinImage.src} class="pin-img" alt="Pin holding the post-it">

    <img src={postItImage.src} class="postit-background" alt="Post-it note background">

    <div class="text-container" style="--fontSizeMultiplier: {fontSizeMultiplier}">
        <div class="text-content">
            {@render children?.()}
        </div>
    </div>
</div>

<style>
    @font-face {
        font-family: 'handwritten'; /* Name the font family */
        src: url('../../assets/fonts/dreaming-outloud-pro-regular.otf'); /* Path to the font file */
    }

    .container {
        container-type: inline-size;
        position: relative;
        
        width: var(--postit-width);
        max-width: 380px;
        min-width: 200px;
        
        box-sizing: border-box;
        transition: transform 20ms;
    }

    .postit-background {
        width: 100%;
        height: auto;
        display: block;
    }

    @media (max-width: 768px) {
        .container {
            min-width: 240px; 
            max-width: 320px; 
        }
    }

    .container:hover{
        transform: rotate(3deg);
    }

    .pin-img {
        position: absolute;
        top: -3%; 
        left: 50%;
        transform: translateX(-50%);
        width: 20cqw;
        height: auto;
        z-index: 10;
    }


    .text-container {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        box-sizing: border-box;
        
        display: grid;
        place-items: top; 
        padding: 8cqw; 
        padding-top: 10cqw; 
    }

    .text-content{
        font-size: clamp(0.75rem, 7cqw, 1.45rem);
        font-family: handwritten;

        padding: 4cqw;
        padding-top: 0;
        text-align: center;
        word-break: break-word; 

        width: 100%;
        box-sizing: border-box;
    }

    .text-content :global(*) {
        margin: 0 0 0.4em 0;
        word-break: break-word;

    }
    .text-content :global(*:last-child) {
        margin-bottom: 0;
    }

    /* Headings scale proportionally based on the base fluid size via 'em' */
    .text-content :global(h1) {
        font-size: calc(1.4em * var(--fontSizeMultiplier)); /* 1.4x larger than the base font-size */
        font-weight: bold;
        line-height: 1.2;
    }

    .text-content :global(h2) {
        font-size: calc(1.2em * var(--fontSizeMultiplier));
        font-weight: bold;
        line-height: 1.2;
    }

    /* Paragraphs match the base fluid size perfectly */
    .text-content :global(p) {
        font-size: calc(1.0em * var(--fontSizeMultiplier));
        line-height: 1.35;
    }

    .text-content :global(small) {
        font-size: calc(0.8em * var(--fontSizeMultiplier));
    }
</style>