# Building Responsive Navigation with Liquid Conditionals
As a front-end developer at [Hybrid Web Agency](https://hybridwebagency.com/) focused on crafting optimized Storefront themes, there is no interface more important than navigation. Whether on desktop, mobile or tablet, the navbar sets the tone for usability and brand perception from the very first interaction. However, as product lines expand and page sections evolve, static text links can no longer keep pace.

This is why I'm always exploring dynamic approaches using Liquid templating. By querying existing content directly rather than relying on duplicative reference data, I can build navbar components that respond to change automatically. Editors need only update a single source, safe in the knowledge updates will roll out consistently every time.

In this article, we'll delve into one such technique for generating fully responsive navigation menus. Using tools native to Shopify's templating language like conditionals, looping and output filtering, we can transform rigid text into a flexible collapsing design. Readers will walk away with the skills to future-proof their entire site navigation against endless content shifts down the line.

From properly structuring HTML elements to pulling dynamic section data, we'll cover every step for both desktop and mobile optimizations. Developers will learn how to conditionally style active states, automate accessibility attributes and more. By applying these templating techniques throughout your theme, endless manual edits can become a thing of the past.


## Setting the Stage for Dynamic Navigation

Our goal is to generate navigation menus that automatically adjust to changes - like adding, removing or reordering pages. To do so, we must first lay the groundwork.

Within a new template called `navbar.liquid`, we'll construct a simple staging area:

```liquid
<nav id="navbar">
  <ul>
  </ul>
</nav>
```

This sets up an outer `<nav>` container and nested unordered list `<ul>` - the region where links will render. 

Although blank for now, these fundamental hooks allow us to strategically position generated content. It serves as our navigation "building site", waiting for dynamic components.

But what dynamic pieces? Likely top sections like "Home" and "About Us". Rather than hardcoding these constants, Shopify exposes live section data.

To tap into this back-end resource and fuel our building project, we include:

```liquid
{% raw %} 
{% include 'sections' %}
{% endraw %}
```

Now our stage pulls in vital building blocks - sections ready for assembly into intuitive navigation.

In the next step, we'll construct a loop carrying these definitional supplies directly onto our staging site. Links will take shape organically derived from real content.

For now, we've established the first necessary groundwork for a fluid, future-proofed navigation system. The building begins!


## Populating the Navigation from Dynamic Data

Now that we've established the underlying framework, it's time to fill our empty navbar skeleton with living, breathing content. 

We'll tap into the sections data pulled from Shopify to dynamically generate each menu item. Within the `navbar.liquid` file, add this code below the placeholder unordered list:

```liquid 
{% for section in sections %}

  <li>
    <a href="{{ section.url }}">
      {{ section.title }}
    </a>
  </li>

{% endfor %}
```

This `for` loop iterates through the collection of global `section` objects. On every pass, it inserts a new `<li>` item containing an anchor link. 

The `<a>` tag's `href` attribute draws its value from the section's unique URL path. Meanwhile, the inner text displays the familiar title like "Home" or "About".

By the end, we've automatically constructed a full menu matching the sections in the admin - no more copying and pasting links! Any additions, removals or order changes below are naturally reflected above.

We've generated a truly dynamic element that self-synchronizes with content variations over time. Let's preview how it manifests in the browser.





## Equipping the Menu with Live Links

It's now time to outfit our navigation with fully-functional links tied to dynamic backend data. 

Within the loop, include this code to wire everything up:

```liquid
<li>
  <a href="{{ section.url }}">
    {{ section.title }}
  </a>  
</li>
```

On each cycle, this assembles an individual menu item container. The anchor tag is strapped in with two key properties:

- `section.url` provides the live address for top-level routing
- `section.title` labels the destination understandably 

Proper closing tags cement the setup.

With a single pass, our board is now stocked with fully-prepped links that fluidly mirror backend changes. Additions or edits instantly propagate.

Let's preview how ably this equips the frontend to interact with the administer content sources in real-time. The toolkit is loaded - refresh to deploy!



## Conditionally Styling Active Links

We can apply conditional formatting to stand out the relevant navigation item. 

Wrap the link markup in an `if` statement to isolate the matching section:

```liquid
{% if section.id == page.section.id %}
```

This checks if the looped section's ID is equal to the ID of the currently active section stored in `page`.

Then include a class to modify the highlighting:

```liquid
<li>
  <a href="{{ section.url }}" class="selected">
    {{ section.title }}
  </a>  
</li>
```

Close the conditional block:

```liquid 
{% endif %}
```

Now the link associated with the current page will glow with the "selected" designation on each page interaction.

This accentuates the pertinent pathway while maintaining context of potential next steps. Refresh to see the conditional classification in the wild!


## Ensuring Proper Markup Structure for Accessible Navigation

For our dynamically generated site navigation to display correctly and be accessible to all, it is important to fully close all parent and child HTML elements.

After each iteration of our navigation item loop, we must close the surrounding unordered list:

```liquid
</ul>  
```

We also should terminate each list item at the end of its cycle:

```liquid
  </li>
```  

Then, when rendering the full navigation, the nested lists will be valid HTML semantics:

```liquid
<nav>
  <ul>

   {% for section in sections %}

     <li>

     </li>

   {% endfor %}

  </ul>
</nav>
```

By intentionally closing all opened tags, we establish a clear parent-child relationship between the navigation items and their parent list.

This ensures conformance with accessibility standards like WCAG and allows assistive technologies to properly integrate and announce the navigation to all users.

Let's check our work by previewing - the navigation structure should now fully support users of all kinds. Proper markup is key for an inclusive experience!


## Integrating the Navigation Across Templates

To provide a consistent navigation experience on every page, we'll add the navbar code to the site's shared layout template.

### Inserting the Navigation Markup

```liquid
{{ 'navbar' | liquid }}
```

This Liquid tag will output the HTML we defined for the navbar snippet. We'll place it in the header region of our main layout template.

### Previewing the Updated Navigation

Now when any page using this template is requested, the dynamically generated nav links will automatically display at the top.

Let's refresh a page now to validate the navigation is rendering site-wide as intended. By integrating it centrally in the layout, it will seamlessly guide users throughout the entire site in a unified way.

Our semantic markup and template logic work together to deliver an accessible and consistent user experience across all interfaces. The navigation is fully realized as an essential structural element.


## Conclusion
In conclusion, implementing a dynamic navigation menu powered by Liquid provides many organizational and user experience benefits. Editors save time by not having to manually update pages, and customers benefit from intuitive navigation that automatically adapts to site changes. While this example covers common use cases, additional customizations could provide even more advanced functionality.

For assistance taking your Shopify site to the next level through customized solutions, theme development, or other expert services, contact the development team at Hybrid Web Agency. We offer a full suite of [Shopify Store Development Services in Fort Worth](https://hybridwebagency.com/fort-worth-tx/shopify-store-design-services/), including design, implementation, integration, and ongoing support. Our skilled Fort Worth developers have extensive experience crafting elegant storefronts that maximize conversions. Whether optimizing an existing site or building a new concept from scratch, we have the talent and Shopify know-how to help your business thrive online.


## References 
Shopify Themes Docs
https://shopify.dev/themes

The official documentation for building Shopify themes, including information on Liquid and theme development best practices.

Shopify Liquid Docs
https://shopify.dev/docs/themes/liquid/reference

In-depth reference guide for all Liquid filters, tags, and conditionals like those used in the blog post.

Shopify Sections documentation
https://shopify.dev/docs/admin-api/rest/reference/sections

Details on accessing section data via the Sections API used to power the dynamic navigation.

Adding Dynamic Content to Shopify Themes with Liquid
https://www.shopify.com/partners/blog/adding-dynamic-content-to-shopify-themes-with-liquid
