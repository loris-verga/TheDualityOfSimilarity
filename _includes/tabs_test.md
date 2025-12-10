
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
