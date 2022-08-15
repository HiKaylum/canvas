<script>
  import { onMount } from 'svelte';
  import { isAuthenticated } from '$lib/store/authentication';
  import { isCanvasDirty } from '$lib/store/canvas';

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
    document.addEventListener('keyup', nuke);

    return () => {
      canvas.removeEventListener('mousedown', onMouseDown);
      canvas.removeEventListener('mouseup', onMouseUp);
      document.removeEventListener('keyup', nuke);
    }
  });


  function nuke({ key }) {
    if (key !== 'f' || !canvas) return;

    ctx.clearRect(0, 0, canvas.width, canvas.height);
    isCanvasDirty.set(false);
  }

  function reposition(event) {
    coord.x = event.clientX - canvas.offsetLeft;
    coord.y = event.clientY - canvas.offsetTop;
  }

  function onMouseDown(event) {
    if (!$isAuthenticated) return;
    canvas.addEventListener("mousemove", draw);
    reposition(event);
  }

  function onMouseUp() {
    canvas.removeEventListener("mousemove", draw);
    isCanvasDirty.set(true);
  }

  function draw(event) {
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
