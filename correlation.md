[Home](#url=README.md) |
[Books](#url=books.md) |
Correlation


# Hike Data Correlation


### Hike Rating vs. Distance

~~~ line-chart
data.url: books.csv
data.joins.0.url: authors.csv
data.joins.0.leftExpression: AuthorId
data.joins.1.url: hikes.csv
data.joins.1.leftExpression: BookId

calculatedFields.0.name: UniqueId
calculatedFields.0.expression: BookId + ', ' + ChapterId + ', ' + HikeId

xField: Distance (mi)
yFields.0: Rating
colorField: UniqueId
~~~


### Hike Rating vs. Elevation Gain

~~~ line-chart
data.url: books.csv
data.joins.0.url: authors.csv
data.joins.0.leftExpression: AuthorId
data.joins.1.url: hikes.csv
data.joins.1.leftExpression: BookId

calculatedFields.0.name: UniqueId
calculatedFields.0.expression: BookId + ', ' + ChapterId + ', ' + HikeId

xField: Elevation Gain (ft)
yFields.0: Rating
colorField: UniqueId
~~~


### Hike Rating vs. High Point

~~~ line-chart
data.url: books.csv
data.joins.0.url: authors.csv
data.joins.0.leftExpression: AuthorId
data.joins.1.url: hikes.csv
data.joins.1.leftExpression: BookId

calculatedFields.0.name: UniqueId
calculatedFields.0.expression: BookId + ', ' + ChapterId + ', ' + HikeId

xField: High Point (ft)
yFields.0: Rating
colorField: UniqueId
~~~
