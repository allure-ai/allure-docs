# Beauty Product Database

This module is used to retrieve details of beauty products in our database.

## Retrieving Article by Article No (AAN)
An item in the Beauty Product Database (e.g. skincare product, ingredient) is known as an Article. Each Article is identified by its Article No (AAN). You can use `retrieveArticle` method to retrieve up to 100 articles at once.

```ts
import BeautyProductDatabase, { ArticleType, SkincareProduct } from '@allure-ai/sdk/services/BeautyProductDatabase';
import apiConfig from './apiConfig';

const service = new BeautyProductDatabase(apiConfig);

async function getSkincareProducts(articleNo: string[]): Promise<Partial<SkincareProduct>[]> {
    const articles = await service.retrieveArticles<SkincareProduct>(ArticleType.SkincareProduct, articleNo);
    return articles;
}
```

You can also specify the fields to get only what you need.
```ts
// ...
const fields = ['article_no', 'name'];
const articles = await service.retrieveArticles<SkincareProduct>(ArticleType.SkincareProduct, articleNo, fields);
// ...
```

Note that the return value of `retrieveArticles` is `Partial<T>`, since you may pick which attributes to retrieve at runtime.

## Article Types

TODO