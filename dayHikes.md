~~~ markdown-script
# Licensed under the MIT License
# https://github.com/craigahobbs/day-hikes/blob/main/LICENSE

include <args.bare>
include <pager.bare>


async function dayHikesMain():
    pagerModel = objectNew( \
        'pages', arrayNew( \
            objectNew('name', 'Home', 'type', objectNew('markdown', objectNew( \
                'url', 'README.md' \
            ))), \
            objectNew('name', 'Books', 'type', objectNew('function', objectNew( \
                'function', dayHikesBooks, \
                'title', 'Day Hikes Books' \
            ))), \
            objectNew('name', 'Hikes', 'type', objectNew('function', objectNew( \
                'function', dayHikesHikes, \
                'title', 'Day Hikes' \
            ))), \
            objectNew('name', 'Correlation', 'type', objectNew('function', objectNew( \
                'function', dayHikesCorrelation, \
                'title', 'Hike Data Correlation' \
            ))) \
        ) \
    )
    pagerMain(pagerModel, objectNew('arguments', dayHikesArguments, 'start', 'Books', 'hideNav', true))
endfunction


# The Day Hikes application arguments
dayHikesArguments = argsValidate(arrayNew( \
    objectNew('name', 'page', 'default', 'Books'), \
    objectNew('name', 'bookId', 'type', 'int'), \
    objectNew('name', 'chapterId', 'type', 'int'), \
    objectNew('name', 'ratingMin', 'type', 'int'), \
    objectNew('name', 'distMin', 'type', 'int'), \
    objectNew('name', 'distMax', 'type', 'int'), \
    objectNew('name', 'gainMin', 'type', 'int'), \
    objectNew('name', 'gainMax', 'type', 'int') \
))


# The Day Hikes Books page
async function dayHikesBooks():
    # Load the book data
    data = dataParseCSV(systemFetch('books.csv'))
    data = dataJoin(data, dataParseCSV(systemFetch('authors.csv')), 'AuthorId')
    data = dataJoin(data, dataParseCSV(systemFetch('hikes.csv')), 'BookId')

    # Add the book and ISBN link fields
    dataCalculatedField(data, 'Book', "argsLink(dayHikesArguments, [Book Title], objectNew('page', 'Hikes', 'bookId', [BookId]), true)")
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
        'formats', objectNew( \
            'Book', objectNew('markdown', true), \
            'ISBN', objectNew('markdown', true) \
        ) \
    ))
endfunction


# The Day Hikes "Hikes" page
async function dayHikesHikes(args):
    # Render the filter links
    markdownPrint( \
        '**Rating:** ', \
        argsLink(dayHikesArguments, 'Excellent', objectNew('ratingMin', 4)), '|', \
        argsLink(dayHikesArguments, 'Good', objectNew('ratingMin', 3)), '  ', \
        '**Distance:** ', \
        argsLink(dayHikesArguments, 'Short', objectNew('distMin', null, 'distMax', 5)), '|', \
        argsLink(dayHikesArguments, 'Medium', objectNew('distMin', 5, 'distMax', 10)), '|', \
        argsLink(dayHikesArguments, 'Long', objectNew('distMin', 10, 'distMax', null)), '  ', \
        '**Gain:** ', \
        argsLink(dayHikesArguments, 'Low', objectNew('gainMin', null, 'gainMax', 500)), '|', \
        argsLink(dayHikesArguments, 'Moderate', objectNew('gainMin', 500, 'gainMax', 1500)), '|', \
        argsLink(dayHikesArguments, 'High', objectNew('gainMin', 1500, 'gainMax', null)), '  ', \
        argsLink(dayHikesArguments, 'Reset', objectNew('page', 'Hikes'), true) \
    )

    # Load the book data
    data = dataParseCSV(systemFetch('books.csv'))
    data = dataJoin(data, dataParseCSV(systemFetch('chapters.csv')), 'BookId')
    data = dataJoin(data, dataParseCSV(systemFetch('hikes.csv')), "BookId + '-' + ChapterId")

    # Filter & sort
    filterVariables = objectNew( \
        'curBookId', objectGet(args, 'bookId'), \
        'curChapterId', objectGet(args, 'chapterId'), \
        'ratingMin', objectGet(args, 'ratingMin'), \
        'distMin', objectGet(args, 'distMin'), \
        'distMax', objectGet(args, 'distMax'), \
        'gainMin', objectGet(args, 'gainMin'), \
        'gainMax', objectGet(args, 'gainMax') \
    )
    data = dataFilter( \
        data, \
        '(curBookId == null || BookId == curBookId) && ' + \
            '(curChapterId == null || ChapterId == curChapterId) && ' + \
            '(ratingMin == null || Rating >= ratingMin) && ' + \
            '(distMin == null || [Distance (mi)] >= distMin) && ' + \
            '(distMax == null || [Distance (mi)] <= distMax) && ' + \
            '(gainMin == null || [Elevation Gain (ft)] >= gainMin) && ' + \
            '(gainMax == null || [Elevation Gain (ft)] <= gainMax)', \
        filterVariables \
    )
    dataSort(data, arrayNew( \
        arrayNew('BookId'), \
        arrayNew('ChapterId'), \
        arrayNew('Rating', true), \
        arrayNew('Difficulty'), \
        arrayNew('Hike Title') \
    ))

    # Compute the WTA links
    dataCalculatedField(data, 'WTA', 'dayHikesWTA([Hike Title])', objectNew('dayHikesWTA', dayHikesWTA))

    # Count the filtered hikes by book
    dataBooks = dataAggregate(data, objectNew( \
        'categories', arrayNew('BookId', 'Book Title'), \
        'measures', arrayNew( \
            objectNew('name', 'Hikes', 'field', 'HikeId', 'function', 'count') \
        ) \
    ))

    # Add the book calculated fields
    dataCalculatedField( \
        dataBooks, \
        'Book', \
        "argsLink(dayHikesArguments, [Book Title], objectNew('bookId', [BookId], 'chapterId', null))", \
        filterVariables \
    )
    dataCalculatedField(dataBooks, 'Min. Rating', "if(ratingMin, ratingMin, '')", filterVariables)
    dataCalculatedField(dataBooks, 'Min. Dist.', "if(distMin, distMin, '')", filterVariables)
    dataCalculatedField(dataBooks, 'Max. Dist.', "if(distMax, distMax, '')", filterVariables)
    dataCalculatedField(dataBooks, 'Min. Gain', "if(gainMin, gainMin, '')", filterVariables)
    dataCalculatedField(dataBooks, 'Max. Gain', "if(gainMax, gainMax, '')", filterVariables)

    # Count the filtered hikes by book/chapter
    dataChapters = dataAggregate(data, objectNew( \
        'categories', arrayNew('BookId', 'ChapterId', 'Chapter Title'), \
        'measures', arrayNew( \
            objectNew('name', 'Hikes', 'field', 'HikeId', 'function', 'count') \
        ) \
    ))

    # Add the chapter calculated fields
    dataCalculatedField( \
        dataChapters, \
        'Chapter', \
        "argsLink(dayHikesArguments, [Chapter Title], objectNew('bookId', [BookId], 'chapterId', [ChapterId]))", \
        filterVariables \
    )

    # Render the books table
    dataTable(dataBooks, objectNew( \
        'fields', arrayNew('BookId', 'Book', 'Hikes', 'Min. Rating', 'Min. Dist.', 'Max. Dist.', 'Min. Gain', 'Max. Gain'), \
        'formats', objectNew( \
            'Book', objectNew('markdown', true) \
        ) \
    ))

    # Render the chapters table
    dataTable(dataChapters, objectNew( \
        'categories', arrayNew('BookId', 'ChapterId'), \
        'fields', arrayNew('Chapter', 'Hikes'), \
        'formats', objectNew( \
            'Chapter', objectNew('markdown', true) \
        ) \
    ))

    # Render the hikes table
    dataTable(data, objectNew( \
        'fields', arrayNew( \
            'BookId', \
            'ChapterId', \
            'HikeId', \
            'Hike Title', \
            'WTA', \
            'Rating', \
            'Difficulty', \
            'Distance (mi)', \
            'Elevation Gain (ft)', \
            'High Point (ft)', \
            'Season' \
        ), \
        'formats', objectNew( \
            'WTA', objectNew('markdown', true) \
        ) \
    ))
endfunction


function dayHikesWTA(hikeTitle):
    wta = stringLower(hikeTitle)
    wta = regexReplace(dayHikesWTARegexStart, wta, '')
    wta = regexReplace(dayHikesWTARegexEnd, wta, '')
    wta = regexReplace(dayHikesWTARegexBlank, wta, '')
    wta = regexReplace(dayHikesWTARegexDash, wta, '-')
    return '[WTA](https://www.wta.org/go-hiking/hikes/' + urlEncodeComponent(wta) + ')'
endfunction


dayHikesWTARegexStart = regexNew('^[^A-Za-z0-9]+')
dayHikesWTARegexEnd = regexNew('[^A-Za-z0-9]+$')
dayHikesWTARegexBlank = regexNew("[']+")
dayHikesWTARegexDash = regexNew('[^A-Za-z0-9]+')


# The Day Hikes Correlation page
async function dayHikesCorrelation():
    # Load the book data
    data = dataParseCSV(systemFetch('books.csv'))
    data = dataJoin(data, dataParseCSV(systemFetch('chapters.csv')), 'BookId')
    data = dataJoin(data, dataParseCSV(systemFetch('hikes.csv')), "[BookId] + '-' + [ChapterId]")

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
endfunction


dayHikesMain()
~~~
