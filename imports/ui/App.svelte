<script>
  import {useTracker} from 'meteor/rdb:svelte-meteor-data';
  import {Resolutions} from '../api/resolutions';
  import {LoginWindow, Logout} from 'meteor/levelup:svelte-accounts-ui';
  import Resolution from './resolutions/Resolution.svelte'

  let newRes = "";
  $: resolutions = useTracker(() => Resolutions.find({}).fetch());
  $: user = useTracker(() => Meteor.user());

  const handleSubmit = event => {
    Resolutions.insert({
      title: newRes
    })

    newRes = ""
  };

</script>

<header>
  <h1>Balpreet Singh is learning svelte</h1>
  {#if $user?._id}
    <Logout />
  {:else}
    <LoginWindow />
  {/if}
  <br>
  <br>
  <form on:submit|preventDefault={handleSubmit} >
    <input type="text" placeholder="Add your resolution" bind:value={newRes} >
    <button>Submit</button>
  </form>

  {#each $resolutions as resolution }
    <Resolution {resolution} />
  {/each}
</header>