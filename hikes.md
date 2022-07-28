[Home](#url=README.md) |
[Books](#url=books.md) |
[Correlation](#url=correlation.md)


# Hikes

~~~ markdown-script
# Hike filter links
markdownPrint( \
    '**Rating:** ', \
    '[Excellent](#url=hikes.md' + \
        if(vBookId, '&var.vBookId=' + vBookId) + \
        if(vChapterId, '&var.vChapterId=' + vChapterId, '') + \
        '&var.vRatingMin=4' + \
        if(vDistMin, '&var.vDistMin=' + vDistMin, '') + \
        if(vDistMax, '&var.vDistMax=' + vDistMax, '') + \
        if(vGainMin, '&var.vGainMin=' + vGainMin, '') + \
        if(vGainMax, '&var.vGainMax=' + vGainMax, '') + ')', \
    '|', \
    '[Good](#url=hikes.md' + \
        if(vBookId, '&var.vBookId=' + vBookId) + \
        if(vChapterId, '&var.vChapterId=' + vChapterId, '') + \
        '&var.vRatingMin=3' + \
        if(vDistMin, '&var.vDistMin=' + vDistMin, '') + \
        if(vDistMax, '&var.vDistMax=' + vDistMax, '') + \
        if(vGainMin, '&var.vGainMin=' + vGainMin, '') + \
        if(vGainMax, '&var.vGainMax=' + vGainMax, '') + ')  ', \
    '**Distance:** ', \
    '[Short](#url=hikes.md' + \
        if(vBookId, '&var.vBookId=' + vBookId) + \
        if(vChapterId, '&var.vChapterId=' + vChapterId, '') + \
        if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + \
        '&var.vDistMax=5' + \
        if(vGainMin, '&var.vGainMin=' + vGainMin, '') + \
        if(vGainMax, '&var.vGainMax=' + vGainMax, '') + ')', \
    '|', \
    '[Medium](#url=hikes.md' + \
        if(vBookId, '&var.vBookId=' + vBookId) + \
        if(vChapterId, '&var.vChapterId=' + vChapterId, '') + \
        if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + \
        '&var.vDistMin=5&var.vDistMax=10' + \
        if(vGainMin, '&var.vGainMin=' + vGainMin, '') + \
        if(vGainMax, '&var.vGainMax=' + vGainMax, '') + ')', \
    '|', \
    '[Long](#url=hikes.md' + \
        if(vBookId, '&var.vBookId=' + vBookId) + \
        if(vChapterId, '&var.vChapterId=' + vChapterId, '') + \
        if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + \
        '&var.vDistMin=10' + \
        if(vGainMin, '&var.vGainMin=' + vGainMin, '') + \
        if(vGainMax, '&var.vGainMax=' + vGainMax, '') + ')  ', \
    '**Gain:** ', \
    '[Low](#url=hikes.md' + \
        if(vBookId, '&var.vBookId=' + vBookId) + \
        if(vChapterId, '&var.vChapterId=' + vChapterId, '') + \
        if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + \
        if(vDistMin, '&var.vDistMin=' + vDistMin, '') + \
        if(vDistMax, '&var.vDistMax=' + vDistMax, '') + \
       '&var.vGainMax=500)', \
    '|', \
    '[Moderate](#url=hikes.md' + \
        if(vBookId, '&var.vBookId=' + vBookId) + \
        if(vChapterId, '&var.vChapterId=' + vChapterId, '') + \
        if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + \
        if(vDistMin, '&var.vDistMin=' + vDistMin, '') + \
        if(vDistMax, '&var.vDistMax=' + vDistMax, '') + \
       '&var.vGainMin=500&var.vGainMax=1500)', \
    '|', \
    '[High](#url=hikes.md' + \
        if(vBookId, '&var.vBookId=' + vBookId) + \
        if(vChapterId, '&var.vChapterId=' + vChapterId, '') + \
        if(vRatingMin, '&var.vRatingMin=' + vRatingMin, '') + \
        if(vDistMin, '&var.vDistMin=' + vDistMin, '') + \
        if(vDistMax, '&var.vDistMax=' + vDistMax, '') + \
       '&var.vGainMin=1500)' \
)
~~~

~~~ data-table
# Hike filter argument report

data.url: books.csv
data.join.0.url: chapters.csv
data.join.0.left: [BookId]
data.join.1.url: hikes.csv
data.join.1.left: [BookId] + '-' + [ChapterId]

calc.0.name: Book
calc.0.expr: '[' + markdownEscape([Book Title]) + '](#url=hikes.md&var.vBookId=' + [BookId] + ')'
calc.1.name: Min. Rating
calc.1.expr: if(vRatingMin, vRatingMin, '')
calc.2.name: Min. Dist.
calc.2.expr: if(vDistMin, vDistMin, '')
calc.3.name: Max. Dist.
calc.3.expr: if(vDistMax, vDistMax, '')
calc.4.name: Min. Gain
calc.4.expr: if(vGainMin, vGainMin, '')
calc.5.name: Max. Gain
calc.5.expr: if(vGainMax, vGainMax, '')

filter: (vBookId == null || BookId == vBookId) && \
    (vChapterId == null || ChapterId == vChapterId) && \
    (vRatingMin == null || Rating >= vRatingMin) && \
    (vDistMin == null || [Distance (mi)] >= vDistMin) && \
    (vDistMax == null || [Distance (mi)] <= vDistMax) && \
    (vGainMin == null || [Elevation Gain (ft)] >= vGainMin) && \
    (vGainMax == null || [Elevation Gain (ft)] <= vGainMax)

agg.category.0: BookId
agg.category.1: Book
agg.category.2: Min. Rating
agg.category.3: Min. Dist.
agg.category.4: Max. Dist.
agg.category.5: Min. Gain
agg.category.6: Max. Gain
agg.measure.0.name: Hikes
agg.measure.0.field: HikeId
agg.measure.0.func: Count

sort.0.field: BookId

field.0: BookId
field.1: Book
field.2: Hikes
field.3: Min. Rating
field.4: Min. Dist.
field.5: Max. Dist.
field.6: Min. Gain
field.7: Max. Gain

markdown.0: Book
~~~

~~~ data-table
# Chapters table

data.url: books.csv
data.join.0.url: chapters.csv
data.join.0.left: [BookId]
data.join.1.url: hikes.csv
data.join.1.left: [BookId] + '-' + [ChapterId]

calc.0.name: Chapter
calc.0.expr: '[' + markdownEscape([Chapter Title]) + '](#url=hikes.md&var.vBookId=' + [BookId] + '&var.vChapterId=' + [ChapterId] + \
    if(vRatingMin != null, '&var.vRatingMin=' + vRatingMin, '') + \
    if(vDistMin != null, '&var.vDistMin=' + vDistMin, '') + \
    if(vDistMax != null, '&var.vDistMax=' + vDistMax, '') + \
    if(vGainMin != null, '&var.vGainMin=' + vGainMin, '') + \
    if(vGainMax != null, '&var.vGainMax=' + vGainMax, '') + ')'

filter: (vBookId == null || BookId == vBookId) && \
    (vChapterId == null || ChapterId == vChapterId) && \
    (vRatingMin == null || Rating >= vRatingMin) && \
    (vDistMin == null || [Distance (mi)] >= vDistMin) && \
    (vDistMax == null || [Distance (mi)] <= vDistMax) && \
    (vGainMin == null || [Elevation Gain (ft)] >= vGainMin) && \
    (vGainMax == null || [Elevation Gain (ft)] <= vGainMax)

agg.category.0: BookId
agg.category.1: ChapterId
agg.category.2: Chapter
agg.measure.0.name: Hikes
agg.measure.0.field: HikeId
agg.measure.0.func: Count

sort.0.field: BookId
sort.1.field: ChapterId

category.0: BookId
category.1: ChapterId
field.0: Chapter
field.1: Hikes

markdown.0: Chapter
~~~

~~~ data-table
# Hikes table

data.url: books.csv
data.join.0.url: chapters.csv
data.join.0.left: [BookId]
data.join.1.url: hikes.csv
data.join.1.left: [BookId] + '-' + [ChapterId]

filter: (vBookId == null || BookId == vBookId) && \
    (vChapterId == null || ChapterId == vChapterId) && \
    (vRatingMin == null || Rating >= vRatingMin) && \
    (vDistMin == null || [Distance (mi)] >= vDistMin) && \
    (vDistMax == null || [Distance (mi)] <= vDistMax) && \
    (vGainMin == null || [Elevation Gain (ft)] >= vGainMin) && \
    (vGainMax == null || [Elevation Gain (ft)] <= vGainMax)

sort.0.field: Rating
sort.0.desc: true
sort.1.field: Difficulty
sort.2.field: Hike Title

field.0: BookId
field.1: ChapterId
field.2: HikeId
field.3: Hike Title
field.4: Rating
field.5: Difficulty
field.6: Distance (mi)
field.7: Elevation Gain (ft)
field.8: High Point (ft)
field.9: Season
~~~
