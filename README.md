# shopify search matched sku first
```
// products - searched products json

  const matchedProducts = products.filter((product) => product.sku.toLowerCase().includes(term.toLowerCase()));
  const unmatchedProucts = products.filter((product) => !product.sku.toLowerCase().includes(term.toLowerCase()));
  
  const resultProducts = matchedProducts.concat(unmatchedProucts);
```
# Shopify Color swatch
```
{%- assign swatch_trigger = 'products.general.color_swatch_trigger' | t | downcase -%}
          {%- for option in product.options_with_values -%}
            {%- liquid
              assign option_name = option.name | downcase
              assign is_color = false
              if option_name contains swatch_trigger
                assign is_color = true
              elsif swatch_trigger == 'color' and option_name contains 'colour'
                assign is_color = true
              endif
            -%}
            {%- if is_color -%}
              {%- assign option_index = forloop.index0 -%}
              {%- assign values = '' -%}
              {%- for variant in product.variants -%}
                {%- assign value = variant.options[option_index] %}
                {%- unless values contains value -%}
                  {%- liquid
                    assign values = values | join: ',' | append: ',' | append: value | split: ','
                  -%}

                  {%- if variant.image -%}
                    <div
                      class="grid-product__color-image grid-product__color-image--{{ variant.id }} small--hide">
                    </div>
                  {%- endif -%}
                {%- endunless -%}
              {%- endfor -%}
            {%- endif -%}
          {%- endfor -%}
```
