# Setup
We provide a Node.js client library to access our APIs. Here are the APIs you can access using this library:

1. Beauty Product Database - used to retrieve beauty product details (including name, brand, ingredients, etc.)
2. Facial Check Service - used to initiate facial check request to assess skin condition scores.
3. Product Suitability Service - used to calculate product suitability scores.
4. Widget Service - used to retrieve widget placement details.

## Installation

```bash
npm install @allure-ai/sdk
```

Or, if you're using yarn:
```bash
yarn add @allure-ai/sdk
```

## Authorization

### Use within external environments
You need an API key to access the resources. The API key can be configured when instantiating the library class, for example:
```ts
const service = new BeautyProductDatabase({
    apiKey: 'your-api-key'
});
```

Contact us to get the API key.

### Use within Allure AI Managed Environment

If you're using the library within Allure AI Managed Environment, the production credentials will be set automatically upon deployment. For the development credentials, you can use AWS CLI to set the necessary AWS credentials.

If you're using AWS SSO to login, don't forget to set the `AWS_PROFILE` environment variable:
```bash
export AWS_PROFILE=sso
```