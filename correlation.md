[Home](#url=README.md) |
[Books](#url=books.md) |
Correlation


# Hike Data Correlation


### Hike Rating vs. Distance

~~~ line-chart
data.url: books.csv
data.joins.0.url: authors.csv
data.joins.0.leftExpression: [AuthorId]
data.joins.1.url: hikes.csv
data.joins.1.leftExpression: [BookId]

aggregation.categoryFields.0: BookId
aggregation.categoryFields.1: ChapterId
aggregation.categoryFields.2: HikeId
aggregation.measures.0.field: Rating
aggregation.measures.0.function: Average
aggregation.measures.1.field: Distance (mi)
aggregation.measures.1.function: Average

postCalculatedFields.0.name: ColorField
postCalculatedFields.0.expression: BookId + ', ' + ChapterId + ', ' + HikeId

xField: Distance (mi)
yFields.0: Rating
colorField: ColorField
~~~


### Hike Rating vs. Elevation Gain

~~~ line-chart
data.url: books.csv
data.joins.0.url: authors.csv
data.joins.0.leftExpression: [AuthorId]
data.joins.1.url: hikes.csv
data.joins.1.leftExpression: [BookId]

aggregation.categoryFields.0: BookId
aggregation.categoryFields.1: ChapterId
aggregation.categoryFields.2: HikeId
aggregation.measures.0.field: Rating
aggregation.measures.0.function: Average
aggregation.measures.1.field: Elevation Gain (ft)
aggregation.measures.1.function: Average

postCalculatedFields.0.name: ColorField
postCalculatedFields.0.expression: BookId + ', ' + ChapterId + ', ' + HikeId

xField: Elevation Gain (ft)
yFields.0: Rating
colorField: ColorField
~~~


### Hike Rating vs. High Point

~~~ line-chart
data.url: books.csv
data.joins.0.url: authors.csv
data.joins.0.leftExpression: [AuthorId]
data.joins.1.url: hikes.csv
data.joins.1.leftExpression: [BookId]

aggregation.categoryFields.0: BookId
aggregation.categoryFields.1: ChapterId
aggregation.categoryFields.2: HikeId
aggregation.measures.0.field: Rating
aggregation.measures.0.function: Average
aggregation.measures.1.field: High Point (ft)
aggregation.measures.1.function: Average

postCalculatedFields.0.name: ColorField
postCalculatedFields.0.expression: BookId + ', ' + ChapterId + ', ' + HikeId

xField: High Point (ft)
yFields.0: Rating
colorField: ColorField
~~~
