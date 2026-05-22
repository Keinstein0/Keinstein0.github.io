<script lang="js">
    let {
        image,
        tapeImage,
        alt,
        width = 100,
        height = 100
    } = $props();
</script>

<div class="container" style="--pic-width: {width}%; --pic-height: {height}%">
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
        max-width: 380px;
        min-width: 200px;
        aspect-ratio: 1 / 1; 

        box-sizing: border-box;
        padding: 4cqw;
        padding-top: 0cqw; 
        transition: transform 20ms;
    }

    .container:hover {
        transform: rotate(3deg);
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