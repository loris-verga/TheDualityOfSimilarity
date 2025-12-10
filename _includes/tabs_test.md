<section id="section5">
    <h2>Test</h2>
  </section>

<ul data-tabs>
	<li><a data-tabby-default href="#shared" style="color: #FF4500;">Shared authorship</a></li>
	<li><a href="#stylo" style="color: #FF4500;">Stylometric</a></li>
	<li><a href="#psycho" style="color: #FF4500;">Psychological</a></li>
</ul>

<div id="shared">

Test first tab

</div>

<div id="stylo">

2nd tab

</div>

<div id="psycho">

</div>


<script>
	var tabs = new Tabby('[data-tabs]');
</script>


test:
<style>
/* --- Tabs container --- */
[data-tabs] {
    display: flex;
    gap: 20px;
    padding: 0;
    margin: 0 0 20px 0;      /* small spacing under tabs */
    list-style: none;
    border: none !important; /* remove grey line */
}

/* --- Tab links --- */
[data-tabs] a {
    text-decoration: none;
    color: #FF4500;
    padding: 8px 14px;
    border-radius: 6px;
    display: inline-block;
    transition: 0.2s;
}

/* --- Active tab --- */
[data-tabs] a.tabby-active {
    background-color: #FF4500;
    color: white !important;
    font-weight: 600;
}

/* --- Tab panels (optional styling) --- */
.tabby-content {
    padding-top: 10px;
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
    var tabs = new Tabby('[data-tabs]', {
        scroll: false   // prevents page from jumping
    });
</script>
