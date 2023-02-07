# Pixabay Side-by-Side

A deep dive into the data behind the [Side-by-Side Pixabay Search Comparison](https://app.kailualabs.com/comparison/image-keyword-vs-semantic-search).

## About the Data

We gathered 143,549 photos from [Pixabay’s API](https://pixabay.com/api/docs/) as follows. The API docs describe 4 filter parameters (color, category, orientation, and order). For each parameter, a list of acceptable values is provided. We iterated through all possible combinations of values of those 4 filters listed in the documentation. We only gathered safe-search filtered photos. The query keywords parameter was left empty for all queries. We randomly sampled 25,000 photos from that set. Since Pixabay’s image links were temporary, we are hosting a copy of each for this demo. Here’s an example of one row of data from the resulting JSON file we created:

```json
{
	"id": 3308154,
	"pageURL": "https://pixabay.com/photos/buddha-s-lamp-mussaenda-pubescens-3308154/",
	"tags": [
		"buddha's lamp",
		"mussaenda pubescens",
		"white"
	],
	"webformatURL": "https://d11p8vtjlacpl4.cloudfront.net/images/3308154.jpg",
	"webformatWidth": 640,
	"webformatHeight": 618
}
```

For more information, check out the source code or feel free to reach out to us at [hello@kailualabs.com](mailto:hello@kailualabs.com).

## Algolia Index Setup

For the most part, we used Algolia’s search out-of-the-box. The only thing that we changed was the searchable attributes, as recommended by Algolia.

1. By default, all attributes are searchable. Could be a problem as it can lead to too much noise according to Algolia.
2. Algolia says that you should rank searchable attributes as well (i.e. one attribute might weigh more than another)
    1. We used the `tags` and `pageURL` column as searchable attributes, ranking `tags` as more important than `pageURL`.

## Kailua Labs Index Setup

We used Kailua Labs search out-of-the-box. We uploaded the [JSON file](https://github.com/kailualabs/pixabay-side-by-side/blob/main/pixabay_data.json) and used the /search API with the following parameters.

You can get started with Kailua Labs by going to [https://kailualabs.com](https://kailualabs.com) and joining the waitlist.

## Important Links

- [Final JSON data used for indexing](https://github.com/kailualabs/pixabay-side-by-side/blob/main/pixabay_data.json)
- [Jupyter notebook showing Algolia index setup & data upload](https://github.com/kailualabs/pixabay-side-by-side/blob/main/algolia_index_setup.ipynb)
- [Pixabay’s API docs](https://pixabay.com/api/docs/)
