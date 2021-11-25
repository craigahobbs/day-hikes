[Home](#url=README.md) |
[Books](#url=books.md)


# Hikes

~~~ data-table
data.url: books.csv

filters.0.field: BookId
filters.0.includes.0.variable: bookId

sorts.0.field: BookId

links.0.name: Book
links.0.text.field: Book Title
links.0.url.string: #url=chapters.md&variables.bookId.number={{BookId}}

fields.0: BookId
fields.1: Book
~~~

~~~ data-table
data.url: books.csv
data.joins.0.url: chapters.csv
data.joins.0.leftFields.0: BookId

variables.distMin.number: 0
variables.distMax.number: 100000
variables.gainMin.number: 0
variables.gainMax.number: 100000

filters.0.field: BookId
filters.0.includes.0.variable: bookId
filters.1.field: ChapterId
filters.1.includes.0.variable: chapterId

sorts.0.field: BookId
sorts.1.field: ChapterId

links.0.name: Chapter
links.0.text.field: Chapter Title
links.0.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}

links.1.name: Short Distance
links.1.text.string: 0 - 5 mi
links.1.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.distMax.number=5&variables.gainMin.number={{gainMin}}&variables.gainMax.number={{gainMax}}

links.2.name: Medium Distance
links.2.text.string: 5 - 10 mi
links.2.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.distMin.number=5&variables.distMax.number=10&variables.gainMin.number={{gainMin}}&variables.gainMax.number={{gainMax}}

links.3.name: Long Distance
links.3.text.string: 10+ mi
links.3.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.distMin.number=10&variables.gainMin.number={{gainMin}}&variables.gainMax.number={{gainMax}}

links.4.name: Low Gain
links.4.text.string: 0 - 500 ft
links.4.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.gainMax.number=500&variables.distMin.number={{distMin}}&variables.distMax.number={{distMax}}

links.5.name: Moderate Gain
links.5.text.string: 500 - 1500 ft
links.5.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.gainMin.number=500&variables.gainMax.number=1500&variables.distMin.number={{distMin}}&variables.distMax.number={{distMax}}

links.6.name: High Gain
links.6.text.string: 1500+ ft
links.6.url.string: #url=hikes.md&variables.bookId.number={{BookId}}&variables.chapterId.number={{ChapterId}}&variables.gainMin.number=1500&variables.distMin.number={{distMin}}&variables.distMax.number={{distMax}}

categoryFields.0: BookId
categoryFields.1: ChapterId
categoryFields.2: Chapter
fields.0: Short Distance
fields.1: Medium Distance
fields.2: Long Distance
fields.3: Low Gain
fields.4: Moderate Gain
fields.5: High Gain
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
