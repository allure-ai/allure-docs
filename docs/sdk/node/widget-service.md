# Widget Service
The Widget Service is used to retrieve the details of a Widget Placement. This includes a list of entitled products, theme, allowed origins, etc.

## Importing the library
```ts
import WidgetService from '@allure-ai/sdk/services/WidgetService';
import apiConfig from './apiConfig';

const widgetService = new WidgetService(apiConfig);
```

## Retrieving widget placements

### Retrieving Skincare Analyzer widget placement
```ts
const placement = await widgetService.retrieveSkincareAnalyzerWidgetPlacement(placementId);
```

### Retrieving Foundation Shade Finder widget placement
```ts
const placement = await widgetService.retrieveFoundationFinderWidgetPlacement(placementId);
```

### Retrieving AR Makeup Tryon widget placement
```ts
const placement = await widgetService.retrieveARMakeupTryonWidgetPlacement(placementId);
```

### Retrieving Main Menu widget placement
```ts
const placement = await widgetService.retrieveMainMenuWidgetPlacement(placementId);
```

## Retrieving product overrides
The Business Suite provides a way for tenants to customize some product data, which is called the Product Override Set. Given the tenant ID, product override set ID, and the product's article no, you can use the library to fetch the overriden data.

### Skincare product override
```ts
const articleNo = "PSA000001010";
const tenantId = "tenant";
const overrideId = "20fb655a-ca00-4dea-922e-80a2c7497674";
const productOverrideData = await widgetService.retrieveSkincareProductOverride(tenantId, overrideId, articleNo)
```

### Makeup product override
```ts
const articleNo = "PMA000001010";
const tenantId = "tenant";
const overrideId = "20fb655a-ca00-4dea-922e-80a2c7497674";
const productOverrideData = await widgetService.retrieveMakeupProductOverride(tenantId, overrideId, articleNo)
```