# kurd-movie-
Kurd Movie - Kurdish subtitled movies
<!DOCTYPE html>
<html lang="ku">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>KURD MOVIE</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background: #080808;
      color: white;
      font-family: Arial, sans-serif;
    }

    /* NAVBAR */
    header {
      position: sticky;
      top: 0;
      z-index: 100;
      background: rgba(8,8,8,0.96);
      padding: 18px 5%;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 15px;
      border-bottom: 1px solid #202020;
    }

    .logo {
      color: #e50914;
      font-size: 25px;
      font-weight: 900;
      letter-spacing: 1px;
      white-space: nowrap;
    }

    .search {
      width: 210px;
      background: #181818;
      border: 1px solid #333;
      border-radius: 7px;
      padding: 11px 14px;
      color: white;
      outline: none;
    }

    .search:focus {
      border-color: #e50914;
    }

    /* HERO */
    .hero {
      min-height: 430px;
      padding: 80px 7%;
      display: flex;
      align-items: center;
      background:
        linear-gradient(90deg, #080808 10%, rgba(8,8,8,.8) 45%, rgba(8,8,8,.25)),
        linear-gradient(180deg, transparent 60%, #080808 100%);
    }

    .hero-content {
      max-width: 620px;
    }

    .hero small {
      color: #bbb;
      font-size: 14px;
    }

    .hero h1 {
      font-size: 48px;
      margin: 12px 0;
      font-weight: 900;
    }

    .hero p {
      color: #ccc;
      line-height: 1.8;
      margin-bottom: 22px;
    }

    .watch {
      background: #e50914;
      color: white;
      border: none;
      padding: 13px 24px;
      border-radius: 6px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
    }

    .watch:hover {
      background: #b20710;
    }

    /* CONTENT */
    main {
      padding: 0 5% 50px;
    }

    .section-title {
      margin: 28px 0 16px;
      font-size: 22px;
    }

    .movies {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 15px;
    }

    .movie {
      background: #151515;
      border-radius: 8px;
      overflow: hidden;
      transition: .25s;
      cursor: pointer;
    }

    .movie:hover {
      transform: translateY(-5px);
    }

    .poster {
      height: 250px;
      display: flex;
      align-items: center;
      justify-content: center;
      background:
        linear-gradient(145deg, #242424, #101010);
      color: #777;
      font-size: 40px;
      font-weight: bold;
    }

    .movie-info {
      padding: 12px;
    }

    .movie-info h3 {
      font-size: 15px;
      margin-bottom: 7px;
    }

    .movie-info span {
      color: #999;
      font-size: 12px;
    }

    .tag {
      display: inline-block;
      margin-top: 8px;
      background: #e50914;
      padding: 4px 7px;
      border-radius: 4px;
      font-size: 10px;
    }

    /* CATEGORIES */
    .categories {
      display: flex;
      gap: 10px;
      overflow-x: auto;
      padding-bottom: 8px;
    }

    .categories button {
      background: #181818;
      color: #ddd;
      border: 1px solid #333;
      border-radius: 20px;
      padding: 9px 16px;
      white-space: nowrap;
      cursor: pointer;
    }

    .categories button:hover {
      background: #e50914;
      border-color: #e50914;
      color: white;
    }

    footer {
      margin-top: 40px;
      padding: 30px 5%;
      text-align: center;
      border-top: 1px solid #222;
      color: #777;
      font-size: 13px;
    }

    /* MOBILE */
    @media (max-width: 700px) {
      header {
        padding: 15px;
      }

      .logo {
        font-size: 20px;
      }

      .search {
        width: 135px;
      }

      .hero {
        min-height: 390px;
        padding: 50px 6%;
      }

      .hero h1 {
        font-size: 35px;
      }

      .movies {
        grid-template-columns: repeat(2, 1fr);
        gap: 10px;
      }

      .poster {
        height: 230px;
      }

      main {
        padding: 0 15px 40px;
      }
    }
  </style>
</head>

<body>

  <header>
    <div class="logo">KURD MOVIE</div>

    <input
      id="search"
      class="search"
      type="text"
      placeholder="گەڕان..."
      onkeyup="searchMovies()"
    >
  </header>

  <section class="hero">
    <div class="hero-content">
      <small>🎬 KURD MOVIE</small>

      <h1>سینەما لە ماڵەوە</h1>

      <p>
        بەخێربێیت بۆ KURD MOVIE.
        شوێنێک بۆ دۆزینەوەی فیلم و ناوەڕۆکی سینەمایی
        بە شێوەیەکی سادە و جوان.
      </p>

      <button class="watch" onclick="showMessage()">
        ▶ دەستپێکردن
      </button>
    </div>
  </section>

  <main>

    <h2 class="section-title">🔥 نوێترین فیلمەکان</h2>

    <div id="movies" class="movies">

      <div class="movie">
        <div class="poster">🎬</div>
        <div class="movie-info">
          <h3>Movie One</h3>
          <span>2026 • Action</span>
          <div class="tag">KURD SUB</div>
        </div>
      </div>

      <div class="movie">
        <div class="poster">🎥</div>
        <div class="movie-info">
          <h3>Movie Two</h3>
          <span>2026 • Drama</span>
          <div class="tag">KURD SUB</div>
        </div>
      </div>

      <div class="movie">
        <div class="poster">🍿</div>
        <div class="movie-info">
          <h3>Movie Three</h3>
          <span>2026 • Adventure</span>
          <div class="tag">KURD SUB</div>
        </div>
      </div>

      <div class="movie">
        <div class="poster">⭐</div>
        <div class="movie-info">
          <h3>Movie Four</h3>
          <span>2026 • Thriller</span>
          <div class="tag">KURD SUB</div>
        </div>
      </div>

      <div class="movie">
        <div class="poster">🎞️</div>
        <div class="movie-info">
          <h3>Movie Five</h3>
          <span>2026 • Sci-Fi</span>
          <div class="tag">KURD SUB</div>
        </div>
      </div>

    </div>

    <h2 class="section-title">🎭 جۆرەکان</h2>

    <div class="categories">
      <button>Action</button>
      <button>Drama</button>
      <button>Comedy</button>
      <button>Horror</button>
      <button>Adventure</button>
      <button>Sci-Fi</button>
      <button>Animation</button>
    </div>

  </main>

  <footer>
    © 2026 KURD MOVIE — All Rights Reserved
  </footer>

  <script>
    function searchMovies() {
      const input = document
        .getElementById("search")
        .value
        .toLowerCase();

      const movies = document.querySelectorAll(".movie");

      movies.forEach(movie => {
        const title = movie
          .querySelector("h3")
          .textContent
          .toLowerCase();

        movie.style.display =
          title.includes(input) ? "block" : "none";
      });
    }

    function showMessage() {
      alert("بەشی بینینی فیلم دواتر زیاد دەکرێت 🎬");
    }
  </script>

</body>
</html>
