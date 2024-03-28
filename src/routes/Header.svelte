<script>
  import weatherImage from "$lib/images/weather.png";
</script>

<header>
  <nav></nav>

  <div class="corner">
    <a href="vladgocorp.kesug.com">
      <img src={weatherImage} alt="wheater" />
    </a>
  </div>
</header>
<div class="footer">
  <h1>Social Network</h1>
  <a href="https://github.com/vladgocorp"> Go GitHub</a>
</div>

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
