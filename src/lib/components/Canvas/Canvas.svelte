<script>
  import { onMount } from 'svelte';
  import { isAuthenticated } from '$lib/store/authentication';

  export let width = 150;
  export let height = 150;
  export let color = '#1d1d1d';

  let canvas;
  let ctx;
  let coord = { x: 0, y: 0 };

  onMount(() => {
    ctx = canvas.getContext('2d');
    canvas.addEventListener('mousedown', onMouseDown);
    canvas.addEventListener('mouseup', onMouseUp);
  });

  function reposition(event) {
    coord.x = event.clientX - canvas.offsetLeft;
    coord.y = event.clientY - canvas.offsetTop;
  }

  function onMouseDown(event) {
    canvas.addEventListener("mousemove", draw);
    reposition(event);
  }

  function onMouseUp() {
    canvas.removeEventListener("mousemove", draw);
  }

  function draw(event) {
    if (!$isAuthenticated) return;

    ctx.beginPath();
    ctx.strokeStyle = color;
    ctx.moveTo(coord.x, coord.y);
    reposition(event);
    ctx.lineTo(coord.x, coord.y);
    ctx.stroke();
  }
</script>

<canvas
  bind:this={canvas}
  width={width}
  height={height}>
</canvas>

<style lang="scss">
  canvas {
    background-color: #FFFFFF;
    z-index: 2;
  }
</style>
