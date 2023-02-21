# Review Endpoint Specification

## Request specifications

Business Suite will send an HTTP GET request to the endpoint specified in the Business Suite Dashboard. 

!!! warning "The server must respond within 5 seconds, otherwise the reviews will not be displayed."


### Query parameters

| Param                | Type     | Description                                                                                                             |
|----------------------|----------|-------------------------------------------------------------------------------------------------------------------------|
| `articleNo`          | `string` | Allure Article Number (AAN) of the referenced product.                                                                  |
| `locale`             | `string` | Locale of the widget. **Currently, only `id_ID` is supported**.                                                         |
| `offset`             | `number` | Offset number for pagination, starts from 0.                                                                            |
| `limit`              | `number` | Number of reviews to fetch.                                                                                             |
| `filter_[filterKey]` | `string` | Custom filter picked by the user. For example, if the filter key is `skintype`, the parameter name will be `filter_skintype`. |
| `sort_[sortKey]`     | `string` | Custom sort picked by the user. For example, if the filter key is `rating`, the parameter name will be `sort_rating`.     |

#### Example

- Endpoint: `https://api.acme.com/reviews`
- Article No: `PSA00000001`
- Applied filters:
    - `skintype` = `sensitive`
    - `recommend` = `yes`
- Applied sorts:
    - `rating` = `ascending`

The request URL becomes:
```
https://api.acme.com/reviews?articleNo=PSA00000001&offset=0&limit=10&locale=id_ID&filter_skintype=sensitive&filter_recommend=yes&sort_rating=ascending
```

## Response specification

The endpoint shall return a schema.org-compliant JSON object with type `Product`.

```json
{
	"@context": "https://schema.org",
	"@type": "Product",
	"aggregateRating": {
		"@type": "AggregateRating",
		"ratingCount": 100,
		"ratingValue": 4,
		"worstRating": 0,
		"bestRating": 5
	},
	"review": [
		// Array of reviews, see below for Review body
	]
}
```

### Individual Review format

```json
{
	"@context": "https://schema.org",
	"@type": "Review",
	"author": {
		"@type": "Person",
		"name": "John Doe",
		"image": "https://image.org/image.png",
		"url": "https://example.com/link-to-user-profile-page",
		"allure:annotations": [
			"Kulit Sensitif",
			"> 40 tahun"
		]
	},
	"datePublished": "2022-01-01",
	"reviewBody": "This is review body",
	"reviewRating": {
		"@type": "Rating",
		"ratingValue": 4,
		"worstRating": 0,
		"bestRating": 5
	},
	"allure:additionalComponents": [
		{
			"title": "Akan beli lagi?",
			"value": "Ya"
		}
	],
	"allure:photos": [
		"https://url-to/photos1.jpg",
        "https://url-to/photos2.jpg"
	]
}
```