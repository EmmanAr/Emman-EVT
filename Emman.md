<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Archers Network Gallery</title>
  <style>
    body {
      font-family: sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 2rem;
    }

    section {
      margin-bottom: 4rem;
    }

    h2 {
      color: green;
      border-bottom: 2px solid green;
      padding-bottom: 0.5rem;
      margin-bottom: 1rem;
    }

    .carousel-container {
      max-width: 800px;
      margin: auto;
    }

    .featured {
      background: linear-gradient(to bottom, #ccc, #000);
      color: white;
      height: 200px;
      padding: 1rem;
      margin-bottom: 1rem;
      display: flex;
      flex-direction: column;
      justify-content: flex-end;
    }

    .carousel {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .carousel-items {
      display: flex;
      overflow: hidden;
      gap: 10px;
    }

    .carousel-item {
      background: linear-gradient(to bottom, #ccc, #000);
      color: white;
      width: 100px;
      height: 60px;
      padding: 0.5rem;
      font-size: 0.7rem;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

    button {
      background: none;
      border: none;
      font-size: 1.5rem;
      cursor: pointer;
    }

    .photo .featured {
      display: none;
    }
  </style>
</head>
<body>

  <section>
    <h2>VIDEO HIGHLIGHTS</h2>
    <div class="carousel-container" id="videoSection"></div>
  </section>

  <section>
    <h2>LIVESTREAMS</h2>
    <div class="carousel-container" id="livestreamSection"></div>
  </section>

  <section class="photo">
    <h2>PHOTO ALBUMS</h2>
    <div class="carousel-container" id="photoSection"></div>
  </section>

  <script>
    function createCarousel(containerId, data, isPhoto = false) {
      const container = document.getElementById(containerId);
      let index = 0;
      const visibleCount = 4;

      const featured = document.createElement("div");
      featured.className = "featured";
      if (!isPhoto) {
        featured.innerHTML = `<h3>${data[0].title}</h3><p>${data[0].date}</p>`;
      }

      const carousel = document.createElement("div");
      carousel.className = "carousel";

      const prev = document.createElement("button");
      prev.textContent = "‹";
      const next = document.createElement("button");
      next.textContent = "›";

      const itemsWrapper = document.createElement("div");
      itemsWrapper.className = "carousel-items";

      function renderItems() {
        itemsWrapper.innerHTML = "";
        const visibleItems = data.slice(index, index + visibleCount);
        visibleItems.forEach(item => {
          const itemDiv = document.createElement("div");
          itemDiv.className = "carousel-item";
          itemDiv.innerHTML = `<strong>${item.title}</strong>${item.date ? `<p>${item.date}</p>` : ""}`;
          itemsWrapper.appendChild(itemDiv);
        });

        if (!isPhoto && data[index]) {
          featured.innerHTML = `<h3>${data[index].title}</h3><p>${data[index].date}</p>`;
        }

        prev.disabled = index === 0;
        next.disabled = index + visibleCount >= data.length;
      }

      prev.onclick = () => {
        if (index > 0) {
          index--;
          renderItems();
        }
      };

      next.onclick = () => {
        if (index + visibleCount < data.length) {
          index++;
          renderItems();
        }
      };

      renderItems();
      if (!isPhoto) container.appendChild(featured);
      carousel.appendChild(prev);
      carousel.appendChild(itemsWrapper);
      carousel.appendChild(next);
      container.appendChild(carousel);
    }

    const videoData = [
      { title: "Video Title", date: "January 1, 2025" },
      { title: "Video Title", date: "January 2, 2025" },
      { title: "Video Title", date: "January 3, 2025" },
      { title: "Video Title", date: "January 4, 2025" },
      { title: "Video Title", date: "January 5, 2025" },
    ];

    const photoAlbums = [
      { title: "Album 1" },
      { title: "Album 2" },
      { title: "Album 3" },
      { title: "Album 4" },
      { title: "Album 5" },
    ];

    createCarousel("videoSection", videoData);
    createCarousel("livestreamSection", videoData);
    createCarousel("photoSection", photoAlbums, true);
  </script>
</body>
</html>
