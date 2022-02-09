[Home](#url=README.md) |
[Books](#url=books.md) |
Correlation


# Hike Data Correlation


### Hike Rating vs. Distance

~~~ line-chart
data.url: books.csv
data.join.0.url: authors.csv
data.join.0.left: AuthorId
data.join.1.url: hikes.csv
data.join.1.left: BookId

calc.0.name: UniqueId
calc.0.expr: BookId + ', ' + ChapterId + ', ' + HikeId

x: Distance (mi)
y.0: Rating
color: UniqueId
~~~


### Hike Rating vs. Elevation Gain

~~~ line-chart
data.url: books.csv
data.join.0.url: authors.csv
data.join.0.left: AuthorId
data.join.1.url: hikes.csv
data.join.1.left: BookId

calc.0.name: UniqueId
calc.0.expr: BookId + ', ' + ChapterId + ', ' + HikeId

x: Elevation Gain (ft)
y.0: Rating
color: UniqueId
~~~


### Hike Rating vs. High Point

~~~ line-chart
data.url: books.csv
data.join.0.url: authors.csv
data.join.0.left: AuthorId
data.join.1.url: hikes.csv
data.join.1.left: BookId

calc.0.name: UniqueId
calc.0.expr: BookId + ', ' + ChapterId + ', ' + HikeId

x: High Point (ft)
y.0: Rating
color: UniqueId
~~~
