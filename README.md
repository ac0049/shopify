# shopify search matched sku first
```
// products - searched products json

  const matchedProducts = products.filter((product) => product.sku.toLowerCase().includes(term.toLowerCase()));
  const unmatchedProucts = products.filter((product) => !product.sku.toLowerCase().includes(term.toLowerCase()));
  
  const resultProducts = matchedProducts.concat(unmatchedProucts);
```
