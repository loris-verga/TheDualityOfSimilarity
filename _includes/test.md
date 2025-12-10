<!-- ===== Group 1 ===== -->
<div class="accordion-group">
  <h3 class="accordion-header">Shared authorship</h3>
  <div class="accordion-content">
    <p>Content for shared authorship in group 1...</p>
  </div>

  <h3 class="accordion-header">Stylometric distance</h3>
  <div class="accordion-content">
    <p>Content for stylometric distance in group 1...</p>
  </div>

  <h3 class="accordion-header">Psychological distance</h3>
  <div class="accordion-content">
    <p>Content for psychological distance in group 1...</p>
  </div>
</div>

<!-- ===== Group 2 ===== -->
<div class="accordion-group">
  <h3 class="accordion-header">Shared authorship</h3>
  <div class="accordion-content">
    <p>Content for shared authorship in group 2...</p>
  </div>

  <h3 class="accordion-header">Stylometric distance</h3>
  <div class="accordion-content">
    <p>Content for stylometric distance in group 2...</p>
  </div>

  <h3 class="accordion-header">Psychological distance</h3>
  <div class="accordion-content">
    <p>Content for psychological distance in group 2...</p>
  </div>
</div>

<style>
.accordion-content {
  display: none;
  padding: 10px 15px;
  border-left: 3px solid #FF4500;
  margin-bottom: 10px;
}
.accordion-content.active {
  display: block;
}
.accordion-header {
  cursor: pointer;
  color: #FF4500;
  margin: 0;
  padding: 10px 0;
  user-select: none;
}
</style>

<script>
document.querySelectorAll('.accordion-group').forEach(group => {
  const headers = group.querySelectorAll('.accordion-header');
  headers.forEach(header => {
    header.addEventListener('click', () => {
      // Close all in this group
      group.querySelectorAll('.accordion-content').forEach(c => c.classList.remove('active'));
      // Open the clicked one
      header.nextElementSibling.classList.add('active');
    });
  });
});
</script>


will add the next two after getting fixed

<div class="two-heatmaps-container">
	<div class="heatmap-container">
	<iframe src="plots/heatmap_authorship_centroids.html" style="width: 100%; height: 100%;"></iframe>
	</div>
	<div class="heatmap-container">
	<iframe src="plots/heatmap_authorship_centroids_2.html" style="width: 100%; height: 100%;"></iframe>
	</div>
</div>

<div class="two-heatmaps-container">
	<div class="heatmap-container">
	<iframe src="plots/heatmap_psycho_centroids.html" style="width: 100%; height: 100%;"></iframe>
	</div>
	<div class="heatmap-container">
	<iframe src="plots/heatmap_psycho_centroids_2.html" style="width: 100%; height: 100%;"></iframe>
	</div>
</div>


determine where to put this?
<div class="container">
<iframe src="graphs/test_all_hyperlinks.html" style="width: 100%; height: 100%;"></iframe>
</div>

{% include basic_plots/sankey_nbr_negative_links.html %}
