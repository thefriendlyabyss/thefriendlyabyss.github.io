---
layout: page
full-width: true
body-class: homepage
---
<style>
  .hero-wrap {
    position: relative;
    margin-left: calc(-50vw + 50%);
    margin-right: calc(-50vw + 50%);
    height: 100vh;
    overflow: hidden;
  }
  .homepage-hero {
    position: absolute;
    inset: 0;
  }
  .homepage-hero .hero-slide {
    position: absolute;
    top: 0; left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
    opacity: 0;
    transition: opacity 1.8s ease-in-out;
  }
  .homepage-hero .hero-slide.active {
    opacity: 1;
  }
  .hero-overlay {
    position: absolute;
    inset: 0;
    background: rgba(0,0,0,0.4);
  }
  .hero-caption {
    position: absolute;
    bottom: 24px;
    right: 28px;
    color: #e0f0d0;
    font-size: 0.85em;
    font-style: italic;
    text-shadow: 0 1px 4px rgba(0,0,0,0.6);
    opacity: 0.85;
    transition: opacity 0.9s ease-in-out;
    z-index: 2;
  }
  .hero-caption.fading {
    opacity: 0;
  }
  .hero-content {
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
    padding: 20px;
    width: 80%;
    z-index: 3;
  }
  .hero-video-wrap {
    max-width: 640px;
    margin: 0 auto 25px auto;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 4px 20px rgba(0,0,0,0.35);
  }
  .hero-video-wrap .ratio {
    position: relative;
    padding-bottom: 56.25%;
    height: 0;
  }
  .hero-video-wrap iframe {
    position: absolute;
    top: 0; left: 0;
    width: 100%;
    height: 100%;
    border: none;
  }

  @media (max-width: 600px) {
    .hero-wrap {
      height: auto;
      overflow: visible;
    }
    .homepage-hero {
      position: relative;
      height: 60svh;
      min-height: 320px;
    }
    .hero-content {
      position: static;
      transform: none;
      width: 100%;
      padding: 30px 16px;
      background-color: #0a2828;
    }
    .hero-content p {
      font-size: 1em !important;
    }
    .hero-content div a {
      display: block;
      margin: 8px auto;
      max-width: 260px;
    }
  }
</style>
<div class="hero-wrap">
  <div class="homepage-hero">
    <img src="/assets/img/isla-de-pinos.webp" alt="El Pinero"
    width="1920" height="1080"
    fetchpriority="high"
    class="hero-slide active"
    data-caption="Isla de la Juventud, Cuba.">
    <img src="/assets/img/presidio-modelo.webp" alt=""
    width="1920" height="1080"
    loading="lazy" fetchpriority="low"
    class="hero-slide"
    data-caption="The Presidio Modelo, begun 1926.">
    <img src="/assets/img/pine-forest.webp" alt=""
    width="1920" height="1080"
    loading="lazy" fetchpriority="low"
    class="hero-slide"
    data-caption="The pine forests that cover the Isla de la Juventud.">
    <div class="hero-overlay"></div>
    <div class="hero-caption" id="heroCaption"></div>
  </div>
  <div class="hero-content">
    <p style="color: #ffffff; font-size: 1.4em; font-style: italic; 
      margin-bottom: 15px;">
      In Cuba, an American man searches for his grandfather's grave, 
      but as he moves through the island, the history he came to recover 
      begins to slip away from him.
    </p>
    <p style="color: #e0f0d0; font-size: 0.95em; margin-bottom: 25px;">
      <em>El Pinero</em> — a short film by Robert Potter and Meilín Quilez Durañona
    </p>
    <div id="heroVideoContainer"></div>
    <div>
      <a href="film" style="display: inline-block; margin: 8px; padding: 10px 24px; 
        background-color: #0d4a52; color: #e0f0d0; text-decoration: none; 
        border-radius: 4px; font-size: 0.95em;">About The Film</a>
      <a href="/support/" target="_blank" 
        style="display: inline-block; margin: 8px; padding: 10px 24px; 
        background-color: #1a7070; color: #e0f0d0; text-decoration: none; 
        border-radius: 4px; font-size: 0.95em;">Support The Film</a>
      <a href="/blog/" 
        style="display: inline-block; margin: 8px; padding: 10px 24px; 
        background-color: #0d4a52; color: #e0f0d0; text-decoration: none; 
        border-radius: 4px; font-size: 0.95em;">Sign Up For Updates</a>
    </div>
  </div>
</div>
<script>
  document.body.classList.add('homepage');

  var HeroSlideshow = (function () {
    var slides = document.querySelectorAll('.homepage-hero .hero-slide');
    var caption = document.getElementById('heroCaption');
    var current = 0;
    var timer = null;

    if (caption && slides.length) {
      caption.textContent = slides[0].dataset.caption || '';
    }

    function tick() {
      slides[current].classList.remove('active');
      current = (current + 1) % slides.length;
      slides[current].classList.add('active');
      if (caption) {
        caption.classList.add('fading');
        setTimeout(function () {
          caption.textContent = slides[current].dataset.caption || '';
          caption.classList.remove('fading');
        }, 900);
      }
    }

    function start() {
      if (timer || slides.length < 2) return;
      if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;
      timer = setInterval(tick, 6000);
    }

    function stop() {
      clearInterval(timer);
      timer = null;
    }

    start();
    return { start: start, stop: stop };
  })();

  // Only load and insert the video on wider screens. On mobile, neither
  // the iframe nor the YouTube API script are added to the page at all.
  if (window.matchMedia('(min-width: 601px)').matches) {
    var container = document.getElementById('heroVideoContainer');
    if (container) {
      container.innerHTML =
        '<div class="hero-video-wrap">' +
          '<div class="ratio">' +
            '<iframe id="heroVideoFrame" ' +
              'src="https://www.youtube.com/embed/g6fpe6pIZBw?rel=0&modestbranding=1&iv_load_policy=3&enablejsapi=1" ' +
              'title="El Pinero fundraising video" ' +
              'allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" ' +
              'allowfullscreen></iframe>' +
          '</div>' +
        '</div>';

      window.onYouTubeIframeAPIReady = function () {
        new YT.Player('heroVideoFrame', {
          events: {
            onStateChange: function (event) {
              if (event.data === YT.PlayerState.PLAYING) {
                HeroSlideshow.stop();
              } else if (event.data === YT.PlayerState.PAUSED || event.data === YT.PlayerState.ENDED) {
                HeroSlideshow.start();
              }
            }
          }
        });
      };

      var apiScript = document.createElement('script');
      apiScript.src = 'https://www.youtube.com/iframe_api';
      document.body.appendChild(apiScript);
    }
  }
</script>
