[Home](#url=README.md) |
[Books](#url=books.md)


# Chapters

~~~ data-table
data.url: books.csv

filters.0.field: BookId
filters.0.includes.0.variable: bookId

fields.0: BookId
fields.1: Book Title
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

aggregation.categories.0.field: BookId
aggregation.categories.1.field: Book Title
aggregation.categories.2.field: ChapterId
aggregation.categories.3.field: Chapter Title
aggregation.measures.0.field: HikeId
aggregation.measures.0.function: Count

sorts.0.field: BookId
sorts.1.field: ChapterId

links.0.name: Chapter
links.0.text.field: Chapter Title
links.0.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}

links.1.name: Short Distance
links.1.text.string: 0 - 5 mi
links.1.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.distMax.number=5

links.2.name: Medium Distance
links.2.text.string: 5 - 10 mi
links.2.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.distMin.number=5&variables.distMax.number=10

links.3.name: Long Distance
links.3.text.string: 10+ mi
links.3.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.distMin.number=10

links.4.name: Low Gain
links.4.text.string: 0 - 500 ft
links.4.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.gainMax.number=500

links.5.name: Moderate Gain
links.5.text.string: 500 - 1500 ft
links.5.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.gainMin.number=500&variables.gainMax.number=1500

links.6.name: High Gain
links.6.text.string: 1500+ ft
links.6.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.gainMin.number=1500

categoryFields.0: BookId
categoryFields.1: ChapterId
categoryFields.2: Chapter
fields.0: COUNT(HikeId)
fields.1: Short Distance
fields.2: Medium Distance
fields.3: Long Distance
fields.4: Low Gain
fields.5: Moderate Gain
fields.6: High Gain
~~~
