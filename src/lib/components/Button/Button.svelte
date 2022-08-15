<script>
  export let click;
  export let large = false;
</script>

<button
  on:click={click}
  class:large
>
  <slot></slot>
</button>

<style lang="scss">
  button {
    cursor: pointer;
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 0.25rem;
    background-color: var(--accent-color);
    color: var(--text-primary-color);

    transition: box-shadow .5s ease-in-out;

    &.large {
      padding: 0.75rem 1.5rem;
      font-size: 1.25rem;
    }

    &:hover {
      box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
    }
  }
</style>
