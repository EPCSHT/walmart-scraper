# Actor - Walmart Scraper

## Walmart scraper

Since Walmart doesn't provide an API, this actor should help you to retrieve data from it.

The Walmart data scraper supports the following features:

-   Scrape product details - You can scrape attributes like images, seller information, photos, brands, variants, ID of the product and many more. You can find details below.

-   Scrape search results - You can scrape for a specific search result by keyword.

-   Scrape and filter any categories - You can provide any category with any kind of filter that you want.

-   Scrape a parent category and get all the items in its subcategory - You can provide any parent(big) category and let actor to scrape its sub-categories

-   Define maximum number of pages that needs to be scraped - If you only want to scrape first 3 pages, there is an option for that.

#### Walmart specific

Don't worry when you get little bit different products than you saw in browser page. Walmart is ordering products differently for each user.

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/walmart-scraper/issues).

### Incoming Changes

-   Fetching product reviews
-   Change shipping address
-   Fetch Questions and Answers
-   Performance upgrades

## Setup & Usage

You can see how this actor works in this video:

### Start URLs

[![Apify - Walmart Scraper - Start URLs](https://img.youtube.com/vi/F6vEx29zPsI/0.jpg)](https://www.youtube.com/watch?v=F6vEx29zPsI)

You can check the output of this video [here](https://api.apify.com/v2/datasets/7L16ONL5ezWnZntlB/items?clean=true&format=json).

### Search

[![Apify - Walmart Scraper - Search](https://img.youtube.com/vi/Qnz6CNdJP1c/0.jpg)](https://www.youtube.com/watch?v=Qnz6CNdJP1c)

You can check the output of this video [here](https://api.apify.com/v2/datasets/5zXILe6UpYc0GdCSB/items?clean=true&format=json).

## Input Parameters

The input of this scraper should be JSON containing the list of pages on Walmart that should be visited. Required fields are:

| Field                | Type    | Description                                                                                                                       |
| -------------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------- |
| startUrls            | Array   | (optional) List of Walmart URLs. You should only provide category detail, product detail or search URLs                           |
| maxItems             | Integer | (optional) You can limit scraped products. This should be useful when you search through the big subcategories.                   |
| endPage              | Integer | (optional) Final number of page that you want to scrape. Default is `Infinite`. This is applies to all list request individually. |
| search               | String  | (optional) Keyword that can be searched in Walmart search engine.                                                                 |
| proxy                | Object  | Proxy configuration                                                                                                               |
| extendOutputFunction | String  | (optional) Function that takes a JQuery handle ($) as argument and returns object with data                                       |
| outputFilterFunction | String  | (optional) Function that takes an output item as argument and returns the mapped data                                             |

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use <a href="https://www.apify.com/docs/proxy">Apify Proxy</a>.

##### Tip

Please keep in mind that for the sake of not to lose any of the data the actor returns all the possible output. That's it's suggested to use `outputFilterFunction` all the time.

When you want to have a filtering over a category URL; go to Walmart, create filters over the category and copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a search list or category list, then put the link for the page and have the `endPage` as 1.

With the last approach that explained above you can also fetch any interval of pages. If you provide the 5th page of a category and define the `endPage` parameter as 6 then you'll have the 5th and 6th pages only.


### Output Filter Function
This function is used for mapping the output data that the actor scrapes from the target. It has the following implementation:

```
data = eval(outputFilterFunction)(data);
```

So you can use this function to retrieve only the attributes you'd like to have. The following example is for retrieving only `id` and `name` attributes:

```
(object) => ({
    id: object.id,
    name: object.name
})
```

### Compute Unit Consumption

The actor optimized to run blazing fast and scrape many as product as possible. Therefore, it forefronts all product detail requests. If actor doesn't block very often it'll scrape 50 products in 2 minutes with ~0.3-0.5 compute units.

### Walmart Scraper Input example

```json
{
    "startUrls": [
        {
            "url": "https://www.walmart.com/browse/auto-tires/brake-pads/91083_1074765_9038935_4582920"
        },
        {
            "url": "https://www.walmart.com/browse/home/"
        },
        {
            "url": "https://www.walmart.com/search?grid=true&query=Mixed+Bouquets"
        },
        {
            "url": "https://www.walmart.com/ip/Mainstays-Blue-Sunflower-Mix-Bouquet/155345382"
        }
    ],
    "search": "apples",
    "endPage": 6,
    "maxItems": 100,
    "outputFilterFunction": "(object) => ({...object})"
}
```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.

When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with failure state and output an explanation of what is wrong.

## Walmart Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any languague (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this Walmart actor.

## Scraped Walmart Products

The structure of each item in Walmart products can be checked from here: https://api.apify.com/v2/datasets/3Nk7RZP8vheqazCtb/items?clean=true&format=json
