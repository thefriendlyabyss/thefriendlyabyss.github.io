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
    /* Center in the space below the fixed menu bar and its round logo
       (about 120px tall), not the whole screen, so the logline isn't
       tucked under the menu on shorter laptop screens */
    top: calc(50% + 60px); left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
    padding: 20px;
    width: 80%;
    z-index: 3;
  }
  .hero-video-wrap {
    /* An explicit width keeps the video from collapsing to 0x0 when a
       mobile rule turns its container into a centered flex column
       (about 601-768px wide, e.g. portrait tablets) */
    width: 100%;
    /* Full 640px on tall screens; shrinks on short ones so the logline,
       video and buttons all fit below the menu */
    max-width: clamp(320px, calc((100vh - 460px) * 16 / 9), 640px);
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


  /* ---- Buttons ---- */
  .home-btn {
    display: inline-block;
    background-color: #1a7070;
    color: #e0f0d0;
    padding: 14px 36px;
    border-radius: 6px;
    font-size: 1.1em;
    font-weight: 700;
    text-decoration: none;
    transition: background-color 0.2s ease;
  }
  .home-btn:hover,
  .home-btn:focus {
    background-color: #0d4a52;
    color: #e0f0d0;
    text-decoration: none;
  }
  .home-btn-hero {
    margin: 8px;
  }
  .home-section-dark .home-btn {
    background-color: #e0f0d0;
    color: #0a2828;
  }
  .home-section-dark .home-btn:hover,
  .home-section-dark .home-btn:focus {
    background-color: #1a7070;
    color: #e0f0d0;
  }

  /* ---- Sections below the hero ---- */
  .home-section {
    margin-left: calc(-50vw + 50%);
    margin-right: calc(-50vw + 50%);
    padding: 72px 16px;
  }
  .home-section-dark {
    background-color: #0a2828;
    color: #e0f0d0;
  }
  .home-section-inner {
    max-width: 960px;
    margin: 0 auto;
    text-align: center;
  }
  .home-eyebrow {
    font-size: 0.85rem;
    text-transform: uppercase;
    letter-spacing: 0.15em;
    opacity: 0.75;
    margin: 0 0 8px;
  }
  .home-section h2 {
    margin: 0 0 32px;
  }
  .home-section-dark h2 {
    color: #e0f0d0;
  }
  .home-cta {
    margin-top: 36px;
  }

  .home-intro {
    max-width: 640px;
    margin: -12px auto 36px;
    font-size: 1.1em;
    line-height: 1.6;
  }

  /* Filmmakers */
  .home-people {
    display: flex;
    justify-content: center;
    gap: 56px;
    flex-wrap: wrap;
  }
  .home-person {
    width: 280px;
  }
  .home-person img {
    max-width: 240px;
    margin-left: auto;
    margin-right: auto;
  }
  .home-person img {
    width: 100%;
    aspect-ratio: 3 / 4;
    object-fit: cover;
    object-position: center 20%;
    border-radius: 6px;
    filter: grayscale(100%);
    display: block;
    margin-bottom: 16px;
    border: 6px solid #ffffff;
    box-shadow: 0 4px 14px rgba(10, 40, 40, 0.18);
  }
  .home-person h3 {
    margin: 0 0 4px;
    font-size: 1.3rem;
  }
  .home-role {
    font-style: italic;
    margin: 0 0 8px;
  }
  .home-socials a {
    margin: 0 5px;
    color: #1d3d3d;
  }
  .home-shoot {
    margin: 40px auto 0;
    font-size: 1.05em;
  }

  /* History */
  .home-history {
    display: flex;
    gap: 40px;
    align-items: center;
    text-align: left;
  }
  .home-history img {
    flex: 0 0 42%;
    max-width: 42%;
    border-radius: 6px;
  }
  .home-history p {
    color: #e0f0d0;
    line-height: 1.7;
  }

  /* Latest update */
  .home-update {
    display: flex;
    gap: 32px;
    align-items: center;
    text-align: left;
    color: inherit;
    text-decoration: none;
    max-width: 800px;
    margin: 0 auto;
  }
  .home-update:hover {
    text-decoration: none;
    color: inherit;
  }
  .home-update img {
    flex: 0 0 300px;
    width: 300px;
    aspect-ratio: 3 / 2;
    object-fit: cover;
    border-radius: 6px;
  }
  .home-update h3 {
    margin: 4px 0 8px;
  }
  .home-update:hover h3 {
    text-decoration: underline;
  }
  .home-update-date {
    font-size: 0.85rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    opacity: 0.7;
  }

  .home-history-short {
    display: none;
  }

  @media (max-width: 767px) {
    .home-section {
      padding: 48px 16px;
    }
    .home-section h2 {
      margin-bottom: 24px;
    }
    .home-cta {
      margin-top: 28px;
    }
    /* Filmmakers: side by side, smaller */
    .home-people {
      gap: 16px;
      flex-wrap: nowrap;
    }
    .home-person {
      width: 50%;
      max-width: 180px;
    }
    .home-person img {
      border-width: 4px;
      margin-bottom: 10px;
    }
    .home-person h3 {
      font-size: 1rem;
    }
    .home-role {
      font-size: 0.9em;
      margin-bottom: 4px;
    }
    .home-shoot {
      margin-top: 24px;
    }
    /* History: one short paragraph and a wide, short photo */
    .home-history-full {
      display: none;
    }
    .home-history-short {
      display: block;
      margin: 0;
      text-align: center;
    }
    .home-history {
      gap: 20px;
    }
    .home-history img {
      aspect-ratio: 16 / 9;
      object-fit: cover;
    }
    /* Updates: title and date only */
    .home-update {
      gap: 14px;
    }
    .home-update img {
      aspect-ratio: 16 / 9;
    }
    .home-update p {
      display: none;
    }
    .home-history,
    .home-update {
      flex-direction: column;
      text-align: center;
    }
    .home-history img,
    .home-update img {
      flex: 0 0 auto;
      max-width: 100%;
      width: 100%;
    }
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
    .hero-content div a.home-btn-hero {
      display: block;
      width: auto;
      margin: 8px auto;
      max-width: 280px;
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
      To fulfill his father's last wish, a young American man travels to
      Isla de la Juventud, Cuba. But as he journeys deeper into the island,
      the search for his grandfather's grave opens the door to a family
      history he never knew.
    </p>
    <p style="color: #e0f0d0; font-size: 0.95em; margin-bottom: 25px;">
      <em>El Pinero</em> — a short film by Robert Potter and Meilín Quilez Durañona
    </p>
    <div id="heroVideoContainer"></div>
    <div>
      <a href="/support/" class="home-btn home-btn-hero">Support The Film</a>
    </div>
  </div>
</div>

<section class="home-section" aria-labelledby="home-filmmakers">
  <div class="home-section-inner">
    <p class="home-eyebrow">The Filmmakers</p>
    <h2 id="home-filmmakers">From Florida to the Isla de la Juventud</h2>
    <p class="home-intro"><em>El Pinero</em> is a true Cuban–American collaboration. Its cast and crew come from both sides of the Florida Straits, telling a story of the two countries' shared past from both perspectives.</p>
    <div class="home-people">
      <div class="home-person">
        <img src="{{ '/assets/img/Robert W. Potter.webp' | relative_url }}" alt="Robert W. Potter" loading="lazy">
        <h3>Robert W. Potter</h3>
        <p class="home-role">Writer / Producer</p>
        <div class="home-socials"><a href="https://www.instagram.com/robertthepotter" target="_blank" rel="noopener" aria-label="Robert W. Potter on Instagram"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="14" height="14" fill="currentColor"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/></svg></a> <a href="https://www.linkedin.com/in/robertwpotter/" target="_blank" rel="noopener" aria-label="Robert W. Potter on LinkedIn"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="14" height="14" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg></a></div>
      </div>
      <div class="home-person">
        <img src="{{ '/assets/img/Meilin Quilez Duranona.webp' | relative_url }}" alt="Meilín Quilez Durañona" loading="lazy">
        <h3>Meilín Quilez Durañona</h3>
        <p class="home-role">Director / Producer</p>
        <div class="home-socials"><a href="https://www.instagram.com/meilinquilez/" target="_blank" rel="noopener" aria-label="Meilín Quilez Durañona on Instagram"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="14" height="14" fill="currentColor"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/></svg></a> <a href="https://meilinquilez.substack.com" target="_blank" title="Substack" style="font-family: Georgia, serif; font-weight: bold; font-size: 1em; color: currentColor; text-decoration: none; margin-left: 8px; vertical-align: middle;" rel="noopener" aria-label="Meilín Quilez Durañona on Substack">S</a></div>
      </div>
    </div>
    <p class="home-shoot">Principal photography is planned for <strong>summer 2027</strong> on location on the Isla de la Juventud.</p>
    <div class="home-cta">
      <a href="{{ '/cast-and-crew/' | relative_url }}" class="home-btn">Meet the Full Cast &amp; Crew</a>
    </div>
  </div>
</section>

<section class="home-section home-section-dark" aria-labelledby="home-history">
  <div class="home-section-inner">
    <p class="home-eyebrow">The History</p>
    <h2 id="home-history">America's Forgotten Colony</h2>
    <div class="home-history">
      <img src="{{ '/assets/img/posts/nueva-gerona-harbor.jpg' | relative_url }}" alt="An old photograph of the harbor at Nueva Gerona" loading="lazy">
      <div class="home-history-full">
        <p>In the early 1900s, while the island's political status sat unresolved, American land companies sold Cuba's Isle of Pines as a tropical paradise ready to be farmed. Thousands of settlers came. At the peak, perhaps two thousand Americans lived there, founding roughly a dozen towns with their own churches, schools, and an English-language newspaper.</p>
        <p>Most eventually left. In 1925 the United States recognized Cuban sovereignty over the island, and after the 1959 Revolution nearly all who remained went home. The last of them died there in 1995. What is left is a weathered cemetery holding the graves of some two hundred Americans, and that is where <em>El Pinero</em> begins.</p>
      </div>
      <p class="home-history-short">In the early 1900s, as many as two thousand Americans settled Cuba's Isle of Pines. Nearly all of them eventually left. What remains is a weathered cemetery holding some two hundred American graves, and that is where <em>El Pinero</em> begins.</p>
    </div>
    <div class="home-cta">
      <a href="{{ '/film/' | relative_url }}" class="home-btn">Learn the History</a>
    </div>
  </div>
</section>

{% assign latest = site.posts.first %}
<section class="home-section" aria-labelledby="home-updates">
  <div class="home-section-inner">
    <p class="home-eyebrow">Updates</p>
    <h2 id="home-updates">Follow Along</h2>
    {% if latest %}
    <a class="home-update" href="{{ latest.url | relative_url }}">
      {% if latest.cover-img %}<img src="{{ latest.cover-img | relative_url }}" alt="" loading="lazy">{% endif %}
      <div>
        <span class="home-update-date">Latest &middot; {{ latest.date | date: "%B %-d, %Y" }}</span>
        <h3>{{ latest.title }}</h3>
        {% if latest.subtitle %}<p>{{ latest.subtitle }}</p>{% endif %}
      </div>
    </a>
    {% endif %}
    <div class="home-cta">
      <a href="{{ '/blog/' | relative_url }}" class="home-btn">Read All Updates</a>
    </div>
  </div>
</section>

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
