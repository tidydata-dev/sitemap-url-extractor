# Sitemap Extractor — All URLs from sitemap.xml — Python, Node.js & cURL examples

Give it a website and get **all the URLs listed in its sitemaps**, with `lastmod`, `priority` and `changefreq`. It finds the sitemaps through **robots.txt** and the usual locations, follows **sitemap indexes** and reads **.gz** files, removes duplicates and can keep only the URLs that contain a text such as `/blog/`. **$0.30 per 1,000 URLs**.

Hosted on Apify: **[Sitemap Extractor — All URLs from sitemap.xml](https://apify.com/tidydata/sitemap-url-extractor?fpr=wtg6qt)**. These examples show how to call it from your code; the Actor runs in the cloud, no API key for the source site, no proxies to manage.

## Python

```bash
pip install apify-client
export APIFY_TOKEN=...   # free account at apify.com → Settings → API & Integrations
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("tidydata/sitemap-url-extractor").call(run_input={
    "websites": [
        {
            "url": "https://www.bbc.com"
        },
        {
            "url": "https://apify.com/sitemap.xml?fpr=wtg6qt"
        }
    ],
    "maxUrlsPerSite": 5000,
    "urlContains": "/news/",
    "removeDuplicates": True
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print({k: item.get(k) for k in ['url', 'lastmod', 'changefreq', 'sitemap']})
```

## Node.js

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('tidydata/sitemap-url-extractor').call({"websites": [{"url": "https://apify.com?fpr=wtg6qt"}], "maxUrlsPerSite": 1000});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items.length, items[0]);
```

## cURL (one call, results as JSON)

```bash
curl -s -X POST "https://api.apify.com/v2/acts/tidydata~sitemap-url-extractor/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"websites": [{"url": "https://apify.com?fpr=wtg6qt"}], "maxUrlsPerSite": 1000}'
```

## More TidyData Actors

[YouTube Transcript](https://apify.com/tidydata/youtube-transcript-scraper?fpr=wtg6qt) · [YouTube Comments](https://apify.com/tidydata/youtube-comments-scraper?fpr=wtg6qt) · [YouTube Scraper](https://apify.com/tidydata/youtube-channel-scraper?fpr=wtg6qt) · [Website Contacts](https://apify.com/tidydata/website-contact-extractor?fpr=wtg6qt) · [Google News](https://apify.com/tidydata/google-news-scraper?fpr=wtg6qt) · [App Reviews](https://apify.com/tidydata/app-reviews-scraper?fpr=wtg6qt) · [Merge & Dedupe](https://apify.com/tidydata/merge-dedupe-datasets?fpr=wtg6qt) · [all of them](https://github.com/tidydata-dev)

Examples are MIT-licensed.

---
<sub>Links to apify.com include our affiliate ID: if you start a paid Apify plan through them, Apify pays TidyData a commission at no extra cost to you.</sub>
