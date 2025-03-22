
![CTA Screenshot](assets/cta.jpg)
---

## My Goals

- ✅ Easy maintenance
- ✅ Easy to jump between projects
- ✅ Familiarity and consistency
- ✅ Easy copy/paste
- ✅ No “Where is this element coming from?”

---

## Creating and Theming a Paragraph

Time breakdown for a typical new Paragraph:

- 🧱 Create Paragraph type: **~1h**
- 🧪 Copy/paste automatic tests: **~0.5h**
- 🎨 Theming: **~4h**

*Theming is the time-consuming part*

---

![Paragraph CTA Screenshot](assets/paragraph_cta.jpg)

---

<pre><code data-trim class="language-php" data-line-numbers>
protected function buildElementCta(string $title, array $body, Link $link): array {
    $elements = [];

    // Title.
    $element = $title;
    $element = $this->wrapTextResponsiveFontSize($element, '3xl');
    $element = $this->wrapTextCenter($element);
    $elements[] = $this->wrapTextFontWeight($element, 'bold');

    // Text.
    $elements[] = $this->wrapProseText($body);

    // Button.
    $elements[] = $this->buildButton($link->getText(), $link->getUrl(), 'primary', NULL, $link->getUrl()->isExternal());

    $elements = $this->wrapContainerVerticalSpacingBig($elements, 'center');

    $elements = $this->buildInnerElementLayout($elements, 'light-gray');
    return $this->wrapContainerNarrow($elements);
}
</code></pre>

---

```
https://drupal-starter.ddev.site:4443/style-guide
```

![Style guide](assets/style-guide.jpg)
---

## Reasoning with Twig Files

- 🧠 Lower the effort of **mental modeling**
- 📄 What you see in the Twig is what you get
- 🔄 Predictable structure

---

```bash
server-theme-staff-card.html.twig
```

![](assets/long-twig.jpg)

---

<pre><code data-trim class="language-twig" data-line-numbers>
# server-theme-text-decoration--italic.html

<div class="italic">
  {{ element }}
</div>
</code></pre>

---

<pre><code data-trim class="language-twig" data-line-numbers>
# server-theme-text-decoration--center.html.twig

<div class="text-center">
  {{ element }}
</div>

</code></pre>

---

<pre><code data-trim class="language-twig" data-line-numbers>
# server-theme-text-decoration--font-weight.html.twig

{% if font_weight == 'normal' %}
  {% set weight_class = 'font-normal' %}
{% elseif font_weight == 'medium' %}
  {% set weight_class = 'font-medium' %}
{% elseif font_weight == 'bold' %}
  {% set weight_class = 'font-bold' %}
{% endif %}

<div class="{{ weight_class }}">
  {{ element }}
</div>


</code></pre>

---

<pre><code data-trim class="language-twig" data-line-numbers>
# server-theme-text-decoration--responsive-font-size.html.twig

{% if size == 'xs' %}
  {% set size_classes = 'text-xs' %}
{% elseif size == 'sm' %}
  {% set size_classes = 'text-xs md:text-sm' %}
{% elseif size == 'base' %}
  {% set size_classes = 'text-sm md:text-base' %}
{% elseif size == 'lg' %}
  {% set size_classes = 'md:text-lg' %}
{% elseif size == 'xl' %}
  {% set size_classes = 'text-lg md:text-xl' %}
{% elseif size == '2xl' %}
  {% set size_classes = 'text-xl md:text-2xl' %}
{% elseif size == '3xl' %}
  {% set size_classes = 'text-xl md:text-2xl lg:text-3xl' %}
{% endif %}

<div class="{{ size_classes }}">
  {{ element }}
</div>


</code></pre>

---

<pre><code data-trim class="language-twig" data-line-numbers>
# server-theme-container-vertical-spacing.html.twig

{% macro getClass(align) %}
  {% set classes = [
    'flex flex-col gap-3 md:gap-5',
    align == 'start' ? 'items-start',
    align == 'center' ? 'items-center',
    align == 'end' ? 'items-end',
  ] | join(' ') | trim %}
  {{ classes }}
{% endmacro %}
<div class="{{ _self.getClass(align) }}">
  {{ items }}
</div>

</code></pre>

---

<pre><code data-trim class="language-php" data-line-numbers>
protected function buildElementCta(string $title, array $body, Link $link): array {
    $elements = [];

    // Title.
    $element = $title;
    $element = $this->wrapTextResponsiveFontSize($element, '3xl');
    $element = $this->wrapTextCenter($element);
    $elements[] = $this->wrapTextFontWeight($element, 'bold');

    // Text.
    $elements[] = $this->wrapProseText($body);

    // Button.
    $elements[] = $this->buildButton($link->getText(), $link->getUrl(), 'primary', NULL, $link->getUrl()->isExternal());

    $elements = $this->wrapContainerVerticalSpacingBig($elements, 'center');

    $elements = $this->buildInnerElementLayout($elements, 'light-gray');
    return $this->wrapContainerNarrow($elements);
}
</code></pre>

---

```
https://drupal-starter.ddev.site:4443/style-guide#element-quote
```

![](assets/quote.jpg)

---

## Two Types of Twig Files

- 🎨 **Styling Twig**:
  Applies **visual styles**
  _e.g. spacing, font size, color, alignment, flex_

- 🧱 **Layout Twig** *(rare)*:
  Defines **layout** and **position**
  _e.g. two columns_

