<script lang='ts'>
  import {UserType} from '../types';
  import User from './User.svelte';
  let user: UserType;
  let query: '';

  const handleSubmit = async () => {
    try {
      let res = await fetch(`https://api.github.com/users/${query}`);
      if (!res.ok) {
       throw new Error(`HTTP error, status: ${res.status}`);
      }
      let data = await res.json();
      user = data;
    }
    catch(e) {
      console.log(e);
    }
  }
</script>

<div class='search-container'>
  <form on:submit|preventDefault={handleSubmit}>
    <input type='text' bind:value={query}>
    <button>Search</button>
  </form>
  {#if user}
    <div class='user-container'>
      <User username={user.login} avatar={user.avatar_url} />
    </div>
  {/if}
</div>

<style>
  .search-container {
    padding: 20px;
    background: #eee;
    border-radius: 10px;
    margin-bottom: 40px;
  }
  .user-container {
    display: flex;
    justify-content: center;
  }
</style>

