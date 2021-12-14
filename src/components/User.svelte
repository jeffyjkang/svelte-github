<script lang='ts'>
  import {UserType} from '../types';
  export let username: UserType['login'];
  export let avatar: UserType['avatar_url'];
</script>

<div class='wrapper'>
  <img src={avatar} alt={`${username}-${avatar}`}>
  <h3>{username}</h3>
</div>
        
<style>
  .wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 15%;
    margin: 20px;
    border: 1px dashed gray;
    border-radius: 10px;
  }
  img {
    max-width: 50px;
  }
  h3 {
    margin: 0;
  }
</style>

