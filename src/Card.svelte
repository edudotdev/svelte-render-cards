<script>
  export let name, image
</script>

<div>
  <img src={image} alt={name} loading='lazy' />
  <h2>{name}</h2>
</div>

<style>
  div {
    display: flex;
    flex-direction: column;
    gap: 10px;
    background: #f5f5f5;
    border-radius: 10px;
    padding: 10px;
  }

  img {
    border-radius: 10px;
  }

  h2 {
    margin: 0;
  }
</style>