---
layout: page
title: All Omeka Classic Plugins
---

{% assign total_addons = 0 %}
{% assign total_matchings = 0 %}
{% assign total_upgraders = 0 %}
{% assign total_upgradables = 0 %}
{% for addon in site.data.omeka_plugins %}
    {% unless addon['Name'] == nil %}
        {% assign total_addons = total_addons | plus: 1 %}
        {% unless addon['Module'] == nil %}
            {% assign total_matchings = total_matchings | plus: 1 %}
        {% endunless %}
        {% if addon['Upgradable'] == 'Yes' %}
            {% assign total_upgradables = total_upgradables | plus: 1 %}
        {% endif %}
        {% if addon['Upgradable'] == 'Yes (auto)' %}
            {% assign total_upgraders = total_upgraders | plus: 1 %}
        {% endif %}
    {% endunless %}
{% endfor %}


<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
<script src="//code.jquery.com/jquery-3.1.1.min.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/list.js/1.5.0/list.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>

<style media="screen" type="text/css">
    .sort { cursor: pointer; }
    .page-content .wrapper { max-width: inherit; }
    .page-content .wrapper .post-header,
    .page-content .wrapper .post-content p { max-width: calc(800px - 30px * 2); margin-left: auto; margin-right: auto; padding-left: 30px: padding-right: 30px; }
    .page-content .wrapper .post-content .container-fluid { max-width: inherit; }
</style>


All plugins can be downloaded freely on <https://github.com> or <https://gitlab.com>. Some of them are old, broken or unsupported. Usually, they work at least on one site. But most of them are up-to-date for [Omeka Classic] and useful. Only a part of them are listed in <https://omeka.org/add-ons/plugins>.

{% if total_addons > 0 %}
Already {{ total_matchings }} / {{ total_addons }} (<strong>{{ total_matchings | times: 100 | divided_by: total_addons | round }}%</strong>) plugins – the most used ones – have an equivalent module for [Omeka S], and {{ total_upgraders }} automatic upgraders are available. See the page of [matching extensions]({{ site.url | append: '/UpgradeToOmekaS' }}).
{% endif; %}

Feel free to add missing plugins, or to create an upgrader processor for the plugin [Upgrade To Omeka S], or contact me.

<div class="container-fluid">
<div id="entry-list">
    <div class="row" style="margin-bottom:10px;">
        <input type="text" class="search form-control" placeholder="Filter" />
    </div>
    <p><em>
    Type some letters to filter the list. Click on row headers to sort. Get the <a href="https://github.com/Daniel-KM/UpgradeToOmekaS/blob/master/docs/_data/omeka_plugins.csv">csv source file</a>.
    </em></p>
    <div class="row">
        <table class="table table-striped">
            <thead>
                <tr>
                    <th><span class="sort" data-sort="addon-link">Plugin</span></th>
                    <th><span class="sort" data-sort="addon-author">Author</span></th>
                    <th><span class="sort" data-sort="addon-version">Last</span></th>
                    <th><span class="sort" data-sort="addon-omeka-org">Omeka.org</span></th>
                    <th><span class="sort" data-sort="addon-upgradable">Upgradable</span></th>
                    <th><span class="sort" data-sort="addon-target">Target</span></th>
                    <th><span class="sort" data-sort="addon-license">License</span></th>
                    <th><span class="sort" data-sort="addon-tags">Tags</span></th>
                    <!--
                    <th><span class="sort" data-sort="addon-required">Required plugins</span></th>
                    <th><span class="sort" data-sort="addon-optional">Optional plugins</span></th>
                    -->
                    <th><span class="sort" data-sort="addon-description">Description</span></th>
                </tr>
            </thead>
            <tbody class="list">
            {% for addon in site.data.omeka_plugins %}
                {% if addon['Name'] %}
                <tr>
                    <td>
                    {% unless addon['Name'] == nil %}
                        <a href="{{ addon['Url'] }}" class="link addon-link">{{ addon['Name'] }}</a>
                    {% endunless %}
                    </td>
                    <td>
                    {% unless addon['Name'] == nil %}
                        {% unless addon['Author'] == nil %}
                            {% assign account_name = addon['Url'] | remove: 'https://github.com/' | remove: 'https://gitlab.com/' | split: '/' | first %}
                            {% assign account_url = addon['Url'] | split: account_name | first | append: account_name %}
                            <a href="{{ account_url }}" class="link addon-author">{{ addon['Author'] }}</a>
                        {% endunless %}
                    {% endunless %}
                    </td>
                    <td class="addon-version">{{ addon['Last'] }}</td>
                    <td class="addon-omeka-org">{{ addon['Omeka.org'] }}</td>
                    <td class="addon-upgradable">{{ addon['Upgradable'] }}</td>
                    <td class="addon-target">
                    {% if addon['Name'] == nil %}
                        {{ addon['Omeka Target'] }}
                    {% else %}
                        {{ addon['Omeka Min'] }}
                    {% endif %}
                    </td>
                    <td class="addon-license">{{ addon['License'] }}</td>
                    <td class="addon-tags">{{ addon['Tags'] | replace: ',', ',<br />' }}</td>
                    <!--
                    <td class="addon-required">{{ addon['Required Plugins'] | replace: ',', ',<br />' }}</td>
                    <td class="addon-required">{{ addon['Optional Plugins'] | replace: ',', ',<br />' }}</td>
                    -->
                    <td class="addon-description">{{ addon['Description'] }}</td>
                </tr>
                {% endif %}
            {% endfor %}
            </tbody>
        </table>
    </div>
</div>
</div>

<script type="text/javascript">
    var options = {
        valueNames: ['addon-link', 'addon-author', 'addon-version', 'addon-omeka-org', 'addon-upgradable', 'addon-target', 'addon-license', 'addon-tags', 'addon-required', 'addon-optional', 'addon-description'],
        page: 500
    };
    var entryList = new List('entry-list', options);
</script>


[Upgrade To Omeka S]: https://github.com/Daniel-KM/UpgradeToOmekaS
[Omeka Classic]: https://omeka.org
[Omeka S]: https://omeka.org/s