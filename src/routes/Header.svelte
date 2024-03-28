<script>
  import weatherImage from "$lib/images/weather.png";
</script>

<header>
  <nav></nav>

  <div class="corner">
    <a href="https://vladgocorp.kesug.com">
      <img src={weatherImage} alt="wheater" />
    </a>
  </div>
</header>

<style>
  header {
    display: flex;
    justify-content: space-between;
  }

  .corner {
    width: 3em;
    height: 3em;
  }

  .corner img {
    width: 2em;
    height: 5em;
    object-fit: contain;
  }
</style>
