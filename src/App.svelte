<script lang="ts">
  import {onMount} from 'svelte';
  import {UserType} from './types';
  import UserSearch from './components/UserSearch.svelte';
  import User from './components/User.svelte';
  
  let users: UserType[];

  const getGitHubUsers = async () => {
    try {
      let res = await fetch('https://api.github.com/users');
      if (!res.ok) {
        throw new Error(`HTTP error, status: ${res.status}`);
      }
      let data = await res.json();
      return data;
    }
    catch(e) {
      console.log(e);
    }
  };
  onMount(async () => {
    const data = await getGitHubUsers()
    if (data) {
      users = data;
    }
  });
</script>

<main>
  <UserSearch />
  {#if users}
    <div class='container'>
      {#each users as user}
          <User username={user.login} avatar={user.avatar_url} />
      {/each}
    </div>
  {/if}
</main>

<style>
  .container {
    margin: 0;
    padding: 0;
    display: flex;
    flex-flow: wrap;
  }
</style>

