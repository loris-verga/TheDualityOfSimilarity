# <span style="color:#ff4500">Birds of a Feather… Fight Together?</span>
### Exploring How Similarity Shapes Conflict in Reddit’s Ecosystem

We often imagine online conflict as something that emerges between groups that share nothing in common : political opposites, rival fandoms, ideological extremes.

But what if this intuition is wrong?<br>
What if the most intense disputes don’t arise between opposites…  
but between communities that look almost exactly the <strong>same</strong>?

Reddit, with its tens of thousands of micro-communities, called subreddits, and millions of cross-subreddit references, offers the opportunity to explore this paradox. Communities cite one another, sometimes to praise, often to mock, and occasionally to even escalate into cultural wars.

Hidden inside these hyperlinks is a wealth of linguistic and psychological information:

- how people <strong>write</strong>
- how they <strong>feel</strong>
- how communities <strong>relate</strong> to one another

This leads us to a provocative set of questions:

<strong>Does similarity create harmony… or fuel conflict?</strong>

And more specifically:

<em>What does “similarity” even mean?</em><br>
Shared users? Writing style? Emotional tone?

<em>Do subreddits within the same thematic universe behave alike?</em>

<em>Is there a type of similarity so fundamental that it predicts whether an inter-community interaction will be positive or hostile?</em>

To investigate this, we rely on two large datasets from Stanford:

- <strong>850,000 inter-subreddit hyperlinks</strong> enriched with stylometric and psychological attributes  
- <strong>300-dimensional subreddit embeddings</strong> capturing patterns of shared authorship

These datasets allow us to view Reddit not as a collection of disconnected topics,  
but as a dynamic ecosystem of <strong>mindsets</strong>, <strong>writing styles</strong>, and <strong>shared populations</strong>.

In this data story, we map out what it means for two communities to be “similar”, examine how similarity relates to negativity, and ask:

<strong>Do birds of a feather flock together, or do they fight?</strong>


## <span style="color:#ff201e">A Map of Reddit’s Interactions</span>

Before we can understand why communities clash, we must first understand **how they resemble one another**.  
On Reddit, similarity is not a single dimension. It is an intricate mix of **who posts where**, **how people write**, and **what psychological traits they express**.  

To capture this, we introduce **three notions of similarity**, each one giving rise to a corresponding **distance** between subreddits:

1. **Shared Authorship Distance**  
2. **Stylometric Distance**  
3. **Psychological Distance**

Together, these distances serve as a springboard to define communities can be close, aligned, or fundamentally opposed.

## 1. Shared Authorship

Every subreddit has a “population signature”: a set of users who post there.  
The Stanford embeddings dataset compresses this information into a **300-dimensional vector** for each community.  
Two subreddits are close in this space **when many of the same users interact with both**.

Mathematically, we compare two communities using **cosine similarity**:

`cosine_sim(A, B) = (A · B) / (‖A‖ × ‖B‖)`

To turn similarity into a distance, we use:

**Shared Authorship Distance = 1 − cosine_sim(A, B)**

- **0** → communities whose authorship overlaps
- **2** → communities with no shared authorship

---

## 2. Stylometric Signatures: How Communities Write

Communities also differ in how they **sound** : their structure, complexity, and textual habits.

To capture a community’s writing style, we compute a **stylometric signature**, a vector built from features such as:

- average character count  
- fraction of uppercase letters  
- number of unique stopwords  
- average characters per sentence  
- automated readability index  

Because these features vary wildly in scale, we first apply **Z-score normalization**:

`(x − μ) / σ`

This ensures that no single feature dominates simply because it has larger numerical values.

Once each subreddit has its stylometric signature, we again compare communities via **cosine similarity**, not Euclidean distance, because we want to measure **proportions**, not magnitudes.

The resulting distance is:

`Stylometric Distance = 1 − cosine_sim(style_A, style_B)`

---

## 3. Psychological Signatures: What Communities Express

Language also reveals psychology.  
Each hyperlink post in the dataset includes **64 LIWC features** and **VADER sentiment scores**. LIWC is a text analysis program that counts words belonging to psychologically meaningful categories. Meanwhile, VADER (Valence Aware Dictionary and Sentiment Reasoner) is a rule-based sentiment analysis tool. It uses a specialized dictionary designed to accurately understand the emotions and opinions found in social media texts.

For each subreddit, we aggregate the normalized LIWC+VADER features of all its outgoing posts to define a **psychological signature**, the average emotional and cognitive expression shown by its authors when interacting with other communities.

As before, similarity is computed as a distance, using cosine similarity:

`Psychological Distance = 1 − cosine_sim(psych_A, psych_B)`

This gives us a final observation angle:  
**how similar communities are in what they feel and the emotions they display**.

---

## <span style="color:#ff201e">Exploring the Geometry of Similarity</span>

Before linking similarity to conflict, we first examine how each distance is distributed across Reddit.  
These distributions reveal the shape of each similarity space and provide intuition for how communities are built.

---

## Distribution of Distances

### **Shared Authorship Distance**

{% include basic_plots/distrib_cosine_dist_embeddings.html %}
 
The right-skewed distribution indicates that subreddits tend to be **moderately aligned** in structural space: they share enough authorship to be related, but rarely enough to be almost identical.  
Only a small fraction of pairs reach very high distances, meaning interactions between structurally opposite communities are uncommon.

---

### **Stylometric Distance**

{% include basic_plots/distrib_cosine_dist_stylo.html %}

In contrast to the embeddings distribution, stylometric distances are typically **lower**.  
This means that the **writing styles** used in cross-subreddit interactions often share structural similarities.

This suggests that users often have matching textual habits when dicussing across communities: sentence length, stopword diversity, or readability levels indicate a stylistic resemblance.

---

### **Psychological Distance**

<p align="center">
  {% include basic_plots/distrib_cosine_dist_psycho.html %}
</p>
{% include basic_plots/distrib_cosine_dist_psycho.html %}

The psychological distance distribution centers around **moderate values**, indicating that most interactions occur between subreddits whose emotional and cognitive signatures are neither identical nor opposed.

Since these signatures are derived from **LIWC** and **VADER**, this pattern suggests that users interacting between different subreddits tend to display **loosely similar psychological traits**.

---

#### <span style="color:#ff201e">Embedding Distance & Link Sentiment</span>

We first look at how subreddit embedding distances relate to the sentiment of the hyperlinks they exchange.<br>
Roughly **10% of all links** in the dataset are negative, enough to notice patterns without depicting Reddit as a civil war.

**Are positive and negative links present at different distances?**
{% include basic_plots/indiv_distrib_cosine_dist_embeddings_by_link_sentiment.html %}

Yes. Subreddit pairs with **negative** link sentiment have noticeably **larger cosine distances** than those with positive links.

This suggests that aligned communities tend to get along more (shocking, we know !), while more distant ones are more likely to disagree.

Positive links show a small bump near cosine distance **~0.1**, while negative links spike around **~0.6**.

The curves cross around <strong>0.5</strong>, below that, positive links dominate; above that, negative links take over.

---

<span style="color:#ff201e">Are the Means Actually Different?</span>

To double-check, we compared the mean cosine distances of the two sentiment groups.

A two-sample t-test (α = 0.05) confirms it:

**p ≤ 0.05**, so we reject the null hypothesis.

Communities with positive links are, on average, **closer** in embedding space than those with negative links.
Not a huge surprise ! but good to have statistical confirmation rather than intuition alone.

---

<span style="color:#ff201e">Correlation: How Strong Is the Relationship?</span>

We use a <strong>point-biserial correlation</strong>, since the distance is continuous and sentiment is binary.<br>
The result:
<ul> <li><strong>r ≈ -0.11</strong></li> <li><strong>p &lt; 0.05</strong></li> </ul>
So yes, the relationship is statistically significant, but the linear effect is <strong>very weak</strong>.<br>
A reasonable interpretation: embedding distance influences sentiment slightly, but it is far from the main factor.

---
### <span style="color:#ff201e">Causal Analysis: Does Distance Cause Negativity?</span>
To test whether being “far apart” in embedding space actually changes the sentiment of links, we frame distance as a treatment.

<ul>

  <li>
    <b>Binarizing distance</b><br>
    There is no natural cutoff in the cosine-distance distribution, so we split at the <b>median</b> — convenient and balanced (with the usual loss of granularity).
  </li>

  <li>
    <b>Visualizing Close vs. Distant Groups</b><br><br>

    {% include basic_plots/number_link_sentiment_distant_groups.html %}

    <br>
    Before controlling for confounders, the <b>Distant</b> group has about <b>twice as many negative links</b> as the Close group.
    <br><br>
    A promising signal, but we need to check whether something else might be driving the effect.
  </li>

  <li>
    <b>Controlling for Confounders</b><br>
    We fit a logistic regression to estimate a <b>propensity score</b> using the hyperlink feature vector.<br>
    One covariate stands out: <b>compound_sentiment</b>, which correlates with both distance and link sentiment, as we can see :<br>
    {% include basic_plots/distrib_compound_embeddings_causal_analysis.html %}

    To handle it properly, we match pairs with a caliper of <code>0.2 × std</code> of that feature.<br><br>


    <br>
    Matching rebalances the covariate well, so we can now measure the treatment effect clearly.
  </li>

  <li>
    <b>ATE: The Final Verdict</b><br>
    We compute the <b>Average Treatment Effect</b> (difference in mean link sentiment between the treated and control groups) and run a t-test.<br>
    The <b>ATE : -0.07</b>
    <ul>
      <li><b>p < 0.05</b></li>
      <li>→ We <b>can reject</b> the null hypothesis.</li>
    </ul>
    After controlling for confounders, we do find evidence that a <b>higher embedding distance</b> <em>causes</em> more  negativity in link sentiment (hooray !).<br><br>
    However, one must keep in mind that although this relation exists, it is weak.
  </li>

</ul>

#### <span style="color:#ff201e">Stylometric Distance & Link Sentiment</span>

Having assessed how semantic distance relates to interaction sentiment, we now turn to a complementary dimension: <b>stylometric similarity</b>.  
Stylometric distance measures how similar two subreddits’ writing styles are.

As with embedding distance, we first compare how stylometric distances vary across the two sentiment groups.

{% include basic_plots/mean_stylo_cosine_dist_across_groups_of_link_sentiment.html %}

The difference is statistically significant—negative interactions occur between slightly more stylometrically distant communities.  
But the effect size is small: about <b>0.77 vs. 0.75</b>.  

Even though the t-test returns <b>p ≤ 0.05</b> (allowing us to reject the null), the absolute difference (<b>≈ 0.017</b>) is minimal.  
Similar writing styles align mildly with positivity, but the relationship remains weak.

---

### <span style="color:#ff201e">Correlation: How Strong Is the Relationship?</span>

Applying the same point-biserial correlation used earlier:

<ul>
  <li><b>r ≈ -0.009</b></li>
  <li><b>p &lt; 0.05</b></li>
</ul>

The sign and significance mirror the embedding findings, but the strength is even weaker.  
Here, stylometric distance shows an <b>almost non-existent</b> linear relationship with link sentiment.  
While statistically detectable, it is far too small to matter in practice.

---

### <span style="color:#ff201e">Causal Analysis: Does Stylometric Distance Influence Negativity?</span>

To parallel our earlier analysis, we test whether being stylometrically “far apart” actually causes shifts in link sentiment.  
Because stylometric distance is continuous, we apply the same dichotomization strategy:

<ul>
  <li><b>Stylometric Distant (treated)</b>: distance > median</li>
  <li><b>Stylometric Close (control)</b>: distance ≤ median</li>
</ul>

We begin by comparing sentiment outcomes in these two groups.

{% include basic_plots/number_link_sentiment_distant_groups_stylo.html %}

At first glance, the distributions look similar, with only mild shifts in negativity for stylometrically distant pairs.

---

### <span style="color:#ff201e">Propensity Score & Confounder Check</span>

Following the same approach as in the embedding analysis, we estimate a <b>propensity score</b> from the hyperlink feature vector to detect potential confounders.

Unlike before, no feature displays a strong correlation with both treatment (stylometric distance) and outcome (sentiment).  
Thus, there is <b>no meaningful linear confounder</b> requiring targeted matching.

As before, matching is performed on a sampled subset for computational efficiency.

---

### <span style="color:#ff201e">ATE: The Final Verdict</span>

We estimate the <b>Average Treatment Effect</b> on the matched sample:  
the difference in mean link sentiment between the Stylometrically Distant and Stylometrically Close groups.

The **Average Treatment Effect** reaches **-0.19**. However, the p-value is equal to 0.18. At a 5% level, we cannot reject the null hypothesis that the Stylometrically Distant and Close groups have the same link sentiment.
 meme/


<p class="ignore">
    Overall, stylometric distance shows—at most—a <b>very weak</b> causal influence on sentiment.  
    Even when statistically identifiable, the practical effect remains minimal.  
    Communities that “write alike” interact slightly more positively, but the strength of this relationship is negligible compared to other factors.
</p>

#### <span style="color:#ff201e">Psychological Distance & Link Sentiment</span>

We now extend our analysis to a third dimension: <b>psychological distance</b>, a metric capturing how differently two communities express emotions, attitudes, and evaluative language.  
As before, we begin by comparing distance values across the two sentiment groups.

{% include basic_plots/mean_psycho_cosine_dist_across_groups_of_link_sentiment.html %}

The difference in sample means is small, only about <b>0.1</b>, yet the confidence intervals indicate that the gap might be statistically significant.  
With a p-value ≤ 0.05, we reject the null hypothesis and conclude that negative interactions occur the most between psychologically more distant communities.

The <b>t-statistic (-75.44)</b> is notably large, far exceeding the stylometric result.  
This reflects a strong statistical signal, but the <b>practical</b> impact remains limited: psychological distance is associated with more negativity, though the effect size is still weak.

---

### <span style="color:#ff201e">Correlation: How Strong Is the Relationship?</span>

We again use the <b>point-biserial correlation</b> to quantify the linear relationship between psychological distance and link sentiment.

<ul>
  <li><b>r ≈ -0.08</b></li>
  <li><b>p &lt; 0.05</b></li>
</ul>

The correlation is statistically significant and stronger than for stylometric distance (10 times larger!), yet remains modest compared with shared authorship.  
Psychological distance therefore captures sentiment-relevant variation, but only partially.

---

### <span style="color:#ff201e">Causal Analysis: Does Psychological Distance Influence Negativity?</span>

To determine whether psychological distance <i>causally</i> affects link sentiment, we apply the same causal framework used in the previous distance analyses.  
Even though the linear correlation is small, causal effects may still exist, possibly non-linear or shaped by confounders, so we use propensity score matching.

As before, we convert the continuous distance into a binary treatment:

<ul>
  <li><b>Psycho Distant (treated)</b>: distance &gt; median</li>
  <li><b>Psycho Close (control)</b>: distance ≤ median</li>
</ul>

We begin by visualizing sentiment distributions across these two groups.

{% include basic_plots/number_link_sentiment_distant_groups_psycho.html %}

At first glance, the distributions appear similar, with only a mild shift toward negativity for psychologically distant communities.

---

### <span style="color:#ff201e">Propensity Score & Confounder Check</span>

We estimate a <b>propensity score</b> using the hyperlink feature vector, following the same procedure as before.  
To detect potential confounders, we inspect correlations between features, the treatment indicator, and the outcome.

One feature, <b>the compound_sentiment</b>, shows a strong link with both treatment and outcome, marking it as a key confounder.  
To mitigate its influence, we enforce a matching constraint: matched pairs must differ by less than <b>0.2 ×</b> the feature’s standard deviation.

As in previous analyses, matching is performed on a subsample for computational efficiency.

---

### <span style="color:#ff201e">ATE: Final Verdict</span>

We compute the <b>Average Treatment Effect (ATE)</b> as the difference in mean link sentiment between the Psychologically Distant (treated) and Psychologically Close (control) groups within the matched sample.  
A t-test will then assess the statistical significance of this difference.

  <li>
    The <b>ATE : -0.08</b>
    <ul>
      <li><b>p < 0.05</b></li>
      <li>→ We <b>can reject</b> the null hypothesis.</li>
    </ul>
    Great news! We find evidence that a <b>higher psychological distance</b> <em>causes</em> more negativity in link sentiment.<br>
    In other words, users who interact from a relatively different emotional space show more negativity than those with similar emotional expressions.<br>
    Once again, this relation exists but is weak.

  </li>

---

<p class="ignore">
    Overall, psychological distance exhibits a clearer association with negativity than stylometric similarity, yet its practical impact remains small.  
    Emotional expression shapes how communities interact, but it accounts for only a limited share of sentiment variation relative to other structural factors.
</p>



## <span style="color:#ff201e">Visualizing the Psychological Space</span>

To better understand how signatures relate across communities, we can visualize the high-dimensional psychological space into two dimensions.  
We present both **PCA** (linear structure) and **t-SNE** (local non-linear structure).
PCA identifies the 2D projection plane that captures the maximum possible variance from the psychological features. On the other hand, t-SNE is a tool that reveals local structures and potential clusters by creating a 2D map that preserves the neighborhood relationships from the original high-dimensional space. We use it here to see if the psychological profiles form distinct groups.

<div style="display:flex; gap:20px; justify-content:center; max-width:1200px; margin:auto;">
    <div style="flex:1; min-width:0;">
        {% include basic_plots/tsne_stylo.html %}
    </div>

    <div style="flex:1; min-width:0;">
        {% include basic_plots/pca_psycho.html %}
    </div>
</div>


---

### **What does it all mean ?**

#### **PCA**
The first two principal components explain **24.07%** of the total variance. As the original data is of high dimension, this value is not inherently bad to grasp to main tendency.
The resulting projection forms a **dense, continuous cloud** without sharp separations, suggesting that subreddits vary smoothly in their psychological tone.  

#### **t-SNE**
While t-SNE also reveals a large central mass, it uncovers **peripheral clusters**. 
These clusters reflect **locally cohesive psychological communities**, even though the global landscape remains continuous.

These insights set the context a deeper question:  
**How does similarity in each space relate to negativity in cross-subreddit interactions?**

---

#### <span style="color:#ff201e">Within– and Inter-Category Analysis</span>

<div class="section">

<h4>Introduction</h4>

We assigned each of the ~51'000 subreddits in our embeddings dataframe to one of thirteen categories using an LLM.  
The list covers broad thematic areas:

<ul>
  <li>Lifestyle</li>
  <li>Miscellaneous</li>
  <li>Gaming</li>
  <li>Humour &amp; Memes</li>
  <li>Adult &amp; Pornography</li>
  <li>Technology</li>
  <li>Science, Nature &amp; Education</li>
  <li>Music</li>
  <li>Politics &amp; News</li>
  <li>Countries &amp; Cities</li>
  <li>Sport</li>
  <li>Automobile</li>
  <li>Cryptocurrencies</li>
</ul>

<div style="background:#f7f7f7; padding:12px; border-radius:8px; font-size:0.9rem;">
<b>Note on accuracy:</b> Subreddit names are often uninformative, and thirteen categories are far too few to reflect the true diversity of Reddit. Expect misclassifications and broad bins that act more like umbrellas than precise labels.
</div>

Our aim here is simpler: look for large-scale patterns. We do not need perfect labels to detect whether broad thematic groups behave differently, interact differently, or exhibit distinct “signatures.”

{% include basic_plots/distrib_category.html %}

As expected, Lifestyle, Miscellaneous, Gaming, and Humour &amp; Memes dominate by sheer volume. To avoid being misled by this imbalance, we rely on confidence intervals and other measures of uncertainty throughout the analysis.

</div>



<hr style="margin:40px 0;">



### <span style="color:#ff201e">1) Relating Distances and Categories</span>

We work at the category level rather than at the individual subreddit level.  
For each category, we compute a **centroid** representing the average embedding or signature of its subreddits. These centroids allow us to assess:

<ul>
  <li><b>Alignment between categories</b> (how similar their centroids are)</li>
  <li><b>Cohesion within categories</b> (how close individual subreddits are to their centroid)</li>
</ul>

The cosine distance scale remains the same:  
<div style="text-align:center; margin-top:10px;">
<span style="font-size:0.9rem; background:#eef1f5; padding:6px 10px; border-radius:6px;">0 = perfectly aligned, &nbsp; 2 = maximally different</span>
</div>

For stylometric and psychological distances, an extra step is required: we first compute a subreddit-level signature, then take the mean per category.



---

## <span style="color:#ff201e">a) Authorship Distance & Categories</span>

<div style="text-align:center;">
  <img src="assets/img/cluster/heatmap_embeddings.png" width="70%" style="margin-right:2%;" alt="Authorship centroid distances">
  <div style="font-size:0.85rem;"><em>Embeddings centroid comparisons</em></div>
</div>

<h4>Centroid alignment: moderately similar</h4>
Generalist categories like Miscellaneous, Lifestyle, and Humour &amp; Memes are all relatively close to each other. These categories spread widely in the embedding space and overlap heavily with others. Gaming and Technology, on the other hand, sit closer together for intuitive reasons: users often post in both, and the topics naturally relate.

<h4>Subreddit cohesion: surprisingly weak</h4>
The right heatmap shows that many subreddits are not especially close to their assigned category’s centroid. In some categories, they are nearly equidistant from several centroids. Why?

<ul>
  <li>LLM classification errors: misleading subreddit names produce noisy assignments.</li>
  <li>Thirteen categories are too coarse for Reddit’s complexity.</li>
  <li>Reddit is inherently fluid: overlapping interests create overlapping clusters.</li>
</ul>

<p>
  To evaluate how well our clustering separates subreddit groups, we use the 
  <b>silhouette score</b>. It measures how similar a point is to its own cluster 
  compared to points in other clusters.
</p>

<div style="
  border: 1px solid #ddd;
  padding: 0.8rem 1rem;
  border-radius: 6px;
  background:#fafafa;
  text-align:center;
  margin: 1rem 0;
  font-size:1.1rem;
">
  <em>\( s = \frac{b - a}{\max(a,\, b)} \)</em>
</div>

<p>
  where:<br>
  • <b>a</b> = average distance to other points within the same cluster<br>
  • <b>b</b> = lowest average distance to points in any <em>other</em> cluster<br><br>
  The silhouette score ranges from -1 to 1, with higher values indicating 
  more coherent and well-separated clusters.
</p>

<div style="background:#f7f7f7; padding:12px; border-radius:8px; font-size:0.9rem; width: fit-content;">
<b>Silhouette score: -0.08</b>
</div>

A silhouette score near 0 confirms that subreddit clusters overlap, reflecting the lack of clear category boundaries. Contrary to expectations of distinct, isolated clusters, Reddit’s broad ecosystem creates thousands of overlapping categories, resulting in a large and interconnected mass of subreddits rather than well-defined clusters.

---

## <span style="color:#ff201e">b) Stylometric Signatures & Categories</span>

<div class="two-heatmaps-container">
	<div class="heatmap-container">
	<iframe src="plots/heatmap_stylo_centroids.html" style="width: 100%; height: 100%;"></iframe>
	</div>
	<div class="heatmap-container">
	<iframe src="plots/heatmap_stylo_centroids_2.html" style="width: 100%; height: 100%;"></iframe>
	</div>
</div>

The left heatmap shows a different picture: stylometric centroids are **more separated** as the cosine distances are larger. Stylometric signatures of categories constitute a strong enough identity to indicate how stylometrically different two subreddit categories are.

For example:

<div style="background:#eef7ff; padding:10px; border-left:4px solid #79a6d2; border-radius:4px; margin:12px 0; font-size:0.9rem;">
<b>Gaming ↔ Technology stylometric distance: ~0.1</b><br>
Such a small distance was expected, as Gaming and Technology subreddits share similar centers of interests, potentially leading similar syntactical structures.
</div>

<h4>Cohesion: still weak</h4>
The right plot shows strong overlap between subreddit signatures. While stylometric clusters appear separated at first glance, they are not fully cohesive. This may be because users from one category borrow textual traits from related categories (e.g., gaming and technology). Additionally, averaging all stylometric features smooths out unique category characteristics.

<h4>Silhouette score</h4>
<div style="background:#f7f7f7; padding:12px; border-radius:8px; font-size:0.9rem; width: fit-content;">
<b>Silhouette score: -0.09</b>
</div>

Close to zero again. Categories differ in stylometric identity but overlap heavily in practice.



---

## <span style="color:#ff201e">c) Psychological Signatures & Categories</span>

<div style="text-align:center;">
  <img src="assets/img/cluster/heatmap_psy.png" width="70%" style="margin-right:2%;" alt="Psychological centroid distances">
  <div style="font-size:0.85rem;"><em>Psychological centroid comparisons.</em></div>
</div>

The left heatmap echoes the stylometric one: categories differ substantially in their emotional and evaluative styles.  
On the right, however, we finally see a hint of cohesion. Subreddits tend to sit closer to their own psychological centroid than to others, which can be deduced through the lower values on the diagonal.

Psychological signatures distinguish categories more clearly than stylometric signatures, as subreddits cluster closer to their own category. This suggests that different community clusters have distinct and well-separated “psychological” states.

<h4>Silhouette score</h4>
<div style="background:#f7f7f7; padding:12px; border-radius:8px; font-size:0.9rem; width: fit-content;">
<b>Silhouette score: -0.05</b>
</div>

Still close to zero, but slightly better. Clusters remain overlapping, yet psychological signatures yield a bit more structure.



<hr style="margin:40px 0;">



## <span style="color:#ff201e">Categories & Distances: Conclusion</span>

We examined authorship, stylometric and psychological distances through the lens of subreddit categories. The main findings:

<ul>
  <li><b>Authorship (embedding) distance:</b> Categories are weakly separated. Subreddits overlap widely in embedding space. With only thirteen categories, strong granularity is not possible.</li>

  <li><b>Stylometric distance:</b> Centroids differ substantially in writing style, though subreddits within a category remain dispersed. Overlaps dominate.</li>

  <li><b>Psychological distance:</b> Similar behavior to stylometric distance, but with slightly more cohesion within categories.</li>
</ul>

<div style="background:#eef1f5; padding:15px; border-radius:10px; margin-top:20px;">
<b>All silhouette scores are near zero.</b>  
This confirms that Reddit categories heavily overlap across all distance types.   
Still, stylometric and psychological signatures show potential as light forms of category identity. They are not strong enough to define boundaries, but they do capture broad differences in how communities write and emotionally express themselves.
</div>


<hr style="margin:40px 0;">


### <span style="color:#ff201e">2) Negativity & Categories</span>

We now take advantage of our hyperlink network, where each edge carries a sentiment from a <em>source</em> subreddit to a <em>target</em> subreddit, to understand how negativity circulates across categories.

At this stage, we step beyond distances and look directly at how categories interact through negative links.



#### Negative interactions between categories

Before relating negativity to distances, we first inspect how negativity flows between categories at a global scale.

<div class="heatmap-container">
<iframe src="plots/heatmap_nbr_negative_links.html" style="width: 100%; height: 100%;"></iframe>
</div>

From the heatmap, two main observations emerge:

<ul>
  <li>
    <b>1. Internal negativity is common.</b><br>
    For many target categories, a substantial share of incoming negative links originates from the same category.  
    Subreddits frequently criticize, mock, or conflict with others in their own thematic sphere.
  </li>

  <li>
    <b>2. Some categories emit far more negativity than others.</b><br>
    Categories such as <em>Politics &amp; News</em> or <em>Humour &amp; Memes</em> generate large amounts of negative interactions, reflecting high polarization or a tendency toward derision.
  </li>
</ul>


The distribution plot confirms this:
{% include basic_plots/distrib_negative_links_categories.html %}

<ul>
  <li>
    <b>Humour &amp; Memes</b> is the largest hub of negativity: it emits far more negative links than it receives.
  </li>
  <li>
    Other categories behave asymmetrically: some attract negativity while emitting much less of it.
  </li>
</ul>

This reinforces the idea that each thematic community on Reddit has its own relational “profile”: some attack, some are attacked, and some do both.



<hr style="margin:40px 0;">



### <span style="color:#ff201e">3) Negativity, Distances & Categories</span>

Earlier , we established a key relationship:

<div style="background:#eef1f5; padding:12px; border-radius:8px; width: fit-content; font-size:0.9rem;">
<b>Negative links → larger cosine distances<br>
Positive links → smaller cosine distances</b> 
</div>
This causal relationship was found for both Authorship and Psychological Distances.

This was supported by a t-test and a causal analysis.

We now extend this to incorporate categories and hyperlink types.



#### Within-cluster vs inter-cluster hyperlinks

To understand how category structure interacts with distances and sentiment, we separate two cases:

<ul>
  <li><b>Within-cluster links:</b> source and target subreddits belong to the same category.</li>
  <li><b>Inter-cluster links:</b> source and target subreddits belong to different categories.</li>
</ul>

We then examine how the **mean cosine distance (authorship distance)** varies across:

- <b>Link sentiment</b> (negative or positive),
- <b>Hyperlink type</b>  (within vs inter cluster).

{% include basic_plots/mean_authorship_dist_for_type_of_links.html %}



#### Key insight

From the plot, we observe—at high confidence (non-overlapping 95% CIs)—the following:

<div style="background:#f7f7f7; padding:15px; border-radius:8px; margin:20px 0;">
<b>1. Smaller distances → positive links (already established causally).</b><br>
<b>2. Inter-cluster distances are larger than within-cluster distances.</b><br>
<b>3. The trend holds for both positive and negative links.</b>
</div>

This pattern is a clear instance of  
<a href="https://en.wikipedia.org/wiki/Simpson%27s_paradox" target="_blank"><b>Simpson’s paradox</b></a>:  
the global trend strengthens once we control for category structure.



#### Category-level decomposition

We further break down mean cosine distance by category and by sentiment:

{% include basic_plots/mean_authorship_dist_for_type_of_links_disentangled_by_cat_within.html %}
{% include basic_plots/mean_authorship_dist_for_type_of_links_disentangled_by_cat_inter.html %}


The same structure emerges:

<ul>
  <li>Within each category, positive links consistently have smaller cosine distances.</li>
  <li>Inter-cluster links have larger distances overall.</li>
</ul>

This strongly supports <b>Hypothesis n°7</b>:  
<b>source and target subreddit pairs from the same category exhibit smaller mean cosine distances than pairs from different categories.</b>



<hr style="margin:40px 0;">



### <span style="color:#ff201e">Beyond Authorship Distance: Stylometric & Psychological Distances</span>

We repeat the same decomposition for the other two signature-based distances.

<div style="display:flex; gap:20px; justify-content:center; max-width:1200px; margin:auto;">
    
    <div style="flex:1; min-width:0;">
        <div style="width:100% !important; height:auto !important; overflow:hidden;">
            {% include basic_plots/mean_stylo_dist_for_type_of_links.html %}
        </div>
    </div>

    <div style="flex:1; min-width:0;">
        <div style="width:100% !important; height:auto !important; overflow:hidden;">
            {% include basic_plots/mean_psycho_dist_for_type_of_links.html %}
        </div>
    </div>

</div>


#### Psychological distance

<ul>
  <li>The pattern mirrors authorship distance: positive links → smaller distances; negative → larger.</li>
  <li>Within-cluster distances are smaller than inter-cluster distances.</li>
</ul>

This also supports Hypothesis n°7.



#### Stylometric distance

Stylometric distance behaves differently:

<ul>
  <li>Distances are nearly identical for positive and negative links.</li>
  <li>Within-cluster and inter-cluster stylometric distances show only small differences.</li>
</ul>

This indicates that stylometric features are **less predictive of sentiment** than authorship or psychological distances, even though they still exhibit a mild within- vs inter-cluster difference (supporting Hypothesis n°7).



<hr style="margin:40px 0;">



### <span style="color:#ff201e">Overall Summary</span>

Across authorship, psychological and stylometric distances, we find:

<ul>
  <li><b>Negative interactions → larger distances</b></li>
  <li><b>Positive interactions → smaller distances</b></li>
  <li><b>Distance gaps widen when moving from within-cluster to inter-cluster links</b></li>
  <li><b>The effect is strongest for authorship distance, moderate for psychological distance, and weakest for stylometric distance</b></li>
</ul>

<div style="background:#eef1f5; padding:15px; border-radius:10px; margin-top:20px;">
Taken together, these results reveal how category structure shapes the relationship between semantic distance and negativity:  
<b>communities that are closer in content tend to interact more positively, while distant communities interact more negatively, especially across category boundaries.</b>
</div>


<hr style="margin:40px 0;">


### <span style="color:#ff201e">4) Case Study: Humour &amp; Memes</span>

On the stylometric and psychological distance heatmaps (part 1), a clear pattern emerged:  
the <b>“Humour &amp; Memes”</b> category appears well separated from all others, with higher centroid cosine distances for both signatures.  

This naturally leads to the following speculation:

<ul>
  <li><b>Stylometric reasons:</b> meme culture often produces short, fragmented posts, frequent uppercase letters, minimal syntax, image-based humour, and text designed primarily for mockery.</li>
  <li><b>Psychological reasons:</b> these communities tend to express negative, sarcastic, or hostile tones. LIWC features related to anger, negativity, or swearing may therefore be elevated.</li>
</ul>

These distinctive patterns may cause the “Humour &amp; Memes” centroid to be unusually distant from others: unlike most categories, these subreddits systematically make fun of other users, other subreddits, or entire topics.

We now evaluate whether this is true in the data.



#### Comparing “Humour & Memes” centroids to all other categories

Our goal is simple:  
<b>compare the stylometric and psychological centroids of “Humour &amp; Memes” to the median centroid of all other categories</b>.

<div style="text-align:center;">
  <img src="assets/img/cluster/humour_memes_deviation_stylometric.png" width="70%" alt="Humour & Memes deviation plot">
  <img src="assets/img/cluster/humour_memes_deviation_psychological.png" width="70%" alt="Humour & Memes deviation plot">
  <div style="font-size:0.85rem;"><em>Deviation of stylometric (top) and psychological (bottom) features compared to the median centroid of all categories.</em></div>
</div>
{% include basic_plots/deviation_stylometric_features.html %}
{% include basic_plots/deviation_psychological_features.html %}


#### Stylometric deviations

As expected:

<ul>
  <li><b>Uppercase fraction</b> is much higher than the median of all categories.</li>
  <li><b>Characters, words, and sentences per post</b> are significantly smaller.</li>
</ul>

Even without inspecting the textual content, this aligns with our expectations about meme-style communication: short, intense, loud, and sharp.



#### Psychological deviations

Psychological signatures show an even stronger deviation:

<ul>
  <li><b>Swear words</b> dominate.</li>
  <li><b>Anger</b>-related dimensions are clearly above typical levels.</li>
  <li><b>General negative emotion</b> signals are significantly elevated.</li>
</ul>

This reinforces the idea that “Humour &amp; Memes” communities contribute disproportionately to negative content on Reddit.



<hr style="margin:40px 0;">



### <span style="color:#ff201e">Where does the negativity go?</span>

Earlier (section 2), we observed that:

<div style="background:#f7f7f7; padding:15px; border-radius:10px; width:fit-content;">
<b>“Humour &amp; Memes” emits more than 25,000 negative hyperlinks.</b><br>
Yet it does <b>not</b> receive an unusually high number of negative links in return.
</div>

This asymmetry is striking and begs the question:

<b>Which subreddits are responsible for emitting this negativity, and where do they send it?</b>



### Subreddits emitting the most negative links

Below is the output from the analysis, displayed in a clean table:

<div style="margin-top:10px;">
<table style="border-collapse:collapse; width:70%; font-size:0.9rem;">
  <thead>
    <tr style="background:#ffefef;">
      <th style="padding:8px; border:1px solid #ccc;">Source Subreddit</th>
      <th style="padding:8px; border:1px solid #ccc;">Negative Links</th>
    </tr>
  </thead>
  <tbody>
    <tr><td style="padding:8px; border:1px solid #ccc;">circlebroke2</td><td style="padding:8px; border:1px solid #ccc;">1768</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">shitpost</td><td style="padding:8px; border:1px solid #ccc;">1307</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">shitredditsays</td><td style="padding:8px; border:1px solid #ccc;">1034</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">shitstatistssay</td><td style="padding:8px; border:1px solid #ccc;">982</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">shitamericanssay</td><td style="padding:8px; border:1px solid #ccc;">792</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">circlebroke</td><td style="padding:8px; border:1px solid #ccc;">774</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">evenwithcontext</td><td style="padding:8px; border:1px solid #ccc;">771</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">shitliberalssay</td><td style="padding:8px; border:1px solid #ccc;">765</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">gamingcirclejerk</td><td style="padding:8px; border:1px solid #ccc;">624</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">fitnesscirclejerk</td><td style="padding:8px; border:1px solid #ccc;">599</td></tr>
  </tbody>
</table>
</div>



### Which subreddits do they target?

Displayed below is the structured version of your output showing the main targets for each source.

<div style="margin-top:10px;">
<table style="border-collapse:collapse; width:95%; font-size:0.88rem;">
  <thead>
    <tr style="background:#eef5ff;">
      <th style="padding:8px; border:1px solid #ccc;">Source Subreddit</th>
      <th style="padding:8px; border:1px solid #ccc;">Target Subreddit</th>
      <th style="padding:8px; border:1px solid #ccc;"># Negative Links</th>
    </tr>
  </thead>
  <tbody>
    <!-- shitstatistssay -->
    <tr><td>shitstatistssay</td><td>news</td><td>56</td></tr>
    <tr><td>shitstatistssay</td><td>politics</td><td>48</td></tr>
    <tr><td>shitstatistssay</td><td>worldnews</td><td>39</td></tr>
    <tr><td>shitstatistssay</td><td>libertarian</td><td>37</td></tr>
    <tr><td>shitstatistssay</td><td>todayilearned</td><td>36</td></tr>

    <!-- shitredditsays -->
    <tr><td>shitredditsays</td><td>twoxchromosomes</td><td>120</td></tr>
    <tr><td>shitredditsays</td><td>worldnews</td><td>41</td></tr>
    <tr><td>shitredditsays</td><td>todayilearned</td><td>33</td></tr>
    <tr><td>shitredditsays</td><td>wtf</td><td>30</td></tr>
    <tr><td>shitredditsays</td><td>videos</td><td>29</td></tr>

    <!-- shitpost -->
    <tr><td>shitpost</td><td>showerthoughts</td><td>54</td></tr>
    <tr><td>shitpost</td><td>adviceanimals</td><td>50</td></tr>
    <tr><td>shitpost</td><td>videos</td><td>46</td></tr>
    <tr><td>shitpost</td><td>tifu</td><td>45</td></tr>
    <tr><td>shitpost</td><td>askreddit</td><td>43</td></tr>

    <!-- shitliberalssay -->
    <tr><td>shitliberalssay</td><td>socialism</td><td>29</td></tr>
    <tr><td>shitliberalssay</td><td>askreddit</td><td>28</td></tr>
    <tr><td>shitliberalssay</td><td>worldnews</td><td>28</td></tr>
    <tr><td>shitliberalssay</td><td>news</td><td>22</td></tr>
    <tr><td>shitliberalssay</td><td>todayilearned</td><td>21</td></tr>

    <!-- shitamericanssay -->
    <tr><td>shitamericanssay</td><td>todayilearned</td><td>39</td></tr>
    <tr><td>shitamericanssay</td><td>news</td><td>32</td></tr>
    <tr><td>shitamericanssay</td><td>pics</td><td>26</td></tr>
    <tr><td>shitamericanssay</td><td>videos</td><td>26</td></tr>
    <tr><td>shitamericanssay</td><td>worldnews</td><td>26</td></tr>

    <!-- gamingcirclejerk -->
    <tr><td>gamingcirclejerk</td><td>gaming</td><td>48</td></tr>
    <tr><td>gamingcirclejerk</td><td>games</td><td>46</td></tr>
    <tr><td>gamingcirclejerk</td><td>pcmasterrace</td><td>36</td></tr>
    <tr><td>gamingcirclejerk</td><td>ps4</td><td>35</td></tr>
    <tr><td>gamingcirclejerk</td><td>pcgaming</td><td>33</td></tr>

    <!-- fitnesscirclejerk -->
    <tr><td>fitnesscirclejerk</td><td>bodybuilding</td><td>37</td></tr>
    <tr><td>fitnesscirclejerk</td><td>fitness</td><td>25</td></tr>
    <tr><td>fitnesscirclejerk</td><td>weightroom</td><td>22</td></tr>
    <tr><td>fitnesscirclejerk</td><td>pics</td><td>18</td></tr>
    <tr><td>fitnesscirclejerk</td><td>adviceanimals</td><td>14</td></tr>

    <!-- evenwithcontext -->
    <tr><td>evenwithcontext</td><td>askreddit</td><td>97</td></tr>
    <tr><td>evenwithcontext</td><td>wtf</td><td>39</td></tr>
    <tr><td>evenwithcontext</td><td>funny</td><td>34</td></tr>
    <tr><td>evenwithcontext</td><td>pics</td><td>28</td></tr>
    <tr><td>evenwithcontext</td><td>gifs</td><td>27</td></tr>

    <!-- circlebroke2 -->
    <tr><td>circlebroke2</td><td>pics</td><td>77</td></tr>
    <tr><td>circlebroke2</td><td>funny</td><td>74</td></tr>
    <tr><td>circlebroke2</td><td>videos</td><td>73</td></tr>
    <tr><td>circlebroke2</td><td>news</td><td>68</td></tr>
    <tr><td>circlebroke2</td><td>adviceanimals</td><td>65</td></tr>

    <!-- circlebroke -->
    <tr><td>circlebroke</td><td>pics</td><td>51</td></tr>
    <tr><td>circlebroke</td><td>videos</td><td>43</td></tr>
    <tr><td>circlebroke</td><td>news</td><td>42</td></tr>
    <tr><td>circlebroke</td><td>askreddit</td><td>41</td></tr>
    <tr><td>circlebroke</td><td>funny</td><td>36</td></tr>
  </tbody>
</table>
</div>



#### What do we learn from this?

A key pattern stands out:

<div style="background:#fff4db; padding:15px; border-radius:10px;">
<b>The subreddits emitting the most negativity within “Humour &amp; Memes” almost never target each other.</b><br><br>
Instead, they target <b>general-purpose</b> or <b>topic-specific</b> communities such as<br>
<em>askreddit, todayilearned, gaming, worldnews, pics, funny, fitness, movies…</em>
</div>

These communities behave almost like “commentary” or “parody” subreddits that take aim at mainstream Reddit spaces, not at humour-oriented neighbours.



<div style="text-align:center; margin-top:20px;">
  <img src="assets/img/cluster/bipartite_humor_memes_negative_links.png" width="85%" alt="Bipartite graph of negative links">
  <div style="font-size:0.85rem;"><em>Bipartite representation of negative links from Humour &amp; Memes subreddits to their targets.</em></div>
</div>

<p>
The bipartite graph reveals that while <em>Humor & Memes</em> subreddits often emit negative links, they rarely target each other. Instead, the negativity is usually directed toward broader, more neutral subreddits outside the humor ecosystem.
</p>

<p>
For instance, <strong>gamingcirclejerk</strong> shows strong negative linking toward general gaming communities like <em>pcgaming</em>, <em>ps4</em>, or <em>games</em>. Similarly, <strong>fitnesscirclejerk</strong> directs negativity toward mainstream fitness subreddits such as <em>fitness</em> and <em>bodybuilding</em>.
</p>

<p>
Overall, one can search almost any topic within <em>Humor & Memes</em> and observe the same pattern: these subreddits tend to cast negative references toward topic-focused communities rather than toward other humor subreddits. Below is an example using <strong>nba</strong>.
</p>




### Additional example: the “nbacirclejerk” pattern

To illustrate how general this behaviour is, here is the table generated for the topic “NBA”:

<div style="margin-top:20px;">
<table style="border-collapse:collapse; width:60%; font-size:0.88rem;">
  <thead>
    <tr style="background:#f0f7ff;">
      <th style="padding:8px; border:1px solid #ccc;">Source Subreddit</th>
      <th style="padding:8px; border:1px solid #ccc;">Target Subreddit</th>
      <th style="padding:8px; border:1px solid #ccc;"># Negative Links</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>nbacirclejerk</td><td>nba</td><td>31</td></tr>
    <tr><td>nbacirclejerk</td><td>torontoraptors</td><td>5</td></tr>
    <tr><td>nbacirclejerk</td><td>bostonceltics</td><td>4</td></tr>
    <tr><td>nbacirclejerk</td><td>warriors</td><td>3</td></tr>
    <tr><td>nbacirclejerk</td><td>chicagobulls</td><td>2</td></tr>
  </tbody>
</table>
</div>

Again, we see the same structure:  
<b>a humour-oriented circlejerk subreddit mocking the “serious” version of the topic.</b>



<hr style="margin:40px 0;">



### <span style="color:#ff201e">Conclusion of the Case Study</span>

This case study reveals a facet of Reddit that would have been very difficult to uncover without:

- the category classification,  
- the hyperlink network,  
- and the signature-based distance analysis.

Our analysis shows that:

<ul>
  <li>“Humour &amp; Memes” subreddits have <b>distinct stylometric and psychological profiles</b>, far from the Reddit norm.</li>
  <li>They generate a <b>massive amount of negativity</b>, yet do not receive much of it.</li>
  <li>They do <b>not</b> primarily target each other, but rather general or topic-oriented communities.</li>
  <li>This reveals an ecosystem of subreddits dedicated to <b>mocking entire topics</b> and the communities built around them.</li>
</ul>

<div style="background:#eef1f5; padding:18px; border-radius:10px; margin-top:20px;">
<b>Overall:</b><br>
While this case study started with a focus on unusual stylometric and psychological signatures,  
it ultimately revealed a broader pattern: a network of humor-oriented subreddits that plays a central role in shaping Reddit’s negativity dynamics.
</div>






