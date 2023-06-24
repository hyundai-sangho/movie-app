<script>
  import Movie from './Movie.svelte';
  import { fetchMovies } from './../api.js';
  import { onMount } from 'svelte';

  // Config
  import { IMAGE_BASE_URL, BACKDROP_SIZE, POSTER_SIZE } from '../config.js';

  // 컴포넌츠
  import Hero from '../components/Hero.svelte';
  import Search from '../components/Search.svelte';
  import Grid from '../components/Grid.svelte';
  import Thumb from './../components/Thumb.svelte';
  import LoadMoreButton from './../components/LoadMoreButton.svelte';
  import Spinner from './../components/Spinner.svelte';

  let movies = { movies: [] };
  let isLoading;
  let searchTerm = '';
  let error;

  const handleFetchMovies = async (loadMore, searchTerm) => {
    try {
      isLoading = true;
      error = false;
      movies = await fetchMovies(movies, loadMore, searchTerm);
    } catch (err) {
      error = true;
    }
    isLoading = false;
  };

  const handleSearch = event => {
    searchTerm = event.detail.searchText;
    movies.movies = [];
    handleFetchMovies(false, searchTerm);
  };

  const handleLoadMore = () => {
    handleFetchMovies(true, searchTerm);
  };

  onMount(async () => {
    const sessionMovies = window.sessionStorage.getItem('svelte-movies');
    if (sessionMovies) {
      console.log('SessionStorage에서 가져오기');
      movies = JSON.parse(sessionMovies);
    } else {
      console.log('API에서 가져오기');
      handleFetchMovies(false, searchTerm);
    }
  });

  $: {
    if (movies.movies.length > 0) {
      window.sessionStorage.setItem('svelte-movies', JSON.stringify(movies));
    }
  }
</script>

{#if error}
  <p>뭔가 문제가 있네요.</p>
{:else if movies.heroImage && !searchTerm}
  <Hero
    image={`${IMAGE_BASE_URL}${BACKDROP_SIZE}${movies.heroImage.backdrop_path}`}
    title={movies.heroImage.original_title}
    text={movies.heroImage.overview}
  />
{/if}

<Search on:search={handleSearch} />
<Grid header={searchTerm ? '검색 결과' : '인기 영화'}>
  {#each movies.movies as movie}
    <Thumb
      clickable
      image={movie.poster_path &&
        `${IMAGE_BASE_URL}${POSTER_SIZE}${movie.poster_path}`}
      movieId={movie.id}
    />
  {/each}
</Grid>

{#if isLoading}
  <Spinner />
{/if}

{#if !isLoading && movies.currentPage < movies.totalPages}
  <LoadMoreButton on:loadMore={handleLoadMore}>더 보기</LoadMoreButton>
{/if}

<style>
</style>
