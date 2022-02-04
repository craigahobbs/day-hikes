[Home](#url=README.md) |
[Books](#url=books.md) |
[Correlation](#url=correlation.md)


# Hikes

~~~ data-table
data.url: books.csv
data.joins.0.url: chapters.csv
data.joins.0.leftExpression: [BookId]
data.joins.1.url: hikes.csv
data.joins.1.leftExpression: [BookId] + '-' + [ChapterId]

calculatedFields.0.name: Book
calculatedFields.0.expression: '[' + markdownEncode([Book Title]) + '](#url=hikes.md&var.vBookId=' + [BookId] + ')'
calculatedFields.1.name: Min. Rating
calculatedFields.1.expression: if(vRatingMin, vRatingMin, '')
calculatedFields.2.name: Min. Dist.
calculatedFields.2.expression: if(vDistMin, vDistMin, '')
calculatedFields.3.name: Max. Dist.
calculatedFields.3.expression: if(vDistMax, vDistMax, '')
calculatedFields.4.name: Min. Gain.
calculatedFields.4.expression: if(vGainMin, vGainMin, '')
calculatedFields.5.name: Max. Gain.
calculatedFields.5.expression: if(vGainMax, vGainMax, '')

filters.0: if(vBookId, BookId == vBookId, 1)
filters.1: if(vChapterId, ChapterId == vChapterId, 1)
filters.2: if(vRatingMin, Rating >= vRatingMin, 1)
filters.3: if(vDistMin, [Distance (mi)] >= vDistMin, 1) && if(vDistMax, [Distance (mi)] <= vDistMax, 1)
filters.4: if(vGainMin, [Elevation Gain (ft)] >= vGainMin, 1) && if(vGainMax, [Elevation Gain (ft)] <= vGainMax, 1)

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
calculatedFields.0.expression: '[Excellent](#url=hikes.md&var.vBookId=' + [BookId] + if(vChapterId, '&var.vChapterId=' + vChapterId, '') + '&var.vRatingMin=4' + if(vDistMin, '&var.vDistMin=' + vDistMin, '') + if(vDistMax, '&var.vDistMax=' + vDistMax, '') + if(vGainMin, '&var.vGainMin=' + vGainMin, '') + if(vGainMax, '&var.vGainMax=' + vGainMax, '') + ')'
calculatedFields.1.name: Rating (3+)
calculatedFields.1.expression: '[Good](#url=hikes.md&var.vBookId=' + [BookId] + if(vChapterId, '&var.vChapterId=' + vChapterId, '') + '&var.vRatingMin=3' + if(vDistMin, '&var.vDistMin=' + vDistMin, '') + if(vDistMax, '&var.vDistMax=' + vDistMax, '') + if(vGainMin, '&var.vGainMin=' + vGainMin, '') + if(vGainMax, '&var.vGainMax=' + vGainMax, '') + ')'
calculatedFields.2.name: Short Dist.
calculatedFields.2.expression: '[0 - 5 mi](#url=hikes.md&var.vBookId=' + [BookId] + if(vChapterId, '&var.vChapterId=' + vChapterId, '') + if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + '&var.vDistMin=0&var.vDistMax=5' + if(vGainMin, '&var.vGainMin=' + vGainMin, '') + if(vGainMax, '&var.vGainMax=' + vGainMax, '') + ')'
calculatedFields.3.name: Med. Dist.
calculatedFields.3.expression: '[5 - 10 mi](#url=hikes.md&var.vBookId=' + [BookId] + if(vChapterId, '&var.vChapterId=' + vChapterId, '') + if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + '&var.vDistMin=5&var.vDistMax=10' + if(vGainMin, '&var.vGainMin=' + vGainMin, '') + if(vGainMax, '&var.vGainMax=' + vGainMax, '') + ')'
calculatedFields.4.name: Long Dist.
calculatedFields.4.expression: '[10+ mi](#url=hikes.md&var.vBookId=' + [BookId] + if(vChapterId, '&var.vChapterId=' + vChapterId, '') + if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + '&var.vDistMin=10&var.vDistMax=1000' + if(vGainMin, '&var.vGainMin=' + vGainMin, '') + if(vGainMax, '&var.vGainMax=' + vGainMax, '') + ')'
calculatedFields.5.name: Low Gain
calculatedFields.5.expression: '[0 - 500 ft](#url=hikes.md&var.vBookId=' + [BookId] + if(vChapterId, '&var.vChapterId=' + vChapterId, '') + if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + if(vDistMin, '&var.vDistMin=' + vDistMin, '') + if(vDistMax, '&var.vDistMax=' + vDistMax, '') + '&var.vGainMin=0&var.vGainMax=500)'
calculatedFields.6.name: Mod. Gain
calculatedFields.6.expression: '[500 - 1500 ft](#url=hikes.md&var.vBookId=' + [BookId] + if(vChapterId, '&var.vChapterId=' + vChapterId, '') + if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + if(vDistMin, '&var.vDistMin=' + vDistMin, '') + if(vDistMax, '&var.vDistMax=' + vDistMax, '') + '&var.vGainMin=500&var.vGainMax=1500)'
calculatedFields.7.name: High Gain
calculatedFields.7.expression: '[1500+ ft](#url=hikes.md&var.vBookId=' + [BookId] + if(vChapterId, '&var.vChapterId=' + vChapterId, '') + if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + if(vDistMin, '&var.vDistMin=' + vDistMin, '') + if(vDistMax, '&var.vDistMax=' + vDistMax, '') + '&var.vGainMin=1500&var.vGainMax=10000)'

filters.0: if(vBookId, BookId == vBookId, 1)

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
data.joins.0.leftExpression: [BookId]
data.joins.1.url: hikes.csv
data.joins.1.leftExpression: [BookId] + '-' + [ChapterId]

calculatedFields.0.name: Chapter
calculatedFields.0.expression: '[' + markdownEncode([Chapter Title]) + '](#url=hikes.md&var.vBookId=' + [BookId] + '&var.vChapterId=' + [ChapterId] + if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + if(vDistMin, '&var.vDistMin=' + vDistMin, '') + if(vDistMax, '&var.vDistMax=' + vDistMax, '') + if(vGainMin, '&var.vGainMin=' + vGainMin, '') + if(vGainMax, '&var.vGainMax=' + vGainMax, '') + ')'

filters.0: if(vBookId, BookId == vBookId, 1)
filters.1: if(vChapterId, ChapterId == vChapterId, 1)
filters.2: if(vRatingMin, Rating >= vRatingMin, 1)
filters.3: if(vDistMin, [Distance (mi)] >= vDistMin, 1) && if(vDistMax, [Distance (mi)] <= vDistMax, 1)
filters.4: if(vGainMin, [Elevation Gain (ft)] >= vGainMin, 1) && if(vGainMax, [Elevation Gain (ft)] <= vGainMax, 1)

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
data.joins.0.leftExpression: [BookId]
data.joins.1.url: hikes.csv
data.joins.1.leftExpression: [BookId] + '-' + [ChapterId]

filters.0: if(vBookId, BookId == vBookId, 1)
filters.1: if(vChapterId, ChapterId == vChapterId, 1)
filters.2: if(vRatingMin, Rating >= vRatingMin, 1)
filters.3: if(vDistMin, [Distance (mi)] >= vDistMin, 1) && if(vDistMax, [Distance (mi)] <= vDistMax, 1)
filters.4: if(vGainMin, [Elevation Gain (ft)] >= vGainMin, 1) && if(vGainMax, [Elevation Gain (ft)] <= vGainMax, 1)

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
