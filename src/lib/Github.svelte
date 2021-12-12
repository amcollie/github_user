<script>
  import { onMount } from 'svelte'

  let users = []
  let loading = true

  onMount(async () => {
    let userData = await fetch('https://api.github.com/users')

    let githubUsers = await userData.json()
    users = githubUsers

    loading = false
  })
</script>

{#if loading }
  <h2>Loading...</h2>
{:else}
  <section>
    {#each users as user (user.id)}
      <article class="user">
        <img src="{user.avatar_url}" alt="{user.login}">
        <div class="user-info">
          <h3>User: {user.login}</h3>
          <a href="{user.html_url}" class="btn btn-primary" target="_blank">github url</a>
        </div>
      </article>
    {/each}
  </section>
{/if}

<style>
  h2 {
    text-align: center;
  }

  .user {
    margin: 2rem 0;
    box-shadow: var(--lightShadow);
    display: grid;
    grid-template-columns: auto 1fr;
    border-radius: var(--mainBorderRadius);
    column-gap: 2rem;
    background: var(--mainWhite);
  }

  .user img {
    width: 6rem;
    border-top-left-radius: var(--mainBorderRadius);
    border-bottom-left-radius: var(--mainBorderRadius);
  }

  .user-info {
    padding-top: 0.75rem;
  }

  .user-info h3 {
    margin-bottom: 0.75rem;
  }
</style>