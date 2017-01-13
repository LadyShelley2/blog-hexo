---
title: tags
layout: tags
comments: false
---
  <div class="layout-wrap-inner tag-cloud">
    <% if(site.tags.length) { %>
        <%- tagcloud() %>
    <% } %>
  </div>