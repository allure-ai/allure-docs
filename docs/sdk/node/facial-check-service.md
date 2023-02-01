# Facial Check Service
The Facial Check Service can be used to initiate a job in which a facial photo is assessed to get the user's skin condition.

## Begin asynchronous Facial Check job
The job will run asynchronously, and an HTTP webhook will be called upon success or failure.

```ts
import FacialCheckService, { FacialCheckComponent } from '@allure-ai/sdk/services/FacialCheckService';
import apiConfig from './apiConfig';

const service = new FacialCheckService(apiConfig);
service.beginInference({
    callbackUrl: 'https://your-callback-url/callback',
    photoUrl: 'https://url-to-your-selfie/photo.jpg',
    withVisualization: true,
    components: [
        FacialCheckComponent.ACNE,
        FacialCheckComponent.WRINKLE
    ]
})
```

Details on the content of the webhook body can be seen on the [API Reference](https://api-business-docs.allure.id/#tag/Facial-Check-API/operation/scoreFacialCheck).