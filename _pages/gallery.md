---
layout: page
permalink: /gallery/
title: Gallery
# description: Miscellaneous 
nav: true
nav_order: 8
---

<div class="carousel" style="text-align: center;">
  <div style="position: relative; display: inline-block;">
    <div class="carousel-slide">
      <img class="carousel-image" src="/assets/img/lab_photo.jpg" alt="Lab Photo" style="width:600px;">
      <div class="caption">KGML Team</div>
    </div>
    
    <div class="carousel-slide" style="display:none;">
      <img class="carousel-image" src="/assets/img/jie_grad_celebration.jpg" alt="Graduation Celebration" style="width:600px;">
      <div class="caption">Jie’s PhD Defense Celebration</div>
    </div>
    
    <button class="prev" onclick="changeSlide(-1)">&#10094;</button>
    <button class="next" onclick="changeSlide(1)">&#10095;</button>

  </div>
</div>

<script>
  let slideIndex = 0;
  showSlides(slideIndex);

  function changeSlide(n) {
    showSlides(slideIndex += n);
  }

  function showSlides(n) {
    let i;
    let slides = document.getElementsByClassName("carousel-slide");
    if (n >= slides.length) { slideIndex = 0 }
    if (n < 0) { slideIndex = slides.length - 1 }
    for (i = 0; i < slides.length; i++) {
      slides[i].style.display = "none";
    }
    slides[slideIndex].style.display = "block";
  }
</script>

<style>
  .carousel {
    position: relative;
    max-width: 100%;
  }

  .carousel-image {
    width: 600px;
    height: auto;
    display: block;
    margin: 0 auto;
  }

  .prev, .next {
    position: absolute;
    top: 50%;
    font-size: 18px;
    padding: 16px;
    cursor: pointer;
    background-color: rgba(0, 0, 0, 0.5);
    color: white;
    border: none;
    transform: translateY(-50%);
    z-index: 1;
  }

  .prev {
    left: -50px;
  }

  .next {
    right: -50px;
  }

  .caption {
    text-align: center;
    color: #333;
    font-size: 16px;
    margin-top: 10px;
    font-style: italic;
  }

  .carousel-slide {
    position: relative;
  }
</style>
