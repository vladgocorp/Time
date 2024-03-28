<script>
  import weatherImage from "$lib/images/weather.png";
</script>

<header>
  <div class="corner">
    <a href="https://weather-app-xi-dun.vercel.app">
      <img src={weatherImage} alt="wheater" />
      <h1>Do you want to know your temperature?</h1>
      <h2>Tap the image above</h2>
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
    align-items: center;
  }

  .corner {
    width: 1em;
    height: 1em;
  }

  .corner img {
    width: 5em;
    height: 6em;
    object-fit: contain;
  }

  h1 {
    color: black;
    font-size: 10px;
    line-height: 0;
    width: 8px;
    height: 10px;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  h2 {
    color: black;
    font-size: 10px;
    line-height: 0;
    width: 8px;
    height: 10px;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .footer {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    background-color: #333;
    color: white;
    text-align: center;
    padding: 20px;
    z-index: 999;
  }
</style>
