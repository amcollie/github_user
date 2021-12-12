<script>
  async function getUsers() {
    let userData = await fetch('https://api.github.com/users')

    let githubUsers = await userData.json()
    return githubUsers
  }
</script>

<section>
  {#await getUsers() }
    <h1>Loading...</h1>
  {:then users}
    {#each users as user (user.id)}
      <article class="user">
        <img src="{user.avatar_url}" alt="{user.login}">
        <div class="user-info">
          <h3>User: {user.login}</h3>
          <a href="{user.html_url}" class="btn btn-primary" target="_blank">github url</a>
        </div>
      </article>
    {/each}
  {:catch error }
    <p>Something went wrong: {error.message}</p>
  {/await}
</section>

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