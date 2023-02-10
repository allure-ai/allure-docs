# Embedding the Widget to a Web Page

The widget can be embedded as a part of your own web page, similar to an embedded YouTube video. You can embed the widget using the following embed script:

```html
<script type="text/javascript" src="https://business.allure.id/scripts/embed/armakeup.js"></script>
<div id="allure-embed-armakeup"></div>
<script>
    var widgetOptions = {
      key: '[widget placement ID]'
    }
    new AllureARMakeupTryonWidget(widgetOptions).render(document.getElementById('allure-embed-armakeup'));
</script>
```

### Widget Options
There are several options you can set to configure the widget behavior.

| Option Name           | Type                 | Description                                                                                          |
|-----------------------|----------------------|------------------------------------------------------------------------------------------------------|
| `key` (required)      | `string`             | Placement ID of the widget, obtained from Business Suite Dashboard.                                  |
| `width`               | `number | string`   | Width of the widget, default is "100%"                                                               |
| `height`              | `number`             | Height of the widget, if unset the height is automatically adjusted according to the widget content. |
| `productCtaLabel`     | `string`             | Override the buy button text, default is "Beli Produk"                                               |
| `onProductCtaClicked` | `(product) => void`  | A callback invoked when a user clicks on the CTA button, overriding the default buy links popover.     |

### CTA clicked callback
This callback will be invoked when the user clicks on the CTA button. The callback shall have the following signature:

```js
const onProductCtaClicked = (product) => {
    console.log(product)
}
```

#### Product Payload

| Key         | Type                  | Description                                             |
|-------------|-----------------------|---------------------------------------------------------|
| `articleNo` | `string`              | Allure Article Number (AAN) for the product.            |
| `skuNo`     | `string | undefined` | Custom SKU number as defined in a Product Override Set. |
| `name`      | `string`              | Product name (without brand name).                      |
| `brandName` | `string`              | Brand name.                                             |
