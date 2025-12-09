<nav class="glass-nav">
  <ul>
    <li><a href="#section1">Overview</a></li>
    <li><a href="#section2">Methods</a></li>
    <li><a href="#section3">Results</a></li>
    <li><a href="#section4">Discussion</a></li>
  </ul>
</nav>

<section id="section1">
  <h2>Overview</h2>
  <p>Content for Overview...</p>
</section>

<section id="section2">
  <h2>Methods</h2>
  <p>Content for Methods...</p>
</section>

<section id="section3">
  <h2>Results</h2>
  <p>Content for Results...</p>
</section>


html {
  scroll-behavior: smooth;
  margin: 0;
  padding: 0;
}

/* Glassy navbar */
.glass-nav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;          /* full width */
  z-index: 1000;
  background: rgba(255, 69, 0, 0.8); /* Reddit orange, slightly transparent */
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  padding: 8px 0;       /* thinner */
  border-radius: 0 0 12px 12px; /* rounded bottom edges */
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  display: flex;
  justify-content: center; /* center the tabs */
  transition: transform 0.3s ease, opacity 0.3s ease;
}

/* Tabs */
.glass-nav ul {
  display: flex;
  gap: 32px;
  list-style: none;
  margin: 0;
  padding: 0;
}

.glass-nav a {
  text-decoration: none;
  font-weight: 600;
  font-size: 16px;
  color: #fafafa;
  padding: 6px 14px;
  border-radius: 8px;
  transition: 0.25s ease;
}

.glass-nav a:hover {
  background: rgba(255, 69, 0, 0.4);
  color: white;
}

/* Sections */
section {
  padding: 0;          /* remove grey padding */
  min-height: 100vh;
}

/* Scroll-up / scroll-down behavior handled via JS */


<script>
let lastScrollTop = 0;
const navbar = document.querySelector('.glass-nav');

window.addEventListener('scroll', function() {
  const st = window.pageYOffset || document.documentElement.scrollTop;

  if (st > lastScrollTop) {
    // scrolling down → hide navbar
    navbar.style.transform = 'translateY(-100%)';
  } else {
    // scrolling up → show navbar
    navbar.style.transform = 'translateY(0)';
  }

  lastScrollTop = st <= 0 ? 0 : st; // for mobile or negative scrolling
});
</script>
