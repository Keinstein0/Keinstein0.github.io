<script lang="js">
    let {
        image,
        href,
        text,
        maxRotation = 6, // max 6 degrees left or right
        maxOffset = 2  // max 2vh shift
    } = $props();

    const randomRotate = (Math.random() * maxRotation * 2 - maxRotation).toFixed(1);
    const randomX = (Math.random() * maxOffset * 2 - maxOffset).toFixed(4);
    const randomY = (Math.random() * maxOffset * 2 - maxOffset).toFixed(4);

    const hoverModifier = randomRotate < 0 ? -3 : 3;
</script>

<div class="container"
style="
--base-rotate: {randomRotate}deg;
--hover-rotate: {parseFloat(randomRotate) + hoverModifier}deg;
--x-offset: {randomX}vw;
--y-offset: {randomY}vh;
">
    <a href = {href}>
        <p><strong>{text}</strong></p>
        <img src={image.src} class="sticker-img" alt="{text} sticker">
    </a>
</div>

<style>
    .container {
        box-sizing: border-box;
        padding: 4cqw;
        padding-top: 0cqw; 
        transition: transform 20ms;
        opacity: 0.75;

        transform: rotate(var(--base-rotate)) translate(var(--x-offset), var(--y-offset));
        transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.3s ease;
    }


    .sticker-img {
        width: 33%;
        height: auto;
        display: block;

    }

    a {
        text-decoration: none;
        color: black;
        display: flex;
        flex-direction: column;
        align-items: center;
        width: fit-content;
    }

    a:hover {
        text-decoration: underline;
        color: #00028a;
    }

    a:hover .sticker-img {
        filter: invert(8%) sepia(100%) saturate(7087%) hue-rotate(247deg) brightness(58%) contrast(142%);
    }

    p {
        text-align: center;
        margin-top: 0.5em;
        font-family: 'handwritten', cursive; /* Use the handwritten font */
        font-size: 24px;

        
    }
</style>
