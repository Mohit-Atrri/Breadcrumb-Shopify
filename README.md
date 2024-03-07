
{% unless template == 'index' or template == 'cart' or template == 'list-collections' %}

 {% for collection in product.collections %}
   
  {% assign collectionTitle = product.collections[0].title %}
  {% assign collectionUrl = product.collections[0].url %}
   
 {% endfor %} 

<nav class="breadcrumb" role="navigation" aria-label="breadcrumbs">

  <a href="/" title="Home">Home</a>

  {% if template contains 'page' %}

    <span aria-hidden="true">&rsaquo;</span>

    <span>{{ page.title }}</span>

  {% elsif template contains 'product' %}

    {% if collection.url %}

      <span aria-hidden="true">&rsaquo;</span>

      {{ collection.title | link_to: collection.url }}

    {% endif %}

    <span aria-hidden="true">&rsaquo;</span>
  
     {{ collectionTitle | link_to: collectionUrl }}
    
    <span aria-hidden="true">&rsaquo;</span>

    <span>{{ product.title }}</span>

  {% elsif template contains 'collection' and collection.handle %}

    <span aria-hidden="true">&rsaquo;</span>

    {% if current_tags %}

      {% capture url %}/collections/{{ collection.handle }}{% endcapture %}

      {{ collection.title | link_to: url }}

      <span aria-hidden="true">&rsaquo;</span>

      <span>{{ current_tags | join: " + " }}</span>

    {% else %}

      <span>{{ collection.title }}</span>

    {% endif %}

  {% elsif template == 'blog' %}

    <span aria-hidden="true">&rsaquo;</span>

    {% if current_tags %}

      {{ blog.title | link_to: blog.url }}

      <span aria-hidden="true">&rsaquo;</span>

      <span>{{ current_tags | join: " + " }}</span>

    {% else %}

    <span>{{ blog.title }}</span>

    {% endif %}

  {% elsif template == 'article' %}

    <span aria-hidden="true">&rsaquo;</span>

    {{ blog.title | link_to: blog.url }}

    <span aria-hidden="true">&rsaquo;</span>

    <span>{{ article.title }}</span>

  {% else %}

   <span aria-hidden="true">&rsaquo;</span>

   <span>{{ page_title }}</span>

  {% endif %}

</nav>

{% endunless %} 
