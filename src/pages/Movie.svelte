<script>
  import { fetchMovie } from './../api';
  import { onMount } from 'svelte';
  import { fade } from 'svelte/transition';

  // 컴포넌츠
  import Navigation from './../components/Navigation.svelte';
  import Spinner from './../components/Spinner.svelte';
  import MovieInfo from './../components/MovieInfo.svelte';
  import MovieInfoBar from './../components/MovieInfoBar.svelte';
  import Actor from './../components/Actor.svelte';
  import Grid from './../components/Grid.svelte';

  export let params;

  let isLoading;
  let error;
  let movie;

  const handleFetchMovie = async () => {
    try {
      isLoading = true;
      error = false;
      movie = await fetchMovie(params.id);
    } catch (err) {
      error = true;
    }

    isLoading = false;
  };

  onMount(async () => {
    const localMovie = window.localStorage.getItem(params.id);
    if (localMovie) {
      console.log('localStorage에서 가져오기');
      movie = JSON.parse(localMovie);
    } else {
      console.log('API에서 가져오기');
      handleFetchMovie();
    }
  });

  $: {
    if (movie) {
      window.localStorage.setItem(params.id, JSON.stringify(movie));
    }
  }
</script>

{#if error}
  <p>뭔가 잘못됐네요.</p>
{:else if movie}
  <div transition:fade={{ duration: 300 }}>
    <Navigation movie={movie.original_title} />
    <MovieInfo {movie} />
    <MovieInfoBar
      time={movie.runtime}
      budget={movie.budget}
      revenue={movie.revenue}
    />
    <Grid header="배우들">
      {#each movie.actors as actor}
        <Actor {actor} />
      {/each}
    </Grid>
  </div>
{/if}

<!-- 로딩 중에는 스피너 실행 -->
{#if isLoading}
  <Spinner />
{/if}

<style>
</style>
