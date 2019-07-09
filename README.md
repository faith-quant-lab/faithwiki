# faithwiki
Wikipedia articles related to Christian faith for NLU research

## Process description

### download and data preparation
* Starting with the huge wikipedia articles archive at https://meta.wikimedia.org/wiki/Data_dump_torrents#enwiki
* choose to download the enwiki-20170820-pages-articles.xml.bz2
* run WikiParser https://dizzylogic.com/wiki-parser/ to expand the archive into XML and plain text files (with option to "skip image caption" and other default options turned on.)

### using our WikiFileReader.ipynb
* created an article reader that opens the huge plain-text-file and read one article at a time in stream format
* create function to classify if the article contains the words ['Jesus', 'Christ ', 'Christianity', 'God', 'salvation', 'theology']
* The flag code starts with 1, then followed by whether the document contains 'Jesus' (code=1) or not (code=0), then for 'Christ ', ...
* e.g. The code '1000101' means the file contains the words 'God', 'theology' but not 'Jesus', 'Christ ', 'Christianity', nor 'salvation'
* goes through the entire wiki plain-text-file, classify each article, so that we can collect statistics on the article distributions.
* based on the statistics, decide to filter articles with codes '1000000', '1000100', leaving potentially faith related articles that contains at least one of the words 'Jesus', 'Christ ', 'Christianity', 'salvation', 'theology'
* the result is 2% of the wiki articles, saved first as text, and then compressed to a 300MB file.
