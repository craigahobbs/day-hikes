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

calculatedFields.0.name: Book
calculatedFields.0.expression: '[' & [Book Title] & '](#url=hikes.md&variables.BookId.number=' & [BookId] & ')'
calculatedFields.1.name: Min. Rating
calculatedFields.1.expression: if([ratingMin], [ratingMin], '')
calculatedFields.2.name: Min. Dist.
calculatedFields.2.expression: if([distMin], [distMin], '')
calculatedFields.3.name: Max. Dist.
calculatedFields.3.expression: if([distMax], [distMax], '')
calculatedFields.4.name: Min. Gain.
calculatedFields.4.expression: if([gainMin], [gainMin], '')
calculatedFields.5.name: Max. Gain.
calculatedFields.5.expression: if([gainMax], [gainMax], '')

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

aggregation.categoryFields.0: BookId
aggregation.categoryFields.1: Book
aggregation.categoryFields.2: Min. Rating
aggregation.categoryFields.3: Min. Dist.
aggregation.categoryFields.4: Max. Dist.
aggregation.categoryFields.5: Min. Gain.
aggregation.categoryFields.6: Max. Gain.
aggregation.measures.0.field: HikeId
aggregation.measures.0.function: Count

sorts.0.field: BookId

fields.0: BookId
fields.1: Book
fields.2: COUNT(HikeId)
fields.3: Min. Rating
fields.4: Min. Dist.
fields.5: Max. Dist.
fields.6: Min. Gain.
fields.7: Max. Gain.

markdownFields.0: Book
~~~

~~~ data-table
data.url: books.csv

calculatedFields.0.name: Rating (4+)
calculatedFields.0.expression: '[Excellent](#url=hikes.md&variables.BookId.number=' & [BookId] & '&variables.ChapterId.number=' & [ChapterId] & '&variables.ratingMin.number=4&variables.distMin.number=' & [distMin] & '&variables.distMax.number=' & [distMax] & '&variables.gainMin.number=' & [gainMin] & '&variables.gainMax.number=' & [gainMax] & ')'
calculatedFields.1.name: Rating (3+)
calculatedFields.1.expression: '[Good](#url=hikes.md&variables.BookId.number=' & [BookId] & '&variables.ChapterId.number=' & [ChapterId] & '&variables.ratingMin.number=3&variables.distMin.number=' & [distMin] & '&variables.distMax.number=' & [distMax] & '&variables.gainMin.number=' & [gainMin] & '&variables.gainMax.number=' & [gainMax] & ')'
calculatedFields.2.name: Short Dist.
calculatedFields.2.expression: '[0 - 5 mi](#url=hikes.md&variables.BookId.number=' & [BookId] & '&variables.ChapterId.number=' & [ChapterId] & '&variables.ratingMin.number=' & [ratingMin] & '&variables.distMax.number=5&variables.gainMin.number=' & [gainMin] & '&variables.gainMax.number=' & [gainMax] & ')'
calculatedFields.3.name: Med. Dist.
calculatedFields.3.expression: '[5 - 10 mi](#url=hikes.md&variables.BookId.number=' & [BookId] & '&variables.ChapterId.number=' & [ChapterId] & '&variables.ratingMin.number=' & [ratingMin] & '&variables.distMin.number=5&variables.distMax.number=10&variables.gainMin.number=' & [gainMin] & '&variables.gainMax.number=' & [gainMax] & ')'
calculatedFields.4.name: Long Dist.
calculatedFields.4.expression: '[10+ mi](#url=hikes.md&variables.BookId.number=' & [BookId] & '&variables.ChapterId.number=' & [ChapterId] & '&variables.ratingMin.number=' & [ratingMin] & '&variables.distMin.number=10&variables.gainMin.number=' & [gainMin] & '&variables.gainMax.number=' & [gainMax] & ')'
calculatedFields.5.name: Low Gain
calculatedFields.5.expression: '[0 - 500 ft](#url=hikes.md&variables.BookId.number=' & [BookId] & '&variables.ChapterId.number=' & [ChapterId] & '&variables.ratingMin.number=' & [ratingMin] & '&variables.gainMax.number=500&variables.distMin.number=' & [distMin] & '&variables.distMax.number=' & [distMax] & ')'
calculatedFields.6.name: Mod. Gain
calculatedFields.6.expression: '[500 - 1500 ft](#url=hikes.md&variables.BookId.number=' & [BookId] & '&variables.ChapterId.number=' & [ChapterId] & '&variables.ratingMin.number=' & [ratingMin] & '&variables.gainMin.number=500&variables.gainMax.number=1500&variables.distMin.number=' & [distMin] & '&variables.distMax.number=' & [distMax] & ')'
calculatedFields.7.name: High Gain
calculatedFields.7.expression: '[1500+ ft](#url=hikes.md&variables.BookId.number=' & [BookId] & '&variables.ChapterId.number=' & [ChapterId] & '&variables.ratingMin.number=' & [ratingMin] & '&variables.gainMin.number=1500&variables.distMin.number=' & [distMin] & '&variables.distMax.number=' & [distMax] & ')'

filters.0.field: BookId
filters.0.includes.0.variable: BookId

sorts.0.field: BookId

fields.0: Rating (4+)
fields.1: Rating (3+)
fields.2: Short Dist.
fields.3: Med. Dist.
fields.4: Long Dist.
fields.5: Low Gain
fields.6: Mod. Gain
fields.7: High Gain

markdownFields.0: Rating (4+)
markdownFields.1: Rating (3+)
markdownFields.2: Short Dist.
markdownFields.3: Med. Dist.
markdownFields.4: Long Dist.
markdownFields.5: Low Gain
markdownFields.6: Mod. Gain
markdownFields.7: High Gain
~~~

~~~ data-table
data.url: books.csv
data.joins.0.url: chapters.csv
data.joins.0.leftFields.0: BookId
data.joins.1.url: hikes.csv
data.joins.1.leftFields.0: BookId
data.joins.1.leftFields.1: ChapterId

calculatedFields.0.name: Chapter
calculatedFields.0.expression: '[' & [Chapter Title] & '](#url=hikes.md&variables.BookId.number=' & [BookId] & '&variables.ChapterId.number=' & [ChapterId] & '&variables.ratingMin.number=' & [ratingMin] & '&variables.distMin.number=' & [distMin] & '&variables.distMax.number=' & [distMax] & '&variables.gainMin.number=' & [gainMin] & '&variables.gainMax.number=' & [gainMax] & ')'

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

aggregation.categoryFields.0: BookId
aggregation.categoryFields.1: ChapterId
aggregation.categoryFields.2: Chapter
aggregation.measures.0.field: HikeId
aggregation.measures.0.function: Count

sorts.0.field: BookId
sorts.1.field: ChapterId

categoryFields.0: BookId
categoryFields.1: ChapterId
fields.0: Chapter
fields.1: COUNT(HikeId)

markdownFields.0: Chapter
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
