Hello

$$1+1=2$$

blabla


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
	<iframe src="plots/heatmap_stylo_centroids.html" style="width: 100%; height: 100%;"></iframe>
	</div>
	<div class="heatmap-container">
	<iframe src="plots/heatmap_stylo_centroids_2.html" style="width: 100%; height: 100%;"></iframe>
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

<div class="heatmap-container">
<iframe src="plots/heatmap_nbr_negative_links.html" style="width: 100%; height: 100%;"></iframe>
</div>

{% include basic_plots/distrib_negative_links_categories.html %}

{% include basic_plots/mean_authorship_dist_for_type_of_links.html %}

{% include basic_plots/mean_authorship_dist_for_type_of_links_disentangled_by_cat_within.html %}
{% include basic_plots/mean_authorship_dist_for_type_of_links_disentangled_by_cat_inter.html %}

{% include basic_plots/mean_stylo_dist_for_type_of_links.html %}
{% include basic_plots/mean_psycho_dist_for_type_of_links.html %}

{% include basic_plots/deviation_stylometric_features.html %}
{% include basic_plots/deviation_psychological_features.html %}

<div class="container">
<iframe src="graphs/test_all_hyperlinks.html" style="width: 100%; height: 100%;"></iframe>
</div>
