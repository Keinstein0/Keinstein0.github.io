<script lang="js">
    let {
        pinImage,
        postItImage,
        postItScale = 100,
        children,
        fontSizeMultiplier = 1,
        maxRotation = 6, // max 6 degrees left or right
        maxOffset = 4  // max 10px shift
    } = $props();

    const randomRotate = (Math.random() * maxRotation * 2 - maxRotation).toFixed(1);
    const randomX = (Math.random() * maxOffset * 2 - maxOffset).toFixed(4);
    const randomY = (Math.random() * maxOffset * 2 - maxOffset).toFixed(4);

    const hoverModifier = randomRotate < 0 ? -3 : 3;

</script>

<div class="container" style="
    --postit-width: {postItScale}%;
    --post-it-texture: url({postItImage.src});
    --base-rotate: {randomRotate}deg;
    --hover-rotate: {parseFloat(randomRotate) + hoverModifier}deg;
    --x-offset: {randomX}vw;
    --y-offset: {randomY}vh;
    ">
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

        transform: rotate(var(--base-rotate)) translate(var(--x-offset), var(--y-offset));
        transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.3s ease;
        
        width: var(--postit-width);
        max-width: 660px;
        min-width: 200px;
        
        
        box-sizing: border-box;
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
        transform: rotate(var(--hover-rotate)) translate(var(--x-offset), var(--y-offset)) scale(1.03);
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

    .text-content :global(h1) {
        font-size: calc(1.4em * var(--fontSizeMultiplier)); 
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

    .text-content :global(li) {
        font-size: calc(1.0em * var(--fontSizeMultiplier));
        line-height: 1.02;
        text-align: left;
    }

    .text-content :global(small) {
        font-size: calc(0.8em * var(--fontSizeMultiplier));
    }
</style>