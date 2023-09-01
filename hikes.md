[Home](#url=README.md) |
[Books](#url=books.md) |
[Correlation](#url=correlation.md)

# Hikes

~~~ markdown-script
# Filter link helper function
function bookLink(text, bookId, chapterId, ratingMin, distMin, distMax, gainMin, gainMax)
    bookId = if(bookId, bookId, vBookId)
    chapterId = if(chapterId, chapterId, vChapterId)
    ratingMin = if(ratingMin, ratingMin, vRatingMin)
    distMin = if(distMin != null, if(distMin, distMin), vDistMin)
    distMax = if(distMax != null, if(distMax, distMax), vDistMax)
    gainMin = if(gainMin != null, if(gainMin, gainMin), vGainMin)
    gainMax = if(gainMax != null, if(gainMax, gainMax), vGainMax)
    return '[' + markdownEscape(text) + '](#url=hikes.md' + \
        if(bookId, '&var.vBookId=' + bookId, '') + \
        if(chapterId, '&var.vChapterId=' + chapterId, '') + \
        if(ratingMin, '&var.vRatingMin=' + ratingMin, '') + \
        if(distMin, '&var.vDistMin=' + distMin, '') + \
        if(distMax, '&var.vDistMax=' + distMax, '') + \
        if(gainMin, '&var.vGainMin=' + gainMin, '') + \
        if(gainMax, '&var.vGainMax=' + gainMax, '') + ')'
endfunction

# Render the filter links
markdownPrint( \
    '**Rating:** ', \
    bookLink('Excellent', null, null, 4), '|', \
    bookLink('Good', null, null, 3) + '  ', \
    '**Distance:** ', \
    bookLink('Short', null, null, null, 0, 5), '|', \
    bookLink('Medium', null, null, null, 5, 10), '|', \
    bookLink('Long', null, null, null, 10, 0) + '  ', \
    '**Gain:** ', \
    bookLink('Low', null, null, null, null, null, 0, 500), '|', \
    bookLink('Moderate', null, null, null, null, null, 500, 1500), '|', \
    bookLink('High', null, null, null, null, null, 1500, 0) \
)

# Load the book data
data = dataParseCSV(systemFetch('books.csv', null, true))
data = dataJoin(data, dataParseCSV(systemFetch('chapters.csv', null, true)), 'BookId')
data = dataJoin(data, dataParseCSV(systemFetch('hikes.csv', null, true)), "BookId + '-' + ChapterId")

# Filter & sort
filterVariables = objectNew( \
    'vBookId', vBookId, \
    'vChapterId', vChapterId, \
    'vRatingMin', vRatingMin, \
    'vDistMin', vDistMin, \
    'vDistMax', vDistMax, \
    'vGainMin', vGainMin, \
    'vGainMax', vGainMax, \
    'bookLink', bookLink \
)
data = dataFilter( \
    data, \
    '(vBookId == null || BookId == vBookId) && ' + \
        '(vChapterId == null || ChapterId == vChapterId) && ' + \
        '(vRatingMin == null || Rating >= vRatingMin) && ' + \
        '(vDistMin == null || [Distance (mi)] >= vDistMin) && ' + \
        '(vDistMax == null || [Distance (mi)] <= vDistMax) && ' + \
        '(vGainMin == null || [Elevation Gain (ft)] >= vGainMin) && ' + \
        '(vGainMax == null || [Elevation Gain (ft)] <= vGainMax)', \
    filterVariables \
)
dataSort(data, arrayNew(arrayNew('BookId'), arrayNew('ChapterId'), arrayNew('Rating', true), arrayNew('Difficulty'), arrayNew('Hike Title')))

# Count the filtered hikes by book
dataBooks = dataAggregate(data, objectNew( \
    'categories', arrayNew('BookId', 'Book Title'), \
    'measures', arrayNew( \
        objectNew('name', 'Hikes', 'field', 'HikeId', 'function', 'count') \
    ) \
))

# Add the book calculated fields
dataCalculatedField(dataBooks, 'Book', "'[' + markdownEscape([Book Title]) + '](#url=hikes.md&var.vBookId=' + BookId + ')'", filterVariables)
dataCalculatedField(dataBooks, 'Min. Rating', "if(vRatingMin, vRatingMin, '')", filterVariables)
dataCalculatedField(dataBooks, 'Min. Dist.', "if(vDistMin, vDistMin, '')", filterVariables)
dataCalculatedField(dataBooks, 'Max. Dist.', "if(vDistMax, vDistMax, '')", filterVariables)
dataCalculatedField(dataBooks, 'Min. Gain', "if(vGainMin, vGainMin, '')", filterVariables)
dataCalculatedField(dataBooks, 'Max. Gain', "if(vGainMax, vGainMax, '')", filterVariables)

# Count the filtered hikes by book/chapter
dataChapters = dataAggregate(data, objectNew( \
    'categories', arrayNew('BookId', 'ChapterId', 'Chapter Title'), \
    'measures', arrayNew( \
        objectNew('name', 'Hikes', 'field', 'HikeId', 'function', 'count') \
    ) \
))

# Add the chapter calculated fields
dataCalculatedField(dataChapters, 'Chapter', "bookLink([Chapter Title], BookId, ChapterId)", filterVariables)

# Render the books table
dataTable(dataBooks, objectNew( \
    'fields', arrayNew('BookId', 'Book', 'Hikes', 'Min. Rating', 'Min. Dist.', 'Max. Dist.', 'Min. Gain', 'Max. Gain'), \
    'markdown', arrayNew('Book') \
))

# Render the chapters table
dataTable(dataChapters, objectNew( \
    'categories', arrayNew('BookId', 'ChapterId'), \
    'fields', arrayNew('Chapter', 'Hikes'), \
    'markdown', arrayNew('Chapter') \
))

# Render the hikes table
dataTable(data, objectNew( \
    'fields', arrayNew( \
        'BookId', \
        'ChapterId', \
        'HikeId', \
        'Hike Title', \
        'Rating', \
        'Difficulty', \
        'Distance (mi)', \
        'Elevation Gain (ft)', \
        'High Point (ft)', \
        'Season' \
    ) \
))
~~~
