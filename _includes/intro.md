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

<p align="center">
  <img src="assets/img/distrib_embeddings.png" width="70%" alt="Histogram of Shared Authorship Distances">
  <br>
  <em>Figure : Distribution of shared authorship distances between subreddit pairs.</em>
</p>
 
The right-skewed distribution indicates that subreddits tend to be **moderately aligned** in structural space: they share enough authorship to be related, but rarely enough to be almost identical.  
Only a small fraction of pairs reach very high distances, meaning interactions between structurally opposite communities are uncommon.

---

### **Stylometric Distance**

<p align="center">
  <img src="assets/img/distrib_stylo.png" width="70%" alt="Histogram of Stylometric Distances">
  <br>
  <em>Figure : Distribution of stylometric distances between subreddit pairs.</em>
</p>

In contrast to the embeddings distribution, stylometric distances are typically **lower**.  
This means that the **writing styles** used in cross-subreddit interactions often share structural similarities.

This suggests that users often have matching textual habits when dicussing across communities: sentence length, stopword diversity, or readability levels indicate a stylistic resemblance.

---

### **Psychological Distance**

<p align="center">
  <img src="assets/img/distrib_psych.png" width="70%" alt="Histogram of Psychological Distances">
  <br>
  <em>Figure : Distribution of psychological distances between subreddit pairs.</em>
</p>

The psychological distance distribution centers around **moderate values**, indicating that most interactions occur between subreddits whose emotional and cognitive signatures are neither identical nor opposed.

Since these signatures are derived from **LIWC** and **VADER**, this pattern suggests that users interacting between different subreddits tend to display **loosely similar psychological traits**.

---

#### <span style="color:#ff201e">Embedding Distance & Link Sentiment</span>

We first look at how subreddit embedding distances relate to the sentiment of the hyperlinks they exchange.<br>
Roughly **10% of all links** in the dataset are negative, enough to notice patterns without depicting Reddit as a civil war.

**Are positive and negative links present at different distances?**
<div style="text-align:center;"> <p style="max-width:70%; margin:auto;"> <img src="assets/img/plot_dist_cosine_by_link_sentiment.png" width="100%" alt="Distribution of cosine distances by link sentiment"> <br> <em>Distribution of cosine distances for positive vs. negative links.</em> </p> </div>

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

    <div style="text-align:center;">
      <img src="assets/img/barplot_linksentiment_by_treatment.png" width="55%" alt="Link sentiment by treatment">
      <div><em>Proportion of positive/negative links in Close vs. Distant groups.</em></div>
    </div>

    <br>
    Before controlling for confounders, the <b>Distant</b> group has about <b>twice as many negative links</b> as the Close group.
    <br><br>
    A promising signal, but we need to check whether something else might be driving the effect.
  </li>

  <li>
    <b>Controlling for Confounders</b><br>
    We fit a logistic regression to estimate a <b>propensity score</b> using the hyperlink feature vector.<br>
    One covariate stands out: <b>compound_sentiment</b>, which correlates with both distance and link sentiment.<br>
    To handle it properly, we match pairs with a caliper of <code>0.2 × std</code> of that feature.<br><br>

    <div style="text-align:center;">
      <img src="assets/img/dist_compound_sentiment_by_is_distant.png" width="55%" alt="Distribution of compound sentiment after matching">
      <div><em>Distribution of compound_sentiment after matching. Balance achieved.</em></div>
    </div>

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

<div style="text-align:center;">
  <img src="assets/img/plot_means_stylometric_by_sentiment.png" width="70%" alt="Mean stylometric distance by sentiment">
  <div><em>Mean stylometric distance for positive vs. negative interactions (95% CI).</em></div>
</div>

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

<div style="text-align:center;">
  <img src="assets/img/barplot_linksentiment_by_stylometric_treatment.png" width="55%" alt="Link sentiment by stylometric distance groups">
  <div><em>Proportion of positive/negative links across Stylometric Close vs. Distant pairs.</em></div>
</div>

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

<div style="text-align:center;">
  <img src="assets/img/plot_means_psychological_by_sentiment.png" width="70%" alt="Mean psychological distance by sentiment">
  <div><em>Mean psychological distance for positive vs. negative interactions (95% CI).</em></div>
</div>

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

<div style="text-align:center;">
  <img src="assets/img/barplot_linksentiment_by_psychological_treatment.png" width="55%" alt="Link sentiment by psychological distance groups">
  <div><em>Proportion of positive/negative links across Psycho Close vs. Psycho Distant pairs.</em></div>
</div>

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

<div style="display:flex; justify-content:center; gap:20px; flex-wrap:wrap;">

  <p align="center" style="max-width:45%;">
    <img src="assets/img/pca_psych.png" width="100%" alt="PCA of Psychological Signatures">
    <br>
    <em>PCA projection of psychological distances.</em>
  </p>

  <p align="center" style="max-width:45%;">
    <img src="assets/img/tsne_psych.png" width="100%" alt="t-SNE of Psychological Signatures">
    <br>
    <em>t-SNE projection of psychological distances.</em>
  </p>

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

<div style="text-align:center; margin-top:20px;">
  <img src="assets/img/cluster/category_distribution.png" width="70%" alt="Distribution of subreddits per category">
  <div style="font-size:0.85rem;"><em>Distribution of subreddits per category.</em></div>
</div>

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

<div style="text-align:center;">
  <img src="assets/img/cluster/heatmap_stylo.png" width="70%" style="margin-right:2%;" alt="Stylometric centroid distances">
  <div style="font-size:0.85rem;"><em>Stylometric centroid comparisons.</em></div>
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

We now take advantage of our hyperlink network—where each edge carries a sentiment from a <em>source</em> subreddit to a <em>target</em> subreddit—to understand how negativity circulates across categories.

At this stage, we step beyond distances and look directly at how categories interact through negative links.



#### Negative interactions between categories

Before relating negativity to distances, we first inspect how negativity flows between categories at a global scale.

<div style="text-align:center; margin-top:20px;">
  <img src="assets/img/cluter/negativity_heatmap_categories.png" width="70%" alt="Negative links between categories">
  <div style="font-size:0.85rem;"><em>Number of negative hyperlinks from each source to each target category.</em></div>
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



<div style="text-align:center; margin-top:20px;">
  <img src="assets/img/cluster/negativity_distribution_emitted_received.png" width="70%" alt="Negativity emitted vs received">
  <div style="font-size:0.85rem;"><em>Distribution of negative links emitted and received per category.</em></div>
</div>

The distribution plot confirms this:

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
Positive links → smaller cosine distances</b> (except for stylometric where the causal link could not be proved)
</div>

This was supported by a t-test and a causal analysis.

We now extend this to incorporate categories and hyperlink types.



#### Within-cluster vs inter-cluster hyperlinks

To understand how category structure interacts with distances and sentiment, we separate two cases:

<ul>
  <li><b>Within-cluster links:</b> source and target subreddits belong to the same category.</li>
  <li><b>Inter-cluster links:</b> source and target subreddits belong to different categories.</li>
</ul>

We then examine how the **mean cosine distance (authorship distance)** varies across:

- link sentiment (negative or positive),
- and hyperlink type (within vs inter cluster).



<div style="text-align:center;">
  <img src="assets/img/cluster/authorship_distance_within_inter_by_sentiment.png" width="70%" alt="Authorship cosine distance by link type and sentiment">
  <div style="font-size:0.85rem;"><em>Mean authorship cosine distance by hyperlink type and link sentiment (95% CIs).</em></div>
</div>



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

<div style="text-align:center;">
  <img src="assets/img/cluster/authorship_distance_by_category_within_inter.png" width="70%" alt="Cosine distance by category and hyperlink type">
  <div style="font-size:0.85rem;"><em>Top: within-cluster links. Bottom: inter-cluster links. (95% CI)</em></div>
</div>

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



<div style="text-align:center;">
  <img src="assets/img/cluster/psychological_and_stylometric_distance_plots.png" width="75%" alt="Stylometric and psychological distance by link type and sentiment">
  <div style="font-size:0.85rem;"><em>Stylometric and psychological distances by hyperlink type and sentiment.</em></div>
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
<b>communities that are closer in content tend to interact more positively, while distant communities interact more negatively—especially across category boundaries.</b>
</div>


# <span style="color: #ff201e">Quick.</span> The fastest and easiest way to&nbsp;create a&nbsp;GitHub Pages website for your project.
#### The Quick theme magically transforms your `README.md` into a GitHub Pages site, applying clean and visually appealing styles.

<p class="ignore">Just see it yourself&thinsp;—&thinsp;<a href="https://devich.github.io/quick/">this page</a> is the same <code>README.md</code> file you’re reading, but with the Quick theme applied:</p>

<a class="ignore" href="https://devich.github.io/quick/"><img src="assets/img/preview.png" alt="Quick preview"></a>

## Quick start

1. Make sure a `README.md` file exists in the root directory of your repo, and GitHub Pages is enabled in your repository settings.

2. Create a file named `_config.yml` in the root directory of your repository. The file should contain the following content:
```yaml
remote_theme: devich/quick@0.0.1
```

3. That’s it! There is no step 3. You now have a GitHub Pages website that’s based on your `README.md` file. The changes will take effect some time after you commit and push your updates to the repository. Enjoy your new website!


## Looking for a simple landing page for your project? 

No problem! You’re not restricted to using `readme.md` as the index page of your site. Simply create a file named `index.md`, and this theme will use it as the home page. Feel free to create as many pages as you want and link them within your site.

For instance, if you need a home page and an ‘About’ page, create files named `index.md` and `about.md`. Inside the `index.md` file, you can link to your ‘About’ page like this:

```md
[About this project](about)
```


## Fine tuning
### Additional settings in _config.yml

You can set additional parameters for the site in the `_config.yml` file.

The following options are available:

- `lang:` sets the language of the site. E.g. `en-US`, `uk`, `pl`, `fr-CA` and so on. The default value is `en-US`.
- `bg_color:` sets the background color of your website. Can be `dark`, `light` or `auto`. The default value is `auto`.
- `theme_color:` sets the main accent color for buttons, links, etc. It can be <nobr><code class="highlighter-rouge" style="color:#c52f21">red</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#d92662">pink</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#c0208a">fuchsia</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#9136a3">purple</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#7540be">violet</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#524ed1">indigo</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#2060de">blue</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#0172ac">azure</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#047878">cyan</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#007a50">jade</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#398712">green</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#a5d601">lime</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#f2df0d">yellow</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#ffbf00">amber</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#ff9500">pumpkin</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#d24317">orange</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#ccc6b4">sand</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#ababab">grey</code>,</nobr> <nobr><code class="highlighter-rouge" style="color:#646b79">zinc</code> or <nobr><code class="highlighter-rouge" style="color:#525f7a">slate</code>.</nobr> The default value is <nobr><code class="highlighter-rouge" style="color:#0172ac">azure</code>.
- `title:` sets the title of the site. If not set, your repository name will be used.
- `description`: sets the meta description tag, which typically contains a concise, relevant summary of the page’s content.
- `keywords`: sets keywords for the page, separated with commas.
- `gtag`: sets your Google Analytics tag if needed (e.g. G-A1BCDEFGHI).

Alternatively, you can copy the contents of the `_config.yml` file from the [theme repository](https://github.com/devich/quick/blob/main/_config.yml) into your own `_config.yml` file. This will give you access to all available options at once.



### Ignoring

If there’s a block in the `README.md` file that you don’t want to display on the GitHub Pages site, you can format this block as HTML and assign the `class="ignore"` attribute to it.

<p class="ignore">
    This paragraph <a href="https://devich.github.io/quick/">will not be displayed</a>
    on the site because it has an <code>"ignore"</code> class.
</p>

```html
<p class="ignore">
    This paragraph <a href="https://devich.github.io/quick/">will not be
    displayed</a> on the site because it has an <code>"ignore"</code> class.
</p>
```


### More customization

If you need to use your own CSS styles, create a file `assets/css/custom.css` in your repository and add your styles to it.

For a custom favicon, just place your file in `PNG` format at `assets/img/favicon.png`.

For full control, clone this repository and modify the template as you need.
