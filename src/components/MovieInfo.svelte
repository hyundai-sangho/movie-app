<script>
  // 컴포넌츠
  import Thumb from './Thumb.svelte';
  // Config
  import { POSTER_SIZE, IMAGE_BASE_URL, BACKDROP_SIZE } from '../config';

  const noImage = '/images/no_image.jpg';
  export let movie;
</script>

<div
  class="wrapper"
  style="--backdrop:{movie.backdrop_path
    ? `url(${IMAGE_BASE_URL}${BACKDROP_SIZE}${movie.backdrop_path})`
    : '#000'}"
>
  <div class="content">
    <div class="thumb">
      <Thumb
        image={movie.poster_path
          ? `${IMAGE_BASE_URL}${POSTER_SIZE}${movie.poster_path}`
          : noImage}
      />
    </div>
    <div class="text">
      <h1>{movie.title}</h1>
      <h3>줄거리</h3>
      <p>{movie.overview}</p>
      <div class="rating-director">
        <div>
          <h3>IMDB 평가</h3>
          <div class="score">
            {Math.round(movie.vote_average)}
          </div>
        </div>
        <div class="director">
          <h3>감독{movie.directors.length > 1 ? '들' : ''}</h3>
          {#each movie.directors as director}
            <p>{director.name}</p>
          {/each}
        </div>
      </div>
    </div>
  </div>
</div>

<style>
  .wrapper {
    background: var(--backdrop);
    background-size: cover;
    background-position: center;
    width: 100%;
    padding: 40px 20px;
    box-sizing: border-box;
    animation: animateMovieinfo 1s;
  }

  .content {
    max-width: 1280px;
    min-height: 450px;
    margin: 0 auto;
    background: rgb(0, 0, 0, 0.7);
    border-radius: 20px;
    position: relative;
  }

  .thumb {
    width: 300px;
    float: left;
  }

  .text {
    padding: 40px;
    color: #fff;
    overflow: hidden;
  }

  h1 {
    font-family: 'Abel', sans-serif;
    font-size: 48px;
    margin: 0;
  }

  h3 {
    font-size: 16px;
    line-height: 0;
    margin-top: 30px;
  }

  p {
    font-family: 'Abel', sans-serif;
    font-size: 18px;
    line-height: 26px;
  }

  .rating-director {
    display: flex;
    justify-content: flex-start;
  }

  .score {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 35px;
    height: 35px;
    background: #fff;
    color: #000;
    font-weight: 800;
    border-radius: 25px;
    margin: 0px 0 0 0;
  }

  .director {
    margin: 0 0 0 40px;
  }

  .director p {
    margin: 0;
  }

  @media screen and (max-width: 768px) {
    .wrapper {
      min-height: 600px;
      height: auto;
    }

    .thumb {
      width: 100% !important;
    }
  }

  @media screen and (max-width: 1000px) {
    h1 {
      font-size: 32px !important;
    }
  }

  @keyframes animateMovieinfo {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
</style>
