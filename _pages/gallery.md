---
layout: page
permalink: /gallery/
title: Gallery
# description: Miscellaneous 
nav: true
nav_order: 8
---


<div class="carousel" style="text-align: center;">
  <div style="position: relative; display: inline-block; width: 80%;" id="carousel-container">
    <button class="prev" onclick="changeSlide(-1)">&#10094;</button>
    <button class="next" onclick="changeSlide(1)">&#10095;</button>
  </div>

  <!-- Scrollable Thumbnail strip (centered) -->
  <div id="thumbnail-container-wrapper" style="display: flex; justify-content: center; margin-top: 20px;">
    <div id="thumbnail-container" style="display: inline-block; width: 80%; overflow-x: auto; white-space: nowrap; padding: 10px 0;">
    </div>
  </div>
</div>

<script>
  let slideIndex = 0;
  let slides = [];

  // Function to load the JSON data
  async function loadGallery() {
    try {
      const response = await fetch('/assets/img/gallery/gallery.json?v=' + new Date().getTime());
      const images = await response.json();
      createCarousel(images);
    } catch (error) {
      console.error("Error loading gallery JSON:", error);
    }
  }

  // Function to dynamically generate carousel slides and thumbnails
  function createCarousel(images) {
    const carouselContainer = document.getElementById('carousel-container');
    const thumbnailContainer = document.getElementById('thumbnail-container');

    images.forEach((image, index) => {
      // Create the slide
      const slideDiv = document.createElement('div');
      slideDiv.classList.add('carousel-slide');
      if (index !== 0) slideDiv.style.display = "none"; // Only show the first image
      slides.push(slideDiv); // Store slides in array

      const img = document.createElement('img');
      img.classList.add('carousel-image');
      img.src = image.src;
      img.alt = image.caption;
      img.style.height = "400px"; // Fixed height for all images
      img.style.objectFit = "contain"; // Preserve aspect ratio, contain within the box

      const caption = document.createElement('div');
      caption.classList.add('caption');
      caption.textContent = image.caption;

      slideDiv.appendChild(img);
      slideDiv.appendChild(caption);
      carouselContainer.insertBefore(slideDiv, carouselContainer.children[0]); // Add slides before buttons

      // Create the thumbnail
      const thumbnail = document.createElement('img');
      thumbnail.src = image.src;
      thumbnail.alt = image.caption;
      thumbnail.classList.add('thumbnail');
      thumbnail.onclick = () => {
        showSlide(index); // Go to specific slide on click
      };
      thumbnailContainer.appendChild(thumbnail);
    });

    // Initialize first thumbnail as active
    updateActiveThumbnail(slideIndex);
  }

  // Function to change slides (next/previous)
  function changeSlide(n) {
    slideIndex += n;
    if (slideIndex >= slides.length) { slideIndex = 0 }
    if (slideIndex < 0) { slideIndex = slides.length - 1 }
    showSlide(slideIndex);
  }

  // Function to show a specific slide and update active thumbnail
  function showSlide(n) {
    slides.forEach(slide => slide.style.display = "none"); // Hide all slides
    slides[n].style.display = "block"; // Show the selected slide
    slideIndex = n;
    updateActiveThumbnail(n); // Update thumbnail highlight
  }

  // Function to update the active thumbnail
  function updateActiveThumbnail(index) {
    const thumbnails = document.querySelectorAll('.thumbnail');
    thumbnails.forEach(thumb => thumb.classList.remove('active')); // Remove active class from all
    thumbnails[index].classList.add('active'); // Add active class to current thumbnail
  }

  // Load the gallery when the page loads
  loadGallery();
</script>

<style>
  .carousel {
    position: relative;
    max-width: 100%;
  }

  .carousel-image {
    width: 100%; /* 100% of the container's width */
    height: 400px; /* Fixed height */
    object-fit: contain; /* Preserve aspect ratio, fit within the box */
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
    left: 10px;
  }

  .next {
    right: 10px;
  }

  /* Default styles (Light Mode) */
  [data-theme="light"] .caption {
    text-align: center;
    color: #333; /* Dark text for light mode */
    font-size: 16px;
    margin-top: 10px;
    font-style: italic;
  }

  /* Dark Mode (when data-theme is set to "dark") */
  [data-theme="dark"] .caption {
    text-align: center;
    color: #fff; /* Light text for dark mode */
    font-size: 16px;
    margin-top: 10px;
    font-style: italic; 
  }

  .carousel-slide {
    position: relative;
  }

  /* Thumbnails */
  .thumbnail {
    width: 80px; /* Fixed width */
    height: 80px; /* Fixed height */
    object-fit: contain; /* Preserve aspect ratio within fixed box */
    margin: 0 5px;
    cursor: pointer;
    opacity: 0.6;
    transition: opacity 0.3s ease;
    display: inline-block;
  }

  .thumbnail:hover {
    opacity: 1;
  }

  .thumbnail.active {
    border: 2px solid #333; /* Highlight the active thumbnail */
    opacity: 1; /* Fully visible */
  }

  /* Scrollbar styling (optional) */
  #thumbnail-container::-webkit-scrollbar {
    height: 8px;
  }

  #thumbnail-container::-webkit-scrollbar-thumb {
    background-color: #888;
    border-radius: 10px;
  }

  #thumbnail-container::-webkit-scrollbar-thumb:hover {
    background-color: #555;
  }
</style>
