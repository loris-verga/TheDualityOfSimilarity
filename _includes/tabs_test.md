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
