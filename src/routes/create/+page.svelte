<script>
  import Header from "$lib/Header.svelte";
  import { addfarm, getfarms } from "$lib/db.js";
  import { goto } from "$app/navigation";
  import { user } from "$lib/state.svelte.js";
  import { landScape } from "$lib/state.svelte.js";

  // let farms = getfarms();

  let newfarm = {
    paddockLandscape: {
      steep: false,
      stoney: false,
      wet: false,
    },
  };

  let newHerd = {
    herdName: "",
    herdSize: "",
  };

  let newPaddock = {
    paddockNumber: "",
    paddockSize: "",
    paddockLandscape: "",
    lastGrazed: "",
    lastFertilised: "",
    currentPlantation: "",
  };
</script>

<!-- all newfarm should be newFarm -->

<Header />

<main class="content section">
  <!-- {#await farms}
    <p>Loading...</p>
  {:then farms}
    {#each farms as farm}
      <p>
        {farm.nameFarm}
        {farm.farmSize}
        {farm.herdNames}
        {farm.herdSize}
        {farm.paddockNumber}
        {farm.paddockSize}
        {farm.paddockLandscape}
        {farm.lastGrazed}
        {farm.lastFertilised}
        {farm.currentPlantation}
      </p>
    {/each}
  {/await} -->
  <div class="box">
    <h2>Farm</h2>
    <label class="label">
      Name Your Farm <input type="text" bind:value={landScape.nameFarm} />
    </label>

    <label class="label">
      What size is your farm in m2 <input
        type="number"
        bind:value={landScape.farmSize}
      />
    </label>
  </div>

  <div class="box">
    <h2>Herds</h2>
    <label class="label">
      Herd Name: <input type="" bind:value={newHerd.herdName} />
    </label>

    <label class="label">
      What is the size of this herd? <input
        type="dates"
        bind:value={newHerd.herdSize}
      />
    </label>

    <button
      class="button"
      on:click={() => {
        landScape.herds = [...landScape.herds, { ...newHerd }];
        newHerd.herdName = "";
        newHerd.herdSize = "";
      }}
    >
      Save Herd
    </button>
    {#each landScape.herds as herd}
      <div class="box">
        <p>Herd:{herd.herdName}</p>
        <p>Size:{herd.herdSize}</p>
      </div>
    {/each}
  </div>

  <div class="box">
    <h2>Paddocks</h2>
    <label class="label">
      Paddock Number: <input
        type="number"
        bind:value={newPaddock.paddockNumber}
      />
    </label>

    <label class="label">
      Size of paddock in m2 <input
        type="number"
        bind:value={newPaddock.paddockSize}
      />
    </label>

    <label class="landscape">
      Landscape of paddock
      <button
        class="button"
        on:click={() => {
          newPaddock.paddockLandscape.steep = true;
        }}
        class:is-success={newPaddock.paddockLandscape.steep}
      >
        Steep
      </button>
      <button
        class="button"
        on:click={() => {
          newPaddock.paddockLandscape.stoney = true;
        }}
        class:is-success={newPaddock.paddockLandscape.stoney}
      >
        Stoney
      </button>
      <button
        class="button"
        on:click={() => {
          newPaddock.paddockLandscape.wet = true;
        }}
        class:is-success={newPaddock.paddockLandscape.wet}
      >
        Wet
      </button>
    </label>

    <label class="label">
      When was this paddock last grazed? <input
        type="dates"
        bind:value={newPaddock.lastGrazed}
      />
    </label>

    <label class="label">
      When was this paddock last fertilised? <input
        type="dates"
        bind:value={newPaddock.lastFertilised}
      />
    </label>

    <label class="label">
      What is the current plantation in this paddock? <input
        type=""
        bind:value={newPaddock.currentPlantation}
      />
    </label>

    <button
      class="button"
      on:click={() => {
        landScape.paddocks = [...landScape.paddocks, { ...newPaddock }];
        newPaddock = {
          paddockNumber: "",
          paddockSize: "",
          paddockLandscape: "",
          lastGrazed: "",
          lastFertilised: "",
          currentPlantation: "",
        };
        // scrollTo("/paddockNumber");
        //is that the right scroll to command
      }}
    >
      Save Paddock
    </button>
    {#each landScape.paddocks as paddock}
      <div class="box">
        <p>Paddock:{paddock.paddockNumber}</p>
        <p>Size:{paddock.paddockSize}</p>
        <p>Landscape:{paddock.paddockLandscape}</p>
        <p>Last Grazed:{paddock.lastGrazed}</p>
        <p>Last Fertilised{paddock.lastFertilised}</p>
        <p>Plantation{paddock.currentPlantation}</p>
      </div>
    {/each}
  </div>

  <div class="box">
    <!-- somehing here needs to same it to the user -->
    <button
      class="button"
      on:click={() => {
        landScape.farm = newfarm;
        addfarm(user);
        goto("/yourfarm");
      }}
    >
      Create Farm
    </button>
  </div>
</main>

<footer class="footer">
  <p class="has-text-centered">&copy; Craighead Diocesan School 2025</p>
</footer>
