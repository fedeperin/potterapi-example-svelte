<script>
    export let character
    const { fullName, image, index, nickname } = character
</script>

<a href="/{ index }" class="card">
    <img src={ image } alt={ fullName }>

    <div class="data">
        <h3>{ fullName }</h3>
        <p>{ nickname }</p>
    </div>
</a>

<style>
    .card {
        background: #fff;
        text-decoration: none;
        color: inherit;
        transition: translate .1s ease;
    }

    .card:hover {
        translate: 0 -5px;
    }

    img {
        width: 100%;
        aspect-ratio: 1/1.5;
        object-fit: cover;
    }

    .data {
        padding: 10px;
    }
</style>