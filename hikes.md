[Home](#url=README.md) |
[Books](#url=books.md) |
[Correlation](#url=correlation.md)


# Hikes

~~~ data-table
data.url: books.csv
data.joins.0.url: chapters.csv
data.joins.0.leftFields.0: BookId
data.joins.1.url: hikes.csv
data.joins.1.leftFields.0: BookId
data.joins.1.leftFields.1: ChapterId

filters.0.field: BookId
filters.0.includes.0.variable: BookId
filters.1.field: ChapterId
filters.1.includes.0.variable: ChapterId
filters.2.field: Rating
filters.2.gte.variable: ratingMin
filters.3.field: Distance (mi)
filters.3.gte.variable: distMin
filters.3.lte.variable: distMax
filters.4.field: Elevation Gain (ft)
filters.4.gte.variable: gainMin
filters.4.lte.variable: gainMax

aggregation.categories.0.field: BookId
aggregation.categories.1.field: Book Title
aggregation.measures.0.field: HikeId
aggregation.measures.0.function: Count

sorts.0.field: BookId

links.0.name: Book
links.0.text.field: Book Title
links.0.url.string: #url=hikes.md&variables.BookId.number={{BookId}}

links.1.name: Min. Rating
links.1.text.variable: ratingMin

links.2.name: Min. Dist.
links.2.text.variable: distMin

links.3.name: Max. Dist.
links.3.text.variable: distMax

links.4.name: Min. Gain.
links.4.text.variable: gainMin

links.5.name: Max. Gain.
links.5.text.variable: gainMax

fields.0: BookId
fields.1: Book
fields.2: COUNT(HikeId)
fields.3: Min. Rating
fields.4: Min. Dist.
fields.5: Max. Dist.
fields.6: Min. Gain.
fields.7: Max. Gain.
~~~

~~~ data-table
data.url: books.csv

filters.0.field: BookId
filters.0.includes.0.variable: BookId

sorts.0.field: BookId

links.0.name: Rating (4+)
links.0.text.string: Excellent
links.0.url.string: #url=hikes.md&variables.BookId.number={{BookId}}&variables.ChapterId.number={{ChapterId}}&variables.ratingMin.number=4&variables.distMin.number={{distMin}}&variables.distMax.number={{distMax}}&variables.gainMin.number={{gainMin}}&variables.gainMax.number={{gainMax}}

links.1.name: Rating (3+)
links.1.text.string: Good
links.1.url.string: #url=hikes.md&variables.BookId.number={{BookId}}&variables.ChapterId.number={{ChapterId}}&variables.ratingMin.number=3&variables.distMin.number={{distMin}}&variables.distMax.number={{distMax}}&variables.gainMin.number={{gainMin}}&variables.gainMax.number={{gainMax}}

links.2.name: Short Dist.
links.2.text.string: 0 - 5 mi
links.2.url.string: #url=hikes.md&variables.BookId.number={{BookId}}&variables.ChapterId.number={{ChapterId}}&variables.ratingMin.number={{ratingMin}}&variables.distMax.number=5&variables.gainMin.number={{gainMin}}&variables.gainMax.number={{gainMax}}

links.3.name: Med. Dist.
links.3.text.string: 5 - 10 mi
links.3.url.string: #url=hikes.md&variables.BookId.number={{BookId}}&variables.ChapterId.number={{ChapterId}}&variables.ratingMin.number={{ratingMin}}&variables.distMin.number=5&variables.distMax.number=10&variables.gainMin.number={{gainMin}}&variables.gainMax.number={{gainMax}}

links.4.name: Long Dist.
links.4.text.string: 10+ mi
links.4.url.string: #url=hikes.md&variables.BookId.number={{BookId}}&variables.ChapterId.number={{ChapterId}}&variables.ratingMin.number={{ratingMin}}&variables.distMin.number=10&variables.gainMin.number={{gainMin}}&variables.gainMax.number={{gainMax}}

links.5.name: Low Gain
links.5.text.string: 0 - 500 ft
links.5.url.string: #url=hikes.md&variables.BookId.number={{BookId}}&variables.ChapterId.number={{ChapterId}}&variables.ratingMin.number={{ratingMin}}&variables.gainMax.number=500&variables.distMin.number={{distMin}}&variables.distMax.number={{distMax}}

links.6.name: Mod. Gain
links.6.text.string: 500 - 1500 ft
links.6.url.string: #url=hikes.md&variables.BookId.number={{BookId}}&variables.ChapterId.number={{ChapterId}}&variables.ratingMin.number={{ratingMin}}&variables.gainMin.number=500&variables.gainMax.number=1500&variables.distMin.number={{distMin}}&variables.distMax.number={{distMax}}

links.7.name: High Gain
links.7.text.string: 1500+ ft
links.7.url.string: #url=hikes.md&variables.BookId.number={{BookId}}&variables.ChapterId.number={{ChapterId}}&variables.ratingMin.number={{ratingMin}}&variables.gainMin.number=1500&variables.distMin.number={{distMin}}&variables.distMax.number={{distMax}}

fields.0: Rating (4+)
fields.1: Rating (3+)
fields.2: Short Dist.
fields.3: Med. Dist.
fields.4: Long Dist.
fields.5: Low Gain
fields.6: Mod. Gain
fields.7: High Gain
~~~

~~~ data-table
data.url: books.csv
data.joins.0.url: chapters.csv
data.joins.0.leftFields.0: BookId
data.joins.1.url: hikes.csv
data.joins.1.leftFields.0: BookId
data.joins.1.leftFields.1: ChapterId

filters.0.field: BookId
filters.0.includes.0.variable: BookId
filters.1.field: ChapterId
filters.1.includes.0.variable: ChapterId
filters.2.field: Rating
filters.2.gte.variable: ratingMin
filters.3.field: Distance (mi)
filters.3.gte.variable: distMin
filters.3.lte.variable: distMax
filters.4.field: Elevation Gain (ft)
filters.4.gte.variable: gainMin
filters.4.lte.variable: gainMax

aggregation.categories.0.field: BookId
aggregation.categories.1.field: ChapterId
aggregation.categories.2.field: Chapter Title
aggregation.measures.0.field: HikeId
aggregation.measures.0.function: Count

sorts.0.field: BookId
sorts.1.field: ChapterId

links.0.name: Chapter
links.0.text.field: Chapter Title
links.0.url.string: #url=hikes.md&variables.BookId.number={{BookId}}&variables.ChapterId.number={{ChapterId}}&variables.ratingMin.number={{ratingMin}}&variables.distMin.number={{distMin}}&variables.distMax.number={{distMax}}&variables.gainMin.number={{gainMin}}&variables.gainMax.number={{gainMax}}

categoryFields.0: BookId
categoryFields.1: ChapterId
fields.0: Chapter
fields.1: COUNT(HikeId)
~~~

~~~ data-table
data.url: books.csv
data.joins.0.url: chapters.csv
data.joins.0.leftFields.0: BookId
data.joins.1.url: hikes.csv
data.joins.1.leftFields.0: BookId
data.joins.1.leftFields.1: ChapterId

filters.0.field: BookId
filters.0.includes.0.variable: BookId
filters.1.field: ChapterId
filters.1.includes.0.variable: ChapterId
filters.2.field: Rating
filters.2.gte.variable: ratingMin
filters.3.field: Distance (mi)
filters.3.gte.variable: distMin
filters.3.lte.variable: distMax
filters.4.field: Elevation Gain (ft)
filters.4.gte.variable: gainMin
filters.4.lte.variable: gainMax

sorts.0.field: Rating
sorts.0.desc: true
sorts.1.field: Difficulty
sorts.2.field: Hike Title

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
