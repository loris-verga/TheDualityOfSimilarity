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

/* Glassy Reddit-orange navbar */
.glass-nav {
  position: fixed;
  top: 0;
  left: 50%;
  transform: translateX(-50%);   /* perfectly centered */
  
  width: 95vw;                   /* slightly inset from edges */
  max-width: 1200px;
  z-index: 2000;

  background: rgba(255, 69, 0, 0.25); /* stronger Reddit orange glass */
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);

  padding: 8px 0;                /* thinner bar */
  border-radius: 14px;           /* rounded corners */
  margin-top: 10px;

  box-shadow: 0 4px 16px rgba(0,0,0,0.18);
  transition: transform 0.3s ease, opacity 0.3s ease;
}

/* Hide the whole navbar on scroll down */
.glass-nav.hidden {
  transform: translate(-50%, -120%);
  opacity: 0;
}

/* Centered list */
.glass-nav ul {
  margin: 0 auto;
  padding: 0;
  list-style: none;

  display: flex;
  justify-content: center;
  gap: 28px;
}

/* Link styling */
.glass-nav a {
  text-decoration: none;
  color: #fff;
  font-weight: 600;
  font-size: 15px;

  padding: 6px 14px;
  border-radius: 8px;

  transition: background 0.25s, box-shadow 0.25s;
}

/* Hover glow */
.glass-nav a:hover {
  background: rgba(255, 69, 0, 0.35);
  box-shadow: 0 0 8px rgba(255, 69, 0, 0.5);
}

/* Active (clicked) */
.glass-nav a:active {
  background: rgba(255, 69, 0, 0.45);
}
</style>

<script>
// Hide on scroll down, show on scroll up
let lastScrollY = window.scrollY;
const nav = document.getElementById("glassNav");

window.addEventListener("scroll", () => {
  if (window.scrollY > lastScrollY + 5) {
    nav.classList.add("hidden");
  } else {
    nav.classList.remove("hidden");
  }
  lastScrollY = window.scrollY;
});
</script>
