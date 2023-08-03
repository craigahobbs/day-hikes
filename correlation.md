[Home](#url=README.md) |
[Books](#url=books.md) |
Correlation

# Hike Data Correlation

~~~ markdown-script
# Load the book data
data = dataParseCSV(httpFetch('books.csv', null, true))
data = dataJoin(data, dataParseCSV(httpFetch('chapters.csv', null, true)), 'BookId')
data = dataJoin(data, dataParseCSV(httpFetch('hikes.csv', null, true)), "[BookId] + '-' + [ChapterId]")

# Add the unique ID calculated field
dataCalculatedField(data, 'UniqueId', "BookId + ', ' + ChapterId + ', ' + HikeId")

# Draw the hike rating vs distance scatter plot
markdownPrint('', '## Hike Rating vs. Distance')
dataLineChart(data, objectNew( \
    'x', 'Distance (mi)', \
    'y', arrayNew('Rating'), \
    'color', 'UniqueId' \
))

# Draw the hike rating vs elevation gain scatter plot
markdownPrint('', '## Hike Rating vs. Elevation Gain')
dataLineChart(data, objectNew( \
    'x', 'Elevation Gain (ft)', \
    'y', arrayNew('Rating'), \
    'color', 'UniqueId' \
))

# Draw the hike rating vs elevation gain scatter plot
markdownPrint('', '## Hike Rating vs. High Point')
dataLineChart(data, objectNew( \
    'x', 'High Point (ft)', \
    'y', arrayNew('Rating'), \
    'color', 'UniqueId' \
))
~~~
