<section id="section5">
    <h2>Test</h2>
  </section>






<style>
/* -------------------------
   Tabs container (no full-width grey line)
   ------------------------- */
ul[data-tabs] {
  display: flex;
  gap: 18px;
  padding: 0;
  margin: 0 0 18px 0;
  list-style: none;
  border: none !important; /* keep no ugly full-width line */
}

/* make links inline-block so padding and pseudo-element behave well */
ul[data-tabs] a {
  text-decoration: none;
  color: #FF4500;                /* default link color (orange) */
  padding: 8px 14px;
  border-radius: 8px;
  display: inline-block;
  transition: all 160ms ease;
  position: relative;            /* for ::after underline */
  background: transparent !important;
}

/* Hover subtle lift */
ul[data-tabs] a:hover {
  transform: translateY(-1px);
}

/* -------------------------
   Active tab: high specificity + important
   ------------------------- */
/* this targets anchors inside the data-tabs UL with the tabby-active class */
ul[data-tabs] a.tabby-active,
ul[data-tabs] a.tabby-active:focus {
  background-color: #FF4500 !important;  /* orange rectangle */
  color: #ffffff !important;             /* white text */
  font-weight: 600 !important;
}

/* small strong underline (only under the active tab text) */
ul[data-tabs] a.tabby-active::after {
  content: "";
  position: absolute;
  left: 10%;
  right: 10%;
  bottom: -8px;                 /* gap between rect and underline */
  height: 4px;
  border-radius: 3px;
  background: #E64A19;          /* slightly darker orange for contrast */
}

/* if you prefer underline to span full tab width, use left:0; right:0; */

/* -------------------------
   Panels
   ------------------------- */
.tabby-content {
  padding-top: 12px;
}
</style>

<ul data-tabs>
  <li><a data-tabby-toggle data-tabby-default href="#shared">Shared authorship</a></li>
  <li><a data-tabby-toggle href="#stylo">Stylometric</a></li>
  <li><a data-tabby-toggle href="#psycho">Psychological</a></li>
</ul>

<div id="shared" class="tabby-content" data-tabby-panel>
  Test first tab
</div>

<div id="stylo" class="tabby-content" data-tabby-panel>
  2nd tab
</div>

<div id="psycho" class="tabby-content" data-tabby-panel>
  Psychological content
</div>

<script>
  var tabs = new Tabby('[data-tabs]', { scroll: false });
</script>
