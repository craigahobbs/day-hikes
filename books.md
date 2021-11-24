[Home](#url=README.md)


# Books

~~~ data-table
data.url: books.csv
data.joins.0.url: authors.csv
data.joins.0.leftFields.0: AuthorId
data.joins.1.url: hikes.csv
data.joins.1.leftFields.0: BookId

aggregation.categories.0.field: BookId
aggregation.categories.1.field: Book Title
aggregation.categories.2.field: Author
aggregation.measures.0.field: HikeId
aggregation.measures.0.function: Count

sorts.0.field: Book Title

links.0.name: Book
links.0.text.field: Book Title
links.0.url.string: #url=chapters.md&variables.bookId.number={{BookId}}

categoryFields.0: Book
categoryFields.1: Author
fields.0: COUNT(HikeId)
~~~
