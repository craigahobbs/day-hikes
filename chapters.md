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

links.0.name: Chapter Link
links.0.text.field: Chapter Title
links.0.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}

links.1.name: 0 - 5 mi
links.1.text.string: Link
links.1.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.distMax.number=5

links.2.name: 5 - 10 mi
links.2.text.string: Link
links.2.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.distMin.number=5&variables.distMax.number=10

links.3.name: 10+ mi
links.3.text.string: Link
links.3.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.distMin.number=10

links.4.name: 0 - 500 ft
links.4.text.string: Link
links.4.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.gainMax.number=500

links.5.name: 500 - 1500 ft
links.5.text.string: Link
links.5.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.gainMin.number=500&variables.gainMax.number=1500

links.6.name: 1500+ ft
links.6.text.string: Link
links.6.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.gainMin.number=1500

categoryFields.0: BookId
categoryFields.1: ChapterId
categoryFields.2: Chapter Link
fields.0: COUNT(HikeId)
fields.1: 0 - 5 mi
fields.2: 5 - 10 mi
fields.3: 10+ mi
fields.4: 0 - 500 ft
fields.5: 500 - 1500 ft
fields.6: 1500+ ft
~~~
