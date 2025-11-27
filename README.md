# <span style="color:#ff201e">Birds of a Feather… Fight Together?</span>
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

**cosine_sim(A, B) = (A · B) / (‖A‖ × ‖B‖)**

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

**(x − μ) / σ**

This ensures that no single feature dominates simply because it has larger numerical values.

Once each subreddit has its stylometric signature, we again compare communities via **cosine similarity**, not Euclidean distance, because we want to measure **proportions**, not magnitudes.

The resulting distance is:

**Stylometric Distance = 1 − cosine_sim(style_A, style_B)**

---

## 3. Psychological Signatures: What Communities Express

Language also reveals psychology.  
Each hyperlink post in the dataset includes **64 LIWC features** and **VADER sentiment scores**, capturing emotional tone, cognitive style, and more.

For each subreddit, we aggregate the normalized LIWC+VADER features of all its outgoing posts to define a **psychological signature**, the average emotional and cognitive expression shown by its authors when interacting with other communities.

As before, similarity is computed as a distance, using cosine similarity:

**Psychological Distance = 1 − cosine_sim(psych_A, psych_B)**

This gives us a final observation angle:  
**how similar communities are in what they feel and the emotions they display**.

---






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
