[Home](#url=README.md) |
[Books](#url=books.md) |
Correlation


# Hike Data Correlation


### Hike Rating vs. Distance

~~~ line-chart
data.url: books.csv
data.joins.0.url: authors.csv
data.joins.0.leftFields.0: AuthorId
data.joins.1.url: hikes.csv
data.joins.1.leftFields.0: BookId

aggregation.categoryFields.0: BookId
aggregation.categoryFields.1: ChapterId
aggregation.categoryFields.2: HikeId
aggregation.measures.0.field: Rating
aggregation.measures.0.function: Average
aggregation.measures.1.field: Distance (mi)
aggregation.measures.1.function: Average

xField: AVERAGE(Distance (mi))
yFields.0: AVERAGE(Rating)
colorFields.0: BookId
colorFields.1: ChapterId
colorFields.2: HikeId
~~~


### Hike Rating vs. Elevation Gain

~~~ line-chart
data.url: books.csv
data.joins.0.url: authors.csv
data.joins.0.leftFields.0: AuthorId
data.joins.1.url: hikes.csv
data.joins.1.leftFields.0: BookId

aggregation.categoryFields.0: BookId
aggregation.categoryFields.1: ChapterId
aggregation.categoryFields.2: HikeId
aggregation.measures.0.field: Rating
aggregation.measures.0.function: Average
aggregation.measures.1.field: Elevation Gain (ft)
aggregation.measures.1.function: Average

xField: AVERAGE(Elevation Gain (ft))
yFields.0: AVERAGE(Rating)
colorFields.0: BookId
colorFields.1: ChapterId
colorFields.2: HikeId
~~~


### Hike Rating vs. High Point

~~~ line-chart
data.url: books.csv
data.joins.0.url: authors.csv
data.joins.0.leftFields.0: AuthorId
data.joins.1.url: hikes.csv
data.joins.1.leftFields.0: BookId

aggregation.categoryFields.0: BookId
aggregation.categoryFields.1: ChapterId
aggregation.categoryFields.2: HikeId
aggregation.measures.0.field: Rating
aggregation.measures.0.function: Average
aggregation.measures.1.field: High Point (ft)
aggregation.measures.1.function: Average

xField: AVERAGE(High Point (ft))
yFields.0: AVERAGE(Rating)
colorFields.0: BookId
colorFields.1: ChapterId
colorFields.2: HikeId
~~~
