<script>
  import {Resolutions} from '../../api/resolutions';
  export let resolution;
  let updateRes = resolution.title;

  const deleteRes = () =>{
    Resolutions.remove(resolution._id)
  };

  const updateResolution = () => {
    Resolutions.update({
      _id: resolution._id
    }, {title: updateRes})
  };
</script>

<li>
  <form on:submit|preventDefault={updateResolution}>
    <input type="text" bind:value={updateRes}>
    <button>Submit</button>
  </form>
  <button on:click={deleteRes}>Delete</button>
</li>