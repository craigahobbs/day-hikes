[Home](#url=README.md) |
Books |
[Correlation](#url=correlation.md)

# Books

~~~ markdown-script
# Load the book, author, and hike data
data = dataParseCSV(fetch('books.csv', null, true))
data = dataJoin(data, dataParseCSV(fetch('authors.csv', null, true)), 'AuthorId')
data = dataJoin(data, dataParseCSV(fetch('hikes.csv', null, true)), 'BookId')

# Add the book and ISBN link fields
dataCalculatedField(data, 'Book', "'[' + [Book Title] + '](#url=hikes.md&var.vBookId=' + [BookId] + ')'")
dataCalculatedField(data, 'ISBN', "'[' + [ISBN] + '](https://isbnsearch.org/isbn/' + [ISBN] + ')'")

# Count the number of hikes per book
dataBooks = dataAggregate(data, objectNew(\
    'categories', arrayNew('Book', 'Author', 'ISBN'), \
    'measures', arrayNew( \
        objectNew('name', 'Hikes', 'field', 'HikeId', 'function', 'count') \
    ) \
))

# Render the books table
dataSort(dataBooks, arrayNew(arrayNew('Book')))
dataTable(dataBooks, objectNew( \
    'fields', arrayNew('Book', 'Author', 'ISBN', 'Hikes'), \
    'markdown', arrayNew('Book', 'ISBN') \
))
~~~
