<nav class="glass-nav">
  <ul>
    <li><a href="#section1">Overview</a></li>
    <li><a href="#section2">Methods</a></li>
    <li><a href="#section3">Results</a></li>
    <li><a href="#section4">Discussion</a></li>
  </ul>
</nav>


/* Smooth scroll for the whole page */
html {
  scroll-behavior: smooth;
}

/* Glassy navbar */
.glass-nav {
  position: sticky;<nav class="glass-nav">
  <ul>
    <li><a href="#section1">Overview</a></li>
    <li><a href="#section2">Methods</a></li>
    <li><a href="#section3">Results</a></li>
    <li><a href="#section4">Discussion</a></li>
  </ul>
</nav>

<style>
/* Smooth scroll for the whole page */
html {
  scroll-behavior: smooth;
}

/* Glassy navbar */
.glass-nav {
  position: sticky;
  top: 0;
  width: 100%;
  z-index: 1000;

  background: rgba(255, 115, 0, 0.15); /* soft orange glass */
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);

  padding: 12px 0;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);

  opacity: 0;
  animation: fadeInNav 0.8s both;
}

/* Center content */
.glass-nav ul {
  display: flex;
  justify-content: center;
  gap: 32px;
  list-style: none;
  margin: 0;
  padding: 0;
}

/* Base link style */
.glass-nav a {
  text-decoration: none;
  font-weight: 600;
  font-size: 16px;

  color: #fafafa;
  padding: 8px 16px;
  border-radius: 8px;
  transition: 0.25s ease;
}

/* Hover */
.glass-nav a:hover {
  background: rgba(255, 115, 0, 0.25);
  color: white;
}

/* Active state when user clicks */
.glass-nav a:active {
  background: rgba(255, 115, 0, 0.35);
}

/* Fade-in animation */
@keyframes fadeInNav {
  from { opacity: 0; transform: translateY(-10px); }
  to   { opacity: 1; transform: translateY(0); }
}
</style>

  top: 0;
  width: 100%;
  z-index: 1000;

  background: rgba(255, 115, 0, 0.15); /* soft orange glass */
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);

  padding: 12px 0;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

/* Center content */
.glass-nav ul {
  display: flex;
  justify-content: center;
  gap: 32px;
  list-style: none;
  margin: 0;
  padding: 0;
}

/* Base link style */
.glass-nav a {
  text-decoration: none;
  font-weight: 600;
  font-size: 16px;

  color: #fafafa;
  padding: 8px 16px;
  border-radius: 8px;
  transition: 0.25s ease;
}

/* Hover */
.glass-nav a:hover {
  background: rgba(255, 115, 0, 0.25);
  color: white;
}

/* Active state when user clicks (optional) */
.glass-nav a:active {
  background: rgba(255, 115, 0, 0.35);
}


.glass-nav {
  opacity: 0;
  animation: fadeInNav 0.8s both;
}

@keyframes fadeInNav {
  from { opacity: 0; transform: translateY(-10px); }
  to   { opacity: 1; transform: translateY(0); }
}
