<script>
  import { onMount } from 'svelte';
  import auth from '$lib/services/authService';
  import { isAuthenticated, user } from '$lib/store/authentication';

  // Components
  import Button from '$lib/components/Button/Button.svelte';

  // Styles
  import 'normalize.css';
  import '$lib/styles/global.scss';

  let auth0Client;

  onMount(async () => {
    auth0Client = await auth.createClient();

    isAuthenticated.set(await auth0Client.isAuthenticated());
    user.set(await auth0Client.getUser());
  });

  function login() {
    auth.loginWithPopup(auth0Client);
  }

  function logout() {
    auth.logout(auth0Client);
  }
</script>

<nav>
  <h1>Canvas</h1>
  {#if !$isAuthenticated }
    <Button on:click={login}>
      Login
    </Button>
  {/if}

  {#if $isAuthenticated}
    <div class="user">
      <p>{$user.email}</p>
      <Button on:click={logout}>
        Log out
      </Button>
    </div>
  {/if}
</nav>

<slot></slot>

<style lang="scss">
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;

    .user {
      display: flex;
      align-items: center;
      gap: 1rem;

      p {
        font-weight: 600;
        margin: 0;
      }
    }
  }
</style>
