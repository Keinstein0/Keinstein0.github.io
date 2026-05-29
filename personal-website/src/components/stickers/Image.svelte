<script lang="js">
    let {
        image,
        tapeImage,
        alt,
        width = 100,
        maxRotation = 6, // max 6 degrees left or right
        maxOffset = 2  // max 10px shift
    } = $props();

    const randomRotate = (Math.random() * maxRotation * 2 - maxRotation).toFixed(1);
    const randomX = (Math.random() * maxOffset * 2 - maxOffset).toFixed(4);
    const randomY = (Math.random() * maxOffset * 2 - maxOffset).toFixed(4);

    const hoverModifier = randomRotate < 0 ? -3 : 3;
</script>

<div class="container" 
style="--pic-width: {width}%;
--base-rotate: {randomRotate}deg;
--hover-rotate: {parseFloat(randomRotate) + hoverModifier}deg;
--x-offset: {randomX}vw;
--y-offset: {randomY}vh;
">
    <img src={tapeImage.src} class="tape-img" alt="Tape holding the image">

    <div class="image-container">
        <img src={image.src} class="sticker-img" alt={alt}>
    </div>
</div>

<style>
.container {
        container-type: inline-size;
        position: relative;
        display: grid;
        grid-template-rows: 1fr; 
        
        width: var(--pic-width);
        max-width: 660px;
        min-width: 200px;
        aspect-ratio: 1 / 1; 

        box-sizing: border-box;
        padding: 4cqw;
        padding-top: 0cqw; 

        transform: rotate(var(--base-rotate)) translate(var(--x-offset), var(--y-offset));
        transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.3s ease;
    }

    .container:hover{
        transform: rotate(var(--hover-rotate)) translate(var(--x-offset), var(--y-offset)) scale(1.03);
    }

    .tape-img {
        position: absolute;
        top: -3%;
        left: 50%;
        transform: translateX(-50%);
        width: 63%;
        height: auto;
        z-index: 100;

        opacity: 0.95;
    }

    .image-container {
        width: 103%;
        height: 103%;
        box-sizing: border-box;
        z-index: 2;
        overflow: hidden;

        box-shadow: -7px 7px 10px rgba(0, 0, 0, 0.5);
    }

    .sticker-img {
        width: 100%;
        height: 100%;
        
        object-fit: contain; 
        
        background-color: #000000; 
        
        display: block;

    }
</style>