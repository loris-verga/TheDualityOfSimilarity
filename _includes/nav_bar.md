<nav id="glassNav" class="glass-nav">
  <ul>
    <li><a href="#section1">Overview</a></li>
    <li><a href="#section2">Methods</a></li>
    <li><a href="#section3">Results</a></li>
    <li><a href="#section4">Discussion</a></li>
  </ul>
</nav>

<style>
html {
  scroll-behavior: smooth;
}

/* Glass + strong Reddit Orange */
.glass-nav {
  position: fixed;
  top: 0;
  left: 50%;
  transform: translateX(-50%);

  width: 95vw;
  max-width: 1100px;

  z-index: 2000;

  background: rgba(255, 69, 0, 0.35); /* Stronger Reddit orange */
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);

  padding: 6px 0;                     /* thinner bar */
  border-radius: 14px;
  margin-top: 10px;

  box-shadow: 0 4px 16px rgba(0,0,0,0.18);
  transition: transform 0.35s ease, opacity 0.35s ease;
}

/* Hide the navbar */
.glass-nav.hidden {
  transform: translate(-50%, -130%);
  opacity: 0;
}

/* Center the tabs PERFECTLY */
.glass-nav ul {
  list-style: none;
  margin: 0 auto;
  padding: 0;

  width: fit-content;
  display: flex;
  justify-content: center;
  gap: 28px;
}

/* Tab links */
.glass-nav a {
  text-decoration: none;
  color: #fff;
  font-weight: 600;
  font-size: 15px;

  padding: 5px 12px;
  border-radius: 8px;
  transition: background 0.25s, box-shadow 0.25s;
}

/* Hover glow */
.glass-nav a:hover {
  background: rgba(255, 69, 0, 0.45);
  box-shadow: 0 0 8px rgba(255, 69, 0, 0.5);
}
</style>

<script>
// Hide on scroll down, show on scroll up ONLY
let lastY = window.scrollY;
const nav = document.getElementById("glassNav");

window.addEventListener("scroll", () => {
  const currentY = window.scrollY;

  // scrolling down → hide
  if (currentY > lastY) {
    nav.classList.add("hidden");
  } 
  // scrolling up → show
  else if (currentY < lastY) {
    nav.classList.remove("hidden");
  }

  lastY = currentY;
});
</script>


<!-- Navbar already points to these IDs -->
<nav class="glass-nav">
  <ul>
    <li><a href="#section1">Overview</a></li>
    <li><a href="#section2">Methods</a></li>
    <li><a href="#section3">Results</a></li>
    <li><a href="#section4">Discussion</a></li>
  </ul>
</nav>

<!-- Page content -->
<section id="section1" style="padding:100px 20px; min-height:100vh; background:#f5f5f5;">
  <h2>Overview</h2>
</section>

<section id="section2" style="padding:100px 20px; min-height:100vh; background:#eaeaea;">
  <h2>Methods</h2>
</section>

<section id="section3" style="padding:100px 20px; min-height:100vh; background:#f5f5f5;">
  <h2>Results</h2>
</section>
