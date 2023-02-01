# Product Suitability Service
The Product Suitability Service can be used to initiate a job to determine the how suitable a product is to the user.

## Assess skincare product suitability
The job will run asynchronously, and an HTTP webhook will be called upon success or failure.

```ts
import ProductSuitabilityService, { GenderEnum, SkinOilinessEnum, SkinSensitivityEnum, SkinGoalsEnum } from '@allure-ai/sdk/services/ProductSuitabilityService';
import apiConfig from './apiConfig';

const service = new ProductSuitabilityService(apiConfig);
service.calculateSkincareProductSuitability({
    callbackUrl: 'https://your-callback-url/callback',
    articleNo: ['PSA0000000001', 'PSA0000000012'],   // Define the article no of skincare products to assess
    user: {
        gender: GenderEnum.MALE,
        age: 23,
        halalPreference: true,
        crueltyFreePreference: false,
        parabenFreePreference: true,
        pregnantPreference: false,
        oilinessVerdict: SkinOilinessEnum.OILY,
        sensitivityVerdict: SkinSensitivityEnum.SENSITIVE,
        skinProblemsToSolve: [
            SkinGoalsEnum.FIGHTING_ACNE,
            SkinGoalsEnum.REMOVING_ACNE_MARKS
        ],
        budgetMin: 20000,
        budgetMax: 50000,
        acneScore: 98,
        wrinkleScore: 75,
        darkspotScore: 95,
        darkCircleScore: 48
    }
})
```

Details on the content of the webhook body can be seen on the [API Reference](https://api-business-docs.allure.id/#tag/Product-Suitability-API/operation/calculateSkincareProductSuitabilityScore).