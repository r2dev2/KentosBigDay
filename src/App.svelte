<script>
  import { Article } from 'spaper';

  const images = [ 'approb', 'felix', 'maid', 'matsuri' ];
  const r1 = 35 * 16;
  const r2 = 18 * 16;
  // from https://stackoverflow.com/a/44000973
  const ellipseAttrsToPath = (rx,cx,ry,cy) =>
    `M${cx-rx},${cy}a${rx},${ry} 0 1,0 ${rx*2},0a${rx},${ry} 0 1,0 -${rx*2},0 Z`;

  const ellipticalPath = ellipseAttrsToPath(r1, 0, r2, 0);
  document.documentElement.style.setProperty('--elliptical-path', `path('${ellipticalPath}')`);
</script>

<main>
  {#each images as src, i}
    <img id="kento-{i}" class="circling-image" src="./img/kento{src}.webp" alt="Circling picture of {src}" style="--pos-offset: {i * 25}%" />
  {/each}
  <div class="poem-container">
    <Article
      title="Happy 18th Birthday Kento Nishi!"
      border
    >
      <p>You are now an adult.</p>
      <p>Good job on expanding your cult.</p>
      <p>Congrats for getting noticed by your oshi, Kiara.</p>
      <p>In your deep voice, please tell me, <q>Ara Ara.</q></p>
      <p>You must do it, <i>deus lo vult.</i></p>
    </Article>
  </div>
</main>

<style>
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    overflow: hidden;
  }

  .poem-container {
    text-align: center;
  }

  p {
    margin: 0.5rem 0 0 0;
  }

  .circling-image {
    position: absolute;
    top: 50%;
    left: 50%;
    height: 6rem;
    background-color: white;
    offset-path: var(--elliptical-path);
    offset-rotate: 0deg;
    animation: followpath 30s linear infinite;
  }

  @keyframes followpath {
    from {
      offset-distance: calc(100% + var(--pos-offset));
    }
    to {
      offset-distance: var(--pos-offset);
    }
  }
</style>
