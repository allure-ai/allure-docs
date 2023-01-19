# Embedding the Widget to a Web Page

The widget can be embedded as a part of your own web page, similar to an embedded YouTube video. You can embed the widget using the following embed script:

```html
<script type="text/javascript" src="https://embed.allure.id/scripts/embed/skinanalyzer.js"></script>
<div id="allure-embed"></div>
<script>
    var widgetOptions = {
      key: '[widget placement ID]'
    }
    new AllureSkincareAnalyzerWidget(widgetOptions).render(document.getElementById('allure-embed'));
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
| `onAnalysisComplete`  | `(analysis) => void` | A callback invoked when the analysis flow is complete.                                               |

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

### Analysis complete callback
This callback will be invoked when the analysis flow is complete. The callback shall have the following signature:

```js
const onAnalysisComplete = (analysis) => {
    console.log(analysis)
}
```

#### Analysis Payload

| Key                  | Type                      | Description                             |
|----------------------|---------------------------|-----------------------------------------|
| `analysisKey`        | `string`                  | Analysis unique identifier.             |
| `skinSurvey`         | `SkinSurvey`              | Skin survey data.                       |
| `facialCheck`        | `FacialCheck`             | Facial check scores.                    |
| `productSuitability` | `Array<[string, number]>` | An array of Article No and Score pairs. |

#### `SkinSurvey` Payload

| Key                      | Type            | Description                                                                                                                                                                                           |
|--------------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `age`                    | `number`        | User age.                                                                                                                                                                                             |
| `gender`                 | `string`        | Gender, enum: `MALE`, `FEMALE`, or `UNKNOWN`                                                                                                                                                          |
| `skinSensitivityVerdict` | `string`        | Skin sensitivity, enum: `SENSITIVE` or `RESISTANT`                                                                                                                                                    |
| `skinOilinessVerdict`    | `string`        | Skin oiliness, enum: `DRY`, `NORMAL`, or `OILY`                                                                                                                                                       |
| `skinGoals`              | `Array<string>` | Skin goals, enum: `BRIGHTENING`, `FIGHTING_ACNE`, `FIGHTING_AGING`, `IMPROVING_SKIN_TEXTURE`, `REMOVING_ACNE_MARKS`, `REMOVING_COMEDO`, `SKIN_FEELS_DRY`, `SKIN_LOOKS_DULL`, or `SUNLIGHT_PROTECTION` |

#### `FacialCheck` Payload

| Key          | Type     | Description                                       |
|--------------|----------|---------------------------------------------------|
| `acne`       | `number` | Acne score, range: 0 (bad) to 100 (great).        |
| `wrinkle`    | `number` | Wrinkle score, range: 0 (bad) to 100 (great).     |
| `darkspot`   | `number` | Darkspot score, range: 0 (bad) to 100 (great).    |
| `darkCircle` | `number` | Dark circle score, range: 0 (bad) to 100 (great). |
| `redness`    | `number` | Redness score, range: 0 (bad) to 100 (great).     |
| `oiliness`   | `number` | Oiliness score, range: 0 (bad) to 100 (great).    |

#### Product Suitability Payload

The `productSuitability` payload contains an array of pairs. The first element of the pair is the Article No, and the second element is the match score. It is sorted descending by score.

#### Example Payload

```js
{
    "analysisKey": "a23f099a-a743-4bf6-8156-c34ebc21eb72",
    "skinSurvey": {
        "age": 23,
        "gender": "MALE",
        "skinSensitivityVerdict": "SENSITIVE",
        "skinOilinessVerdict": "OILY",
        "skinGoals": [
            "FIGHTING_ACNE",
            "REMOVING_ACNE_MARKS",
            "SUNLIGHT_PROTECTION"
        ],
        "specialPreferences": ["HALAL"],
        "minBudget": 150000,
        "maxBudget": 500000,
        "contact": {
            "name": "John Doe"
        }
    },
    "facialCheck": {
        "acne": 93,
        "wrinkle": 100,
        "darkspot": 57,
        "darkCircle": 71,
        "redness": 98,
        "oiliness": 98
    },
    "productSuitability": [
        ["PSA00000457", 63],
        ["PSA00000458", 62],
        ["PSA00000493", 62],
        ["PSA00000456", 61],
        ["PSA00000463", 58],
        ["PSA00000461", 57],
        ["PSA00000465", 56],
        ["PSA00000479", 40],
        ["PSA00000481", 32],
        ["PSA00000482", 31], 
    ]
}
```