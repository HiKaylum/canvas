<script>
  import { GetColorName } from 'hex-color-to-color-name';
  import { isAuthenticated } from '$lib/store/authentication';

  export let colors = [];
  export let chosenColor = colors[0];
</script>


<div class="palette">
  {#each colors as color}
    <label
      style:background={color}
      class:selected={color === chosenColor}
      alt={GetColorName(color)}
    >
      
      <input
        type="radio"
        bind:group={chosenColor}
        value={color}
      >
    </label>
  {/each}

  {#if !$isAuthenticated}
    <p>You must be logged in to draw!</p>
  {/if}
</div>

<style lang="scss">
  .palette {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin: 0 0 1rem;

    label {
      width: 1.5rem;
      height: 1.5rem;
      border-radius: 100%;
      border: 1px solid #f1f1f1;
      transition: transform .3s ease-in-out;

      &.selected {
        transform: scale(1.25);
      }

      &:hover {
        cursor: pointer;
      }

      input {
        display: none;
      }
    }
  }
</style>


