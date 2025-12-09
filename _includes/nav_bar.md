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

/* Glassmorphic Reddit-orange navbar */
.glass-nav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;               /* span entire screen */
  z-index: 2000;
  
  background: rgba(255, 69, 0, 0.15); /* #FF4500 but softened */
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);

  padding: 14px 0;
  box-shadow: 0 4px 15px rgba(0,0,0,0.15);

  transition: transform 0.35s ease, background 0.25s ease;
  animation: fadeInNav 0.8s ease both;
}

/* Hide the navbar (scroll down) */
.glass-nav.hidden {
  transform: translateY(-100%);
}

/* List layout */
.glass-nav ul {
  max-width: 1000px;
  margin: auto;
  display: flex;
  justify-content: center;
  gap: 36px;
  padding: 0;
  list-style: none;
}

/* Link appearance */
.glass-nav a {
  text-decoration: none;
  color: #fff;
  font-weight: 600;
  font-size: 17px;

  padding: 8px 16px;
  border-radius: 10px;
  transition: 0.25s ease;
}

/* Hover glow */
.glass-nav a:hover {
  background: rgba(255, 69, 0, 0.27);
  box-shadow: 0 0 10px rgba(255, 69, 0, 0.4);
}

/* Click */
.glass-nav a:active {
  background: rgba(255, 69, 0, 0.4);
}

/* Fade-in animation */
@keyframes fadeInNav {
  from { opacity: 0; transform: translateY(-12px); }
  to   { opacity: 1; transform: translateY(0); }
}
</style>

<script>
// Smooth hide on scroll down, show on scroll up
let lastScrollY = window.scrollY;
const nav = document.getElementById("glassNav");

window.addEventListener("scroll", () => {
  if (window.scrollY > lastScrollY) {
    nav.classList.add("hidden");    // scrolling down → hide
  } else {
    nav.classList.remove("hidden"); // scrolling up → show
  }
  lastScrollY = window.scrollY;
});
</script>
