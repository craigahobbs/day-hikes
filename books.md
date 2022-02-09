[Home](#url=README.md) |
Books |
[Correlation](#url=correlation.md)


# Books

~~~ data-table
data.url: books.csv
data.join.0.url: authors.csv
data.join.0.left: [AuthorId]
data.join.1.url: hikes.csv
data.join.1.left: [BookId]

calc.0.name: Book
calc.0.expr: '[' + [Book Title] + '](#url=hikes.md&var.vBookId=' + [BookId] + ')'
calc.1.name: ISBN Link
calc.1.expr: '[' + [ISBN] + '](https://isbnsearch.org/isbn/' + [ISBN] + ')'

agg.category.0: Book
agg.category.1: Author
agg.category.2: ISBN Link
agg.measure.0.name: Hikes
agg.measure.0.field: HikeId
agg.measure.0.func: Count

sort.0.field: Book

markdown.0: Book
markdown.1: ISBN Link
~~~
