<script lang="js">
    let {
        pinImage,
        postItImage,
        postItScale = 30,
        children
    } = $props();
</script>

<div class="container" style="--postit-width: {postItScale}%; --post-it-texture: url({postItImage.src})">
    <img src={pinImage.src} class="pin-img" alt="Pin holding the post-it">

    <div class="text-container">
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

        display: grid;

        grid-template-rows: auto; 
        
        width: var(--postit-width);
        max-width: 380px;
        min-width: 200px;

        aspect-ratio: 1 / 1; 

        background-image: var(--post-it-texture);
        background-size: contain;
        background-position: center;
        background-repeat: no-repeat;
        
        box-sizing: border-box;

        padding: 4cqw;

        transition: 20ms;
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
        top: 0;
        left: 50%;
        transform: translate(-50%, -30%);

        width: 20cqw;
        height: fit-content;


        margin-top: 8px;
        z-index: 2;
    }

    .text-container {
        display: grid;
        place-items: top;
        width: 100%;
        height: 100%;
        box-sizing: border-box;

        padding-top: 0rem;
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
        font-size: 1.4em; /* 1.4x larger than the base font-size */
        font-weight: bold;
        line-height: 1.2;
    }

    .text-content :global(h2) {
        font-size: 1.2em;
        font-weight: bold;
        line-height: 1.2;
    }

    /* Paragraphs match the base fluid size perfectly */
    .text-content :global(p) {
        font-size: 1em; 
        line-height: 1.35;
    }

    .text-content :global(small) {
        font-size: 0.8em;
    }
</style>