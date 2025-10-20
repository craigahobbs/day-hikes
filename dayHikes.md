~~~ markdown-script
# Licensed under the MIT License
# https://github.com/craigahobbs/day-hikes/blob/main/LICENSE

include <args.bare>
include <pager.bare>


async function dayHikesMain():
    pagerModel = { \
        'pages': [ \
            {'name': 'Home', 'type': {'markdown': { \
                'url': 'README.md' \
            }}}, \
            {'name': 'Books', 'type': {'function': { \
                'function': dayHikesBooks, \
                'title': 'Day Hikes Books' \
            }}}, \
            {'name': 'Hikes', 'type': {'function': { \
                'function': dayHikesHikes, \
                'title': 'Day Hikes' \
            }}}, \
            {'name': 'Correlation', 'type': {'function': { \
                'function': dayHikesCorrelation, \
                'title': 'Hike Data Correlation' \
            }}} \
        ] \
    }
    pagerMain(pagerModel, {'arguments': dayHikesArguments, 'start': 'Books', 'hideNav': true})
endfunction


# The Day Hikes application arguments
dayHikesArguments = argsValidate([ \
    {'name': 'page', 'default': 'Books'}, \
    {'name': 'bookId', 'type': 'int'}, \
    {'name': 'chapterId', 'type': 'int'}, \
    {'name': 'ratingMin', 'type': 'int'}, \
    {'name': 'distMin', 'type': 'int'}, \
    {'name': 'distMax', 'type': 'int'}, \
    {'name': 'gainMin', 'type': 'int'}, \
    {'name': 'gainMax', 'type': 'int'} \
])


# The Day Hikes Books page
async function dayHikesBooks():
    # Load the book data
    data = dataParseCSV(systemFetch('books.csv'))
    data = dataJoin(data, dataParseCSV(systemFetch('authors.csv')), 'AuthorId')
    data = dataJoin(data, dataParseCSV(systemFetch('hikes.csv')), 'BookId')

    # Add the book and ISBN link fields
    dataCalculatedField(data, 'Book', "argsLink(dayHikesArguments, [Book Title], {'page': 'Hikes', 'bookId': [BookId]}, true)")
    dataCalculatedField(data, 'ISBN', "'[' + [ISBN] + '](https://isbnsearch.org/isbn/' + [ISBN] + ')'")

    # Count the number of hikes per book
    dataBooks = dataAggregate(data, { \
        'categories': ['Book', 'Author', 'ISBN'], \
        'measures': [ \
            {'name': 'Hikes', 'field': 'HikeId', 'function': 'count'} \
        ] \
    })

    # Render the books table
    dataSort(dataBooks, [['Book']])
    dataTable(dataBooks, { \
        'fields': ['Book', 'Author', 'ISBN', 'Hikes'], \
        'formats': { \
            'Book': {'markdown': true}, \
            'ISBN': {'markdown': true} \
        } \
    })
endfunction


# The Day Hikes "Hikes" page
async function dayHikesHikes(args):
    # Render the filter links
    markdownPrint( \
        '**Rating:** ', \
        argsLink(dayHikesArguments, 'Excellent', {'ratingMin': 4}), '|', \
        argsLink(dayHikesArguments, 'Good', {'ratingMin': 3}), '  ', \
        '**Distance:** ', \
        argsLink(dayHikesArguments, 'Short', {'distMin': null, 'distMax': 5}), '|', \
        argsLink(dayHikesArguments, 'Medium', {'distMin': 5, 'distMax': 10}), '|', \
        argsLink(dayHikesArguments, 'Long', {'distMin': 10, 'distMax': null}), '  ', \
        '**Gain:** ', \
        argsLink(dayHikesArguments, 'Low', {'gainMin': null, 'gainMax': 500}), '|', \
        argsLink(dayHikesArguments, 'Moderate', {'gainMin': 500, 'gainMax': 1500}), '|', \
        argsLink(dayHikesArguments, 'High', {'gainMin': 1500, 'gainMax': null}), '  ', \
        argsLink(dayHikesArguments, 'Reset', {'page': 'Hikes'}, true) \
    )

    # Load the book data
    data = dataParseCSV(systemFetch('books.csv'))
    data = dataJoin(data, dataParseCSV(systemFetch('chapters.csv')), 'BookId')
    data = dataJoin(data, dataParseCSV(systemFetch('hikes.csv')), "BookId + '-' + ChapterId")

    # Filter & sort
    filterVariables = { \
        'curBookId': objectGet(args, 'bookId'), \
        'curChapterId': objectGet(args, 'chapterId'), \
        'ratingMin': objectGet(args, 'ratingMin'), \
        'distMin': objectGet(args, 'distMin'), \
        'distMax': objectGet(args, 'distMax'), \
        'gainMin': objectGet(args, 'gainMin'), \
        'gainMax': objectGet(args, 'gainMax') \
    }
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
    dataSort(data, [ \
        ['BookId'], \
        ['ChapterId'], \
        ['Rating', true], \
        ['Difficulty'], \
        ['Hike Title'] \
    ])

    # Compute the WTA links
    dataCalculatedField(data, 'WTA', 'dayHikesWTA([Hike Title])', {'dayHikesWTA': dayHikesWTA})

    # Count the filtered hikes by book
    dataBooks = dataAggregate(data, { \
        'categories': ['BookId', 'Book Title'], \
        'measures': [ \
            {'name': 'Hikes', 'field': 'HikeId', 'function': 'count'} \
        ] \
    })

    # Add the book calculated fields
    dataCalculatedField( \
        dataBooks, \
        'Book', \
        "argsLink(dayHikesArguments, [Book Title], {'bookId': [BookId], 'chapterId': null})", \
        filterVariables \
    )
    dataCalculatedField(dataBooks, 'Min. Rating', "if(ratingMin, ratingMin, '')", filterVariables)
    dataCalculatedField(dataBooks, 'Min. Dist.', "if(distMin, distMin, '')", filterVariables)
    dataCalculatedField(dataBooks, 'Max. Dist.', "if(distMax, distMax, '')", filterVariables)
    dataCalculatedField(dataBooks, 'Min. Gain', "if(gainMin, gainMin, '')", filterVariables)
    dataCalculatedField(dataBooks, 'Max. Gain', "if(gainMax, gainMax, '')", filterVariables)

    # Count the filtered hikes by book/chapter
    dataChapters = dataAggregate(data, { \
        'categories': ['BookId', 'ChapterId', 'Chapter Title'], \
        'measures': [ \
            {'name': 'Hikes', 'field': 'HikeId', 'function': 'count'} \
        ] \
    })

    # Add the chapter calculated fields
    dataCalculatedField( \
        dataChapters, \
        'Chapter', \
        "argsLink(dayHikesArguments, [Chapter Title], {'bookId': [BookId], 'chapterId': [ChapterId]})", \
        filterVariables \
    )

    # Render the books table
    dataTable(dataBooks, { \
        'fields': ['BookId', 'Book', 'Hikes', 'Min. Rating', 'Min. Dist.', 'Max. Dist.', 'Min. Gain', 'Max. Gain'], \
        'formats': { \
            'Book': {'markdown': true} \
        } \
    })

    # Render the chapters table
    dataTable(dataChapters, { \
        'categories': ['BookId', 'ChapterId'], \
        'fields': ['Chapter', 'Hikes'], \
        'formats': { \
            'Chapter': {'markdown': true} \
        } \
    })

    # Render the hikes table
    dataTable(data, { \
        'fields': [ \
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
        ], \
        'formats': { \
            'WTA': {'markdown': true} \
        } \
    })
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
    dataLineChart(data, { \
        'x': 'Distance (mi)', \
        'y': ['Rating'], \
        'color': 'UniqueId' \
    })

    # Draw the hike rating vs elevation gain scatter plot
    markdownPrint('', '## Hike Rating vs. Elevation Gain')
    dataLineChart(data, { \
        'x': 'Elevation Gain (ft)', \
        'y': ['Rating'], \
        'color': 'UniqueId' \
    })

    # Draw the hike rating vs elevation gain scatter plot
    markdownPrint('', '## Hike Rating vs. High Point')
    dataLineChart(data, { \
        'x': 'High Point (ft)', \
        'y': ['Rating'], \
        'color': 'UniqueId' \
    })
endfunction


dayHikesMain()
~~~
