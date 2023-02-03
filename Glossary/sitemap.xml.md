- An XML file that lists the URLs for a site which are available for crawling. It can include extra information about each URL: last updated date and time, frequency of updates, and rate of importance/priority. 
- It is a _URL inclusion protocol_ and complements `robots.txt`.
- Example `sitemap.xml` file:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
	<url>
		<loc>http://www.example.com/</loc>
		<lastmod>2022-01-01</lastmod>
		<changefreq>monthly</changefreq>
		<priority>0.8</priority>
	</url>
</urlset>
```
