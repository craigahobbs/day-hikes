[Home](#url=README.md) |
[Books](#url=books.md)


# Hikes

~~~ data-table
data.url: books.csv
data.joins.0.url: chapters.csv
data.joins.0.leftFields.0: BookId

filters.0.field: BookId
filters.0.includes.0.variable: bookId
filters.1.field: ChapterId
filters.1.includes.0.variable: chapterId

links.0.name: Book Link
links.0.text.field: Book Title
links.0.url.string: #url=chapters.md&variables.bookId.number={{BookId}}

fields.0: BookId
fields.1: Book Link
fields.2: ChapterId
fields.3: Chapter Title
~~~

~~~ data-table
data.url: books.csv
data.joins.0.url: chapters.csv
data.joins.0.leftFields.0: BookId
data.joins.1.url: hikes.csv
data.joins.1.leftFields.0: BookId
data.joins.1.leftFields.1: ChapterId

filters.0.field: BookId
filters.0.includes.0.variable: bookId
filters.1.field: ChapterId
filters.1.includes.0.variable: chapterId
filters.2.field: Distance (mi)
filters.2.gte.variable: distMin
filters.2.lte.variable: distMax
filters.3.field: Elevation Gain (ft)
filters.3.gte.variable: gainMin
filters.3.lte.variable: gainMax

sorts.0.field: Rating
sorts.0.desc: true
sorts.1.field: Hike Title

fields.0: BookId
fields.1: ChapterId
fields.2: HikeId
fields.3: Hike Title
fields.4: Rating
fields.5: Difficulty
fields.6: Distance (mi)
fields.7: Elevation Gain (ft)
fields.8: High Point (ft)
fields.9: Season
~~~
