---
title: firehose
layout: default
---

# firehose
Every post on this site in one stream, newest first. Pages are listed at build time; shower thoughts come from [rss.json](/rss.json).

<style>
  .firehose { list-style: none; padding: 0; }
  .firehose .h-entry { margin: 0 0 1.5em; }
  .firehose .meta { opacity: 0.6; font-size: 0.85em; margin: 0; }
  .firehose .e-content { margin: 0.25em 0 0; white-space: pre-line; }
</style>

<ol class="firehose h-feed" id="firehose-feed">
{%- assign dated = site.pages | where_exp: "p", "p.date" -%}
{%- for p in dated -%}
  <li class="h-entry">
    <p class="meta"><time class="dt-published" datetime="{{ p.date | date_to_xmlschema }}">{{ p.date | date: "%a, %-d %b %Y" }}</time> · page</p>
    <a class="u-url p-name" href="{{ site.baseurl }}{{ p.url }}">{{ p.title }}</a>
    <p class="e-content p-summary">{{ p.content | markdownify | strip_html | normalize_whitespace | truncatewords: 40 }}</p>
  </li>
{%- endfor -%}
</ol>

<script>
(async () => {
  const list = document.getElementById('firehose-feed');
  const fmt = d => `${d.toLocaleDateString('en-US', { weekday: 'short' })}, ${d.getDate()} ${d.toLocaleDateString('en-US', { month: 'short' })} ${d.getFullYear()}`;
  function linkify(el, text) {
    text.split(/(https?:\/\/\S+)/).forEach((part, i) => {
      if (i % 2) { const a = document.createElement('a'); a.href = part; a.textContent = part; el.appendChild(a); }
      else el.appendChild(document.createTextNode(part));
    });
  }
  try {
    const feed = await (await fetch('{{ site.baseurl }}/rss.json')).json();
    for (const item of feed.items) {
      const li = document.createElement('li');
      li.className = 'h-entry';
      const meta = document.createElement('p');
      meta.className = 'meta';
      const time = document.createElement('time');
      time.className = 'dt-published';
      time.dateTime = item.date_published;
      time.textContent = fmt(new Date(item.date_published));
      meta.append(time, ' · note');
      const a = document.createElement('a');
      a.className = 'u-url p-name';
      a.href = item.url;
      a.textContent = item.title;
      const body = document.createElement('p');
      body.className = 'e-content';
      linkify(body, item.content_text || '');
      li.append(meta, a, body);
      list.appendChild(li);
    }
  } catch (e) {
    console.error('firehose: rss.json failed', e);
  }
  [...list.children]
    .sort((x, y) => new Date(y.querySelector('time').dateTime) - new Date(x.querySelector('time').dateTime))
    .forEach(li => list.appendChild(li));
})();
</script>
