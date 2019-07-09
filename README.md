# faithwiki
We filter Wikipedia articles to a smaller subset that relates to the Christian faith, for the purpose of Natural Language Understanding research.

## Process description

### download and data preparation
* Starting with the huge wikipedia articles archive at https://meta.wikimedia.org/wiki/Data_dump_torrents#enwiki
* choose to download the enwiki-20170820-pages-articles.xml.bz2
* run WikiParser https://dizzylogic.com/wiki-parser/ to expand the archive into XML and plain text files (with option to "skip image caption" and other default options turned on.)

### using our WikiFileReader.ipynb
* created an article reader that opens the huge plain-text-file and read one article at a time in stream format
* create function to classify if the article contains certain Christian-faith related words.
* upon consulting various Christianity keyword lists, finalize on the words: ['Jesus', 'Christ ', 'Christianity', 'God', 'salvation', 'theology']
* Form flag code: start with 1, followed by 1's and 0's to encode whether the document contains the words 'Jesus' (code=1) or not (code=0), then for 'Christ ', ...
* e.g. The code '1000101' means the file contains the words 'God', 'theology' but not 'Jesus', 'Christ ', 'Christianity', nor 'salvation'
* goes through the entire wiki plain-text-file, classify each article, so that we can collect statistics on the article distributions.
* based on the statistics, decide to filter out articles with codes '1000000' (totally without any faith words), '1000100' (containing only 'God' but not the other five). What remains are potential faith related articles that contains at least one of the words 'Jesus', 'Christ ', 'Christianity', 'salvation', 'theology'
* the result is 2% of the original wiki articles
* we compress the resulting text file to a 300MB file.

### resulting files
* wiki_articles_christian2.zip - 300MB too large for github, hence:
 [GoogleDrive shared link](https://drive.google.com/file/d/1gyLNp1q5AbTdUatOrPgNyynln4hql3-a/view?usp=sharing)  or [IceDrive shared link](https://icedrive.net/0/8fGUHufg4S) 
* above file format is still the same as the WikiParser output format, and thus can be read with our WikiFileReader
* wiki_articles_christian2_tail.txt : the last 50 lines of the 300MB zip file, can also be accessed by WikiFileReader for debugging
* wiki_titles_christian2_code.txt : each line represents the title of an article in the 300MB file, preceeded by the article flagcode. The number of lines in this file should match the number of articles in the 300MB zip file.
