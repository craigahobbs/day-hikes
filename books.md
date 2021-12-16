[Home](#url=README.md) |
Books |
[Correlation](#url=correlation.md)


# Books

~~~ data-table
data.url: books.csv
data.joins.0.url: authors.csv
data.joins.0.leftFields.0: AuthorId
data.joins.1.url: hikes.csv
data.joins.1.leftFields.0: BookId

calculatedFields.0.name: Book
calculatedFields.0.expression: '[' & [Book Title] & '](#url=hikes.md&variables.BookId.number=' & [BookId] & ')'
calculatedFields.1.name: ISBN Link
calculatedFields.1.expression: '[' & [ISBN] & '](https://isbnsearch.org/isbn/' & [ISBN] & ')'

aggregation.categoryFields.0: BookId
aggregation.categoryFields.1: Book
aggregation.categoryFields.2: Author
aggregation.categoryFields.3: ISBN Link
aggregation.measures.0.field: HikeId
aggregation.measures.0.function: Count

sorts.0.field: Book

categoryFields.0: Book
fields.0: Author
fields.1: COUNT(HikeId)
fields.2: ISBN Link

markdownFields.0: Book
markdownFields.1: ISBN Link
~~~
