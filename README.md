# Bookstore
PersonalPersonal
bookstore-theme/
├── assets/
│   ├── custom.css
│   └── custom.js
├── config/
│   └── settings_schema.json
├── layout/
│   └── theme.liquid
├── locales/
│   └── en.default.json
├── sections/
│   ├── featured-collection.liquid
│   ├── hero.liquid
│   └── scrolling-books.liquid
├── snippets/
│   └── product-card.liquid
└── templates/
    └── index.liquid

my-shopify-bookstore-theme/
├── assets/
│   ├── custom.css
│   └── custom.js
├── config/
│   └── settings_schema.json
├── layout/
│   └── theme.liquid
├── sections/
│   ├── scrolling-books.liquid
│   └── featured-collection.liquid
├── snippets/
│   └── product-card.liquid
├── templates/
│   ├── index.liquid
│   ├── product.liquid
│   └── collection.liquid
└── locales/
    └── en.default.{% schema %}
{
  "name": "Scrolling Books",
  "settings": [
    {
      "type": "collection",
      "id": "collection",
      "label": "Select Book Collection"
    },
    {
      "type": "text",
      "id": "title",
      "label": "Section Title",
      "default": "Best Selling Books"
    }
  ],
  "presets": [
    {
      "name": "Scrolling Books",
      "category": "Books"
    }
  ]
}
{% endschema %}

{% assign collection = collections[section.settings.collection] %}

<section style="padding: 16px;">
  <h2 style="font-size: 20px; margin-bottom: 10px;">{{ section.settings.title }}</h2>
  <div style="display: flex; overflow-x: auto; gap: 12px; padding-bottom: 10px;">
    {% for product in collection.products limit: 10 %}
      <div style="flex: 0 0 auto; width: 140px; text-align: center;">
        <a href="{{ product.url }}">
          <img src="{{ product.featured_image | image_url: width: 300 }}" alt="{{ product.title }}" style="width: 100%; height: 100px; object-fit: cover;">
          <p style="font-size: 13px; margin: 6px 0;">{{ product.title }}</p>
        </a>
        <form method="post" action="/cart/add">
          <input type="hidden" name="id" value="{{ product.variants.first.id }}">
          <button type="submit" style="padding: 6px 12px; background: #000; color: #fff; border: none; font-size: 13px; border-radius: 4px; cursor: pointer;">
            Add to Cart
          </button>
        </form>
      </div>
    {% endfor %}
  </div>
</section><!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>{{ page_title }} - {{ shop.name }}</title>
  {{ content_for_header }}
  <link href="{{ 'custom.css' | asset_url }}" rel="stylesheet" type="text/css" />
  <script src="{{ 'custom.js' | asset_url }}" defer></script>
</head>
<body>
  <header>
    <nav>
      <ul>
        <li><a href="{{ routes.root_url }}">Home</a></li>
        {% for link in linklists.main-menu.links %}
          <li><a href="{{ link.url }}">{{ link.title }}</a></li>
        {% endfor %}
      </ul>
      <form action="/search" method="get" role="search">
        <input type="search" name="q" placeholder="Search books..." aria-label="Search" />
        <button type="submit">Search</button>
      </form>
      <a href="/cart">Cart ({{ cart.item_count }})</a>
    </nav>
  </header>

  <main>
    {{ content_for_layout }}
  </main>

  <footer>
    <section>
      <p>Contact: info@yourbookstore.com | Phone: +880 1234 567890</p>
      <p>© {{ 'now' | date: "%Y" }} {{ shop.name }}</p>
    </section>
  </footer>

  {{ content_for_footer }}
</body>
</html>{% schema %}
{
  "name": "Scrolling Books",
  "settings": [
    {
      "type": "collection",
      "id": "collection",
      "label": "Select Book Collection"
    },
    {
      "type": "text",
      "id": "title",
      "label": "Section Title",
      "default": "Best Selling Books"
    }
  ],
  "presets": [
    {
      "name": "Scrolling Books",
      "category": "Books"
    }
  ]
}
{% endschema %}

{% assign collection = collections[section.settings.collection] %}

<section style="padding: 16px;">
  <h2 style="font-size: 20px; margin-bottom: 10px;">{{ section.settings.title }}</h2>
  <div style="display: flex; overflow-x: auto; gap: 12px; padding-bottom: 10px;">
    {% for product in collection.products limit: 10 %}
      <div style="flex: 0 0 auto; width: 140px; text-align: center;">
        <a href="{{ product.url }}">
          <img src="{{ product.featured_image | image_url: width: 300 }}" alt="{{ product.title }}" style="width: 100%; height: 100px; object-fit: cover;">
          <p style="font-size: 13px; margin: 6px 0;">{{ product.title }}</p>
        </a>
        <form method="post" action="/cart/add">
          <input type="hidden" name="id" value="{{ product.variants.first.id }}">
          <button type="submit" style="padding: 6px 12px; background: #000; color: #fff; border: none; font-size: 13px; border-radius: 4px; cursor: pointer;">
            Add to Cart
          </button>
        </form>
      </div>
    {% endfor %}
  </div>
</section>body {
  font-family: Arial, sans-serif;
  margin: 0; padding: 0;
  background: #fafafa;
  color: #222;
}
header nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #333;
  padding: 10px 20px;
}
header nav ul {
  display: flex;
  list-style: none;
  margin: 0; padding: 0;
}
header nav ul li {
  margin-right: 20px;
}
header nav ul li a {
  color: #fff;
  text-decoration: none;
  font-weight: 600;
}
header nav form {
  display: flex;
}
header nav input[type="search"] {
  padding: 5px;
  border: none;
  border-radius: 3px 0 0 3px;
  outline: none;
}
header nav button {
  padding: 5px 10px;
  border: none;
  background: #f60;
  color: #fff;
  border-radius: 0 3px 3px 0;
  cursor: pointer;
  font-weight: 600;
}
footer {
  background: #222;
  color: #ccc;
  text-align: center;
  padding: 20px 0;
  margin-top: 40px;
}
footer section p {
  margin: 5px 0;
}body {
  font-family: Arial, sans-serif;
  margin: 0; padding: 0;
  background: #fafafa;
  color: #222;
}
header nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #333;
  padding: 10px 20px;
}
header nav ul {
  display: flex;
  list-style: none;
  margin: 0; padding: 0;
}
header nav ul li {
  margin-right: 20px;
}
header nav ul li a {
  color: #fff;
  text-decoration: none;
  font-weight: 600;
}
header nav form {
  display: flex;
}
header nav input[type="search"] {
  padding: 5px;
  border: none;
  border-radius: 3px 0 0 3px;
  outline: none;
}
header nav button {
  padding: 5px 10px;
  border: none;
  background: #f60;
  color: #fff;
  border-radius: 0 3px 3px 0;
  cursor: pointer;
  font-weight: 600;
}
footer {
  background: #222;
  color: #ccc;
  text-align: center;
  padding: 20px 0;
  margin-top: 40px;
}
footer section p {
  margin: 5px 0;
}body {
  font-family: Arial, sans-serif;
  margin: 0; padding: 0;
  background: #fafafa;
  color: #222;
}
header nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #333;
  padding: 10px 20px;
}
header nav ul {
  display: flex;
  list-style: none;
  margin: 0; padding: 0;
}
header nav ul li {
  margin-right: 20px;
}
header nav ul li a {
  color: #fff;
  text-decoration: none;
  font-weight: 600;
}
header nav form {
  display: flex;
}
header nav input[type="search"] {
  padding: 5px;
  border: none;
  border-radius: 3px 0 0 3px;
  outline: none;
}
header nav button {
  padding: 5px 10px;
  border: none;
  background: #f60;
  color: #fff;
  border-radius: 0 3px 3px 0;
  cursor: pointer;
  font-weight: 600;
}
footer {
  background: #222;
  color: #ccc;
  text-align: center;
  padding: 20px 0;
  margin-top: 40px;
}
footer section p {
  margin: 5px 0;
}// Add your custom JS here if needed
console.log('Custom JS loaded');{% comment %}
  Homepage template - shows hero banner, collections & scrolling books section
{% endcomment %}

{% section 'hero' %}

{% section 'featured-collection' %}

{% section 'scrolling-books' %}{% schema %}
{
  "name": "Hero Section",
  "settings": [
    {
      "type": "image_picker",
      "id": "hero_image",
      "label": "Hero Image"
    },
    {
      "type": "text",
      "id": "hero_heading",
      "label": "Heading",
      "default": "Welcome to Our Bookstore"
    },
    {
      "type": "text",
      "id": "hero_subheading",
      "label": "Subheading",
      "default": "Find your favorite books here"
    }
  ],
  "presets": [
    {
      "name": "Hero",
      "category": "Homepage"
    }
  ]
}
{% endschema %}

<section style="text-align:center; padding: 40px 20px; background: #eee;">
  {% if section.settings.hero_image %}
    <img src="{{ section.settings.hero_image | image_url: width: 1200 }}" alt="{{ section.settings.hero_heading }}" style="max-width: 100%; height: auto;"/>
  {% endif %}
  <h1 style="font-size: 2rem; margin-top: 20px;">{{ section.settings.hero_heading }}</h1>
  <p style="font-size: 1.2rem; color: #555;">{{ section.settings.hero_subheading }}</p>
</section>{% schema %}
{
  "name": "Featured Collection",
  "settings": [
    {
      "type": "collection",
      "id": "collection",
      "label": "Select Collection"
    },
    {
      "type": "text",
      "id": "title",
      "label": "Section Title",
      "default": "Featured Books"
    }
  ],
  "presets": [
    {
      "name": "Featured Collection",
      "category": "Books"
    }
  ]
}
{% endschema %}

{% assign collection = collections[section.settings.collection] %}

<section style="padding: 20px;">
  <h2 style="font-size: 22px; margin-bottom: 15px;">{{ section.settings.title }}</h2>
  <div style="display: flex; flex-wrap: wrap; gap: 20px;">
    {% for product in collection.products limit: 8 %}
      <div style="width: 180px; text-align: center;">
        <a href="{{ product.url }}">
          <img src="{{ product.featured_image | image_url: width: 250 }}" alt="{{ product.title }}" style="width: 100%; height: 160px; object-fit: cover;">
          <p style="margin: 10px 0 5px; font-weight: 600;">{{ product.title }}</p>
          <p style="color: #f60; font-weight: 700;">{{ product.price | money }}</p>
        </a>
      </div>
    {% endfor %}
  </div>
</section><div class="product-card" style="text-align:center;">
  <a href="{{ product.url }}">
    <img src="{{ product.featured_image | image_url: width: 250 }}" alt="{{ product.title }}" style="width: 100%; height: 160px; object-fit: cover;" />
    <h3>{{ product.title }}</h3>
    <p>{{ product.price | money }}</p>
  </a>
  <form method="post" action="/cart/add" style="margin-top: 5px;">
    <input type="hidden" name="id" value="{{ product.variants.first.id }}" />
    <button type="submit" style="background:#000;color:#fff;padding:8px 16px;border:none;cursor:pointer;">
      Add to Cart
    </button>
  </form>
</div>[
  {
    "name": "Theme settings",
    "settings": [
      {
        "type": "text",
        "id": "store_phone",
        "label": "Store Phone Number",
        "default": "+8801234567890"
      },
      {
        "type": "text",
        "id": "store_email",
        "label": "Store Email",
        "default": "info@yourbookstore.com"
      }
    ]
  }
]{
  "general": {
    "search_placeholder": "Search books...",
    "add_to_cart": "Add to Cart"
  }
}
