<script>
  import Palette from '$lib/components/Palette/Palette.svelte';
  import Canvas from '$lib/components/Canvas/Canvas.svelte';

  let colors = ['#C2185B', '#212121'];
  let chosenColor;
</script>

<div class="wrapper">
  <section class="cavas">
    <Palette
      colors={colors}
      bind:chosenColor={chosenColor}
    />
    
    <Canvas
      width={500}
      height={500}
      color={chosenColor}
    />
  </section>
</div>

<style lang="scss">
  .wrapper {
    display: flex;
    width: 100%;
    height: 100%;
    justify-content: center;
    align-items: center;
  }
</style>
