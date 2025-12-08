<p class="ignore">
    put all plot includes here (this file is not linked to website) to avoid ID conflicts
</p>

{% include basic_plots/distrib_cosine_dist_embeddings.html %}
{% include basic_plots/indiv_distrib_cosine_dist_embeddings_by_link_sentiment.html %}
{% include basic_plots/mean_cosine_dist_across_groups_of_link_sentiment.html %}
{% include basic_plots/number_link_sentiment_distant_groups.html %}
{% include basic_plots/distrib_compound_embeddings_causal_analysis.html %}

{% include basic_plots/distrib_cosine_dist_stylo.html %}


<div class="heatmap-container">
<iframe src="plots/correl_matrix_stylo.html" style="width: 100%; height: 100%;"></iframe>
</div>

{% include basic_plots/pca_stylo.html %}
{% include basic_plots/tsne_stylo.html %}

{% include basic_plots/mean_stylo_cosine_dist_across_groups_of_link_sentiment.html %}
{% include basic_plots/number_link_sentiment_distant_groups_stylo.html %}


{% include basic_plots/distrib_cosine_dist_psycho.html %}

<div class="heatmap-container">
<iframe src="plots/correl_matrix_psycho.html" style="width: 100%; height: 100%;"></iframe>
</div>

{% include basic_plots/pca_psycho.html %} #
{% include basic_plots/tsne_psycho.html %} #
{% include basic_plots/mean_psycho_cosine_dist_across_groups_of_link_sentiment.html %}
{% include basic_plots/number_link_sentiment_distant_groups_psycho.html %}    

{% include basic_plots/distrib_category.html %}

<div class="two-heatmaps-container">
	<div class="heatmap-container">
	<iframe src="plots/heatmap_stylo_centroids.html" style="width: 100%; height: 100%;"></iframe>
	</div>
	<div class="heatmap-container">
	<iframe src="plots/heatmap_stylo_centroids_2.html" style="width: 100%; height: 100%;"></iframe>
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