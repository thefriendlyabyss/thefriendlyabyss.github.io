---
layout: page
full-width: true
body-class: homepage
---
<style>
  .homepage-hero .hero-slide {
    position: absolute;
    top: 0; left: 0;
    width: 100%;
    height: 100vh;
    object-fit: cover;
    display: block;
    opacity: 0;
    transition: opacity 1.8s ease-in-out;
  }
  .homepage-hero .hero-slide.active {
    opacity: 1;
  }
</style>
<div class="homepage-hero" style="position: relative; margin-left: calc(-50vw + 50%); 
  margin-right: calc(-50vw + 50%); margin-bottom: 0;
  height: 100vh; overflow: hidden;">
  <img src="/assets/img/isla-de-pinos.webp" alt="El Pinero"
  width="1920" height="1080"
  fetchpriority="high"
  class="hero-slide active">
  <img src="/assets/img/presidio-modelo.webp" alt=""
  width="1920" height="1080"
  loading="lazy" fetchpriority="low"
  class="hero-slide">
  <img src="/assets/img/pine-forest.webp" alt=""
  width="1920" height="1080"
  loading="lazy" fetchpriority="low"
  class="hero-slide">
  <div style="position: absolute; top: 0; left: 0; right: 0; bottom: 0; 
    background: rgba(0,0,0,0.4);">
  </div>
  <div class="hero-content" style="position: absolute; top: 50%; left: 50%; 
    transform: translate(-50%, -50%); text-align: center; padding: 20px; width: 80%;">
    <p style="color: #ffffff; font-size: 1.4em; font-style: italic; 
      margin-bottom: 15px;">
      In Cuba, an American man searches for his grandfather's grave, 
      but as he moves through the island, the history he came to recover 
      begins to slip away from him.
    </p>
    <p style="color: #e0f0d0; font-size: 0.95em; margin-bottom: 25px;">
      <em>El Pinero</em> — a short film by Robert Potter and Meilín Quilez Durañona
    </p>
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

  (function () {
    var slides = document.querySelectorAll('.homepage-hero .hero-slide');
    if (slides.length < 2) return;
    if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;
    var current = 0;
    setInterval(function () {
      slides[current].classList.remove('active');
      current = (current + 1) % slides.length;
      slides[current].classList.add('active');
    }, 7000);
  })();
</script>
