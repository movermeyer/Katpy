## Katpy

[![Code Health](https://landscape.io/github/s4chin/Katpy/master/landscape.svg?style=flat)](https://landscape.io/github/s4chin/Katpy/master)
[![Latest Version](https://img.shields.io/pypi/v/katpy.svg)](https://pypi.python.org/pypi/katpy/)
[![Downloads](https://img.shields.io/pypi/dm/katpy.svg)](https://pypi.python.org/pypi/katpy/)

An unofficial Python API for [KickAssTorrents](http://kickass.to/)

### Installation
```
pip install katpy
```
Or:
(https://pypi.python.org/pypi/katpy/1.0.0)
Download and un-pack.
```
python setup.py install
```

### Usage
Perform searches using kat.popular(), kat.search() and kat.recent()
Results returned are iterable and can be accessed individually to
see individual torrent information.
```python
import kat

# Get home page results. ------------------------------------------------

home = kat.popular()

# See information about first result 
print home[0].title # Some torrent title

# Or print out details of every torrent returned

for torrent in home:
  torrent.print_details()

# By default kat.popular returns 70 results, 10 for each category.
# We can refine our results by using categories.

home_games = kat.popular(category=kat.Categories.GAMES)

# We can see how many results we got
print len(home) # 70
print len(home_games) # 10


# ----------------------------------------------------------------------


# Perform a search -----------------------------------------------------

s = kat.search("the walking dead")

# Searches can be categorized and also sorted.
s = kat.search("the walking dead", category=kat.Categories.TV, 
                sort=kat.Sorting.SEED, order=kat.Sorting.Order.DESC)

# They can also span multiple pages
multi = kat.search("the walking dead", pages=3)
# And we can keep track of the current page
print multi.current_page # 3

# We can go to a particular page
multi.page(7)

# And to the next page
multi.next_page()


#-----------------------------------------------------------------------

# Get recently added torrents ------------------------------------------

r = kat.recent()

# Recent results can be categorized and sorted like normal searches
# and can also contain multiple pages.

# Change base url
kat.set_base_url("http://kickmirror.com")

```
### Sorting and Categories
#### Sort Options
* Sorting.SIZE
* Sorting.AGE
* Sorting.FILES
* Sorging.SEED
* Sorting.LEECH
* Sorting.Order.ASC
* Sorting.Order.DESC

#### Category Options
* Categories.ALL
* Categories.MOVIES
* Categories.TV
* Categories.ANIME
* Categories.MUSIC
* Categories.BOOKS
* Categories.APPS
* Categories.GAMES
* Categories.XXX

### Torrent Information Available
* title
* category
* size
* seeders
* leechers
* magnet
* download
* files
* age
* page
* print_details()

### TODO
* Implement sorting for kat.popular() 
* Trying to get a page after the end of the results returns the first page, I want to make it return nothing.
* Create a filter class to group sort & search options.
* Implement sub-categories.
* ~~Add support for searching mirror sites e.g kickmirror.com~~