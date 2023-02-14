# Embedding the Widget to a Web Page

The widget can be embedded as a part of your own web page, similar to an embedded YouTube video. You can embed the widget using the following embed script:

```html
<script type="text/javascript" src="https://business.allure.id/scripts/embed/mainmenu.js"></script>
<div id="allure-embed-mainmenu"></div>
<script>
    var widgetOptions = {
      placementId: '[widget placement ID]'
    }
    new AllureMainMenuWidget(widgetOptions).render(document.getElementById('allure-embed-mainmenu'));
</script>
```

### Widget Options
There are several options you can set to configure the widget behavior.

| Option Name           | Type                 | Description                                                                                          |
|-----------------------|----------------------|------------------------------------------------------------------------------------------------------|
| `key` (required)      | `string`             | Placement ID of the widget, obtained from Business Suite Dashboard.                                  |
| `width`               | `number | string`   | Width of the widget, default is "100%"                                                               |
| `height`              | `number`             | Height of the widget, if unset the height is automatically adjusted according to the widget content. |
