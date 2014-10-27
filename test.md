# TOC
   - [cms](#cms)
     - [site](#cms-site)
       - [#pages](#cms-site-pages)
       - [#yourvar](#cms-site-yourvar)
       - [#activePage](#cms-site-activepage)
       - [#page(uri)](#cms-site-pageuri)
     - [pages](#cms-pages)
       - [#size()](#cms-pages-size)
       - [#first()](#cms-pages-first)
       - [#last()](#cms-pages-last)
       - [#where('isVisible')](#cms-pages-whereisvisible)
       - [#reject('isVisible')](#cms-pages-rejectisvisible)
       - [#find({dirname:'01-products'})](#cms-pages-finddirname01-products)
       - [#find({uid:'products'})](#cms-pages-finduidproducts)
       - [#reject({uid:'ps4'})](#cms-pages-rejectuidps4)
       - [#find({title:'Electronics Products'})](#cms-pages-findtitleelectronics-products)
       - [#find('isOpen')](#cms-pages-findisopen)
       - [#where({brand:'Apple'})](#cms-pages-wherebrandapple)
       - [#slice(0, limit)](#cms-pages-slice0-limit)
       - [#slice(offset)](#cms-pages-sliceoffset)
       - [#slice(offset, offset + limit)](#cms-pages-sliceoffset-offset--limit)
       - [#slice().reverse()](#cms-pages-slicereverse)
       - [#shuffle()](#cms-pages-shuffle)
       - [#sortBy('title')](#cms-pages-sortbytitle)
       - [#sortBy('title').reverse()](#cms-pages-sortbytitlereverse)
     - [page](#cms-page)
       - [#title](#cms-page-title)
         - [When the title exists](#cms-page-title-when-the-title-exists)
         - [When the title doesn't exist](#cms-page-title-when-the-title-doesnt-exist)
       - [#yourvar](#cms-page-yourvar)
       - [#uri](#cms-page-uri)
       - [#page(uri)](#cms-page-pageuri)
       - [#parent](#cms-page-parent)
       - [#siblings](#cms-page-siblings)
       - [#template](#cms-page-template)
       - [#next](#cms-page-next)
       - [#prev](#cms-page-prev)
       - [#nextVisible](#cms-page-nextvisible)
       - [#prevVisible](#cms-page-prevvisible)
       - [isHomePage](#cms-page-ishomepage)
       - [#isActive](#cms-page-isactive)
       - [#isChildOf(page)](#cms-page-ischildofpage)
       - [#isDescendantdOf(page)](#cms-page-isdescendantdofpage)
       - [#isAncestorOf(page)](#cms-page-isancestorofpage)
       - [#isDescendantdOf(site.activePage)](#cms-page-isdescendantdofsiteactivepage)
       - [#isOpen](#cms-page-isopen)
       - [#files](#cms-page-files)
       - [if(page.files.size() > 0)](#cms-page-ifpagefilessize--0)
       - [#images](#cms-page-images)
       - [if(page.images.size() > 0)](#cms-page-ifpageimagessize--0)
       - [#videos](#cms-page-videos)
       - [#documents](#cms-page-documents)
       - [#sounds](#cms-page-sounds)
     - [files](#cms-files)
       - [#size()](#cms-files-size)
       - [#find({filename:'doc2.xls'})](#cms-files-findfilenamedoc2xls)
       - [#yourvar](#cms-files-yourvar)
       - [#where({author: 'Chakib Ouhajjou'})](#cms-files-whereauthor-chakib-ouhajjou)
     - [#file](#cms-file)
       - [#filename](#cms-file-filename)
       - [#name](#cms-file-name)
       - [#extension](#cms-file-extension)
       - [#uri](#cms-file-uri)
       - [#type](#cms-file-type)
       - [#next](#cms-file-next)
       - [#prev](#cms-file-prev)
<a name=""></a>
 
<a name="cms"></a>
# cms
<a name="cms-site"></a>
## site
Root of all content.

```js

```

<a name="cms-site-pages"></a>
### #pages
Pages at the root of the site, this is a lodash array. Check https://lodash.com/docs.

```js
var pages = site.pages;
//=>
pages.should.exist;
```

<a name="cms-site-yourvar"></a>
### #yourvar
A variable of the site defined in site.txt.

```js
var title = site.title;
var author = site.author;
//=>
title.should.equal("This the title");
author.should.equal("Cloudscale SARL");
```

<a name="cms-site-activepage"></a>
### #activePage
Returns the currently active page.

```js
site._activePage = site.page("products/iphone");
var page = site.activePage;
//=>
page.should.equal(site.page("products/iphone"));
```

<a name="cms-site-pageuri"></a>
### #page(uri)
Finds the page with uri, or nothing if not found. A uri has the format projects/project-1/subpage.

```js
var nonExistingPage = site.page("non/existing");
var accessoriesPage = site.page("products/ps4/accessories");
//=>
should.not.exist(nonExistingPage);
accessoriesPage.dirname.should.equal("accessories");
```

<a name="cms-pages"></a>
## pages
A list of pages, can be root site pages (site.pages) or children pages of a page (anyPage.pages) this is a  lodash array. Check https://lodash.com/docs for additionnal information on how to use lodash..

```js

```

<a name="cms-pages-size"></a>
### #size()
Number of pages.

```js
var n = site.pages.size();
//=>
n.should.equal(3);
```

<a name="cms-pages-first"></a>
### #first()
First page.

```js
var first = site.pages.first();
//=>
first.dirname.should.equal("01-products");
```

<a name="cms-pages-last"></a>
### #last()
Last page.

```js
var last = site.pages.last();
//=>
last.dirname.should.equal("categories");
```

<a name="cms-pages-whereisvisible"></a>
### #where('isVisible')
Visible pages.

```js
var visiblePages = site.pages.where("isVisible");
//=>
visiblePages.size().should.equal(2);
```

<a name="cms-pages-rejectisvisible"></a>
### #reject('isVisible')
Invisible pages.

```js
var invisiblePages = site.pages.reject("isVisible");
//=>
invisiblePages.size().should.equal(1);
```

<a name="cms-pages-finddirname01-products"></a>
### #find({dirname:'01-products'})
Find a page by it's directory name.

```js
var products = site.pages.find({ dirname: "01-products" });
//=>
products.dirname.should.equal("01-products");
```

<a name="cms-pages-finduidproducts"></a>
### #find({uid:'products'})
Find a page by it's uid.

```js
var products = site.pages.find({ uid: "products" });
//=>
products.uid.should.equal("products")
```

<a name="cms-pages-rejectuidps4"></a>
### #reject({uid:'ps4'})
Return all the pages expect the one with uid.

```js
var allSubPagesExceptPs4 = site.pages.find({ dirname: "01-products" }).pages.reject({ uid: "ps4" });
//=>
allSubPagesExceptPs4.size().should.equal(2);
```

<a name="cms-pages-findtitleelectronics-products"></a>
### #find({title:'Electronics Products'})
Find the page by it's title.

```js
var electronics = site.pages.find({ title: "Electronics Products" });
//=>
electronics.title.should.equal("Electronics Products");
```

<a name="cms-pages-findisopen"></a>
### #find('isOpen')
Return the open page in a list of pages.

```js
site._activePage = site.page("products/ps4/accessories");
var ps4 = site.page("products").pages.find("isOpen");
var notFound = site.page("categories").pages.find("isOpen");
//=>
ps4.dirname.should.equal("02-ps4");
should.not.exist(notFound);
```

<a name="cms-pages-wherebrandapple"></a>
### #where({brand:'Apple'})
Filter the pages by key and value.

```js
var appleProducts = site.pages.find({ dirname: "01-products" }).pages.where({ brand: "Apple" });
//=>
appleProducts.size().should.equal(1);
```

<a name="cms-pages-slice0-limit"></a>
### #slice(0, limit)
Return a limited number of pages.

```js
var twoPages = site.pages.find({ dirname: "01-products" }).pages.slice(0, 2);
//=>
twoPages.size().should.equal(2);
```

<a name="cms-pages-sliceoffset"></a>
### #slice(offset)
Return pages starting from an offset.

```js
var onePage = site.pages.find({ dirname: "01-products" }).pages.slice(2);
//=>
onePage.size().should.equal(1);
```

<a name="cms-pages-sliceoffset-offset--limit"></a>
### #slice(offset, offset + limit)
Return pages starting from an offset, and limited to a limit.

```js
var twoPages = site.pages.find({ dirname: "01-products" }).pages.slice(1, 1 + 2);
//=>
twoPages.size().should.equal(2);
twoPages.first().title.should.equal("Playstation 4");
```

<a name="cms-pages-slicereverse"></a>
### #slice().reverse()
Return pages in reverse order.

```js
var products = site.pages.find({ dirname: "01-products" }).pages;
var reversedProducts = products.slice().reverse();
//=>
reversedProducts.size().should.equal(3);
reversedProducts.first().dirname.should.equal(products.last().dirname);
reversedProducts.last().dirname.should.equal(products.first().dirname);
```

<a name="cms-pages-shuffle"></a>
### #shuffle()
Shuffle the order of pages.

```js
var shuffledProducts = site.pages.find({ dirname: "01-products" }).pages.shuffle();
//=>
shuffledProducts.size().should.equal(3);
```

<a name="cms-pages-sortbytitle"></a>
### #sortBy('title')
Sort pages by key in ascending order.

```js
var products = site.pages.find({ dirname: "01-products" });
var sortedProducts = products.pages.sortBy("title");
sortedProducts.size().should.equal(3);
//=>
sortedProducts.first().title.should.equal("Asus U7");
sortedProducts.last().title.should.equal("Playstation 4");
```

<a name="cms-pages-sortbytitlereverse"></a>
### #sortBy('title').reverse()
Sort pages by key in descending order.

```js
var products = site.pages.find({ dirname: "01-products" });
var sortedProducts = products.pages.sortBy("title").reverse();
//=>
sortedProducts.size().should.equal(3);
sortedProducts.first().title.should.equal("Playstation 4");
sortedProducts.last().title.should.equal("Asus U7");
```

<a name="cms-page"></a>
## page
Currently active page.

```js

```

<a name="cms-page-title"></a>
### #title
<a name="cms-page-title-when-the-title-exists"></a>
#### When the title exists
Return the page title.

```js
var title = site.page("products").title;
//=>
title.should.equal("Electronics Products");
```

<a name="cms-page-title-when-the-title-doesnt-exist"></a>
#### When the title doesn't exist
Return the uid of the page.

```js
var title = site.page("categories").title;
//=>
title.should.equal("categories");
```

<a name="cms-page-yourvar"></a>
### #yourvar
Return the field yourvar of the page.

```js
var header = site.page("categories").header;
//=>
header.should.equal("This is a header");
```

<a name="cms-page-uri"></a>
### #uri
Return the full uri of the page (doesn't include the root path).

```js
var uri = site.page("products/ps4/accessories").uri;
//=>
uri.should.equal("products/ps4/accessories");
```

<a name="cms-page-pageuri"></a>
### #page(uri)
Return the descendant page having the uri. A uri has the format projects/project-1/subpage.

```js
var accessories = site.page("products").page("ps4/accessories");
var nonExistant = site.page("products").page("non/existing");
//=>
accessories.dirname.should.equal("accessories");
should.not.exist(nonExistant);
```

<a name="cms-page-parent"></a>
### #parent
Return the parent page, at the root parent is the site node.

```js
var parentPage = site.page("products/ps4/accessories").parent;
var grandParentPage = parentPage.parent;
var root = grandParentPage.parent;
//=>
parentPage.uri.should.equal("products/ps4");
grandParentPage.uri.should.equal("products");
root.should.equal(site);
```

<a name="cms-page-siblings"></a>
### #siblings
Return all siblings of a page.

```js
var siblings = site.page("products").siblings;
//=>
siblings.size().should.equal(2);
siblings.first().dirname.should.equal("02-newsletter");
siblings.valueOf()[1].dirname.should.equal("categories");
```

<a name="cms-page-template"></a>
### #template
Name of the template used to render the page.

```js
var template = site.page("products").template;
//=>
template.should.equal("default");
```

<a name="cms-page-next"></a>
### #next
Return the next page.

```js
var newsletter = site.page("products").next;
var categories = newsletter.next;
var notFound = categories.next;
//=>
newsletter.dirname.should.equal("02-newsletter");
categories.dirname.should.equal("categories");
should.not.exist(notFound);
```

<a name="cms-page-prev"></a>
### #prev
Return the previous page.

```js
var newsletter = site.page("categories").prev;
var products = newsletter.prev;
var notFound1 = products.prev;
//=>
newsletter.dirname.should.equal("02-newsletter");
products.dirname.should.equal("01-products");
should.not.exist(notFound1);

var ps4 = site.page("products/iphone").prev;
var notebook = ps4.prev;
var notFound2 = notebook.prev;
//=>
ps4.dirname.should.equal("02-ps4");
notebook.dirname.should.equal("01-notebook");
should.not.exist(notFound2);
```

<a name="cms-page-nextvisible"></a>
### #nextVisible
Return the next visible page.

```js
var newsletter = site.page("products").nextVisible;
var notFound1 = newsletter.nextVisible;
//=>
newsletter.dirname.should.equal("02-newsletter");
should.not.exist(notFound1);

var ps4 = site.page("products/notebook").nextVisible;
var iphone = ps4.nextVisible;
var notFound2 = iphone.nextVisible;
//=>
ps4.dirname.should.equal("02-ps4");
iphone.dirname.should.equal("03-iphone");
should.not.exist(notFound2);
```

<a name="cms-page-prevvisible"></a>
### #prevVisible
Return the previous visible page.

```js
var newsletter = site.page("categories").prevVisible;
var products = site.page("categories").prevVisible.prevVisible;
var notFound1 = site.page("categories").prevVisible.prevVisible.prevVisible;
//=>
newsletter.dirname.should.equal("02-newsletter");
products.dirname.should.equal("01-products");
should.not.exist(notFound1);

var ps4 = site.page("products/iphone").prevVisible;
var notebook = ps4.prevVisible;
var notFound2 = notebook.prevVisible;
//=>
ps4.dirname.should.equal("02-ps4");
notebook.dirname.should.equal("01-notebook");
should.not.exist(notFound1);
```

<a name="cms-page-ishomepage"></a>
### isHomePage
Checks to see if the page is the home page of the website.

```js
var val1 = site.page("products").isHomePage;
var val2 = site.page("products/ps4").isHomePage;
//=>
val1.should.be.true;
val2.should.be.false;
```

<a name="cms-page-isactive"></a>
### #isActive
Check if the page is the currently active one.

```js
site._activePage = site.page("products/iphone");
var val1 = site.page("products/iphone").isActive;
//=>
val1.should.equal(true);
```

<a name="cms-page-ischildofpage"></a>
### #isChildOf(page)
Check if this is a direct child of another page.

```js
var val1 = site.page("products/iphone/accessories").isChildOf(site.page("products/iphone"));
var val2 = site.page("products/iphone/accessories").isChildOf(site.page("products"));
//=>
val1.should.be.true;
val2.should.be.false;
```

<a name="cms-page-isdescendantdofpage"></a>
### #isDescendantdOf(page)
Check if this is a descendant of another page.

```js
var accessories= site.page("products/iphone/accessories");
var val1 = accessories.isDescendantOf(site.page("products/iphone/accessories"));
var val2 = accessories.isDescendantOf(site.page("products/iphone"));
var val3 = accessories.isDescendantOf(site.page("products"));
//=>
val1.should.be.false;
val2.should.be.true;
val3.should.be.true;
```

<a name="cms-page-isancestorofpage"></a>
### #isAncestorOf(page)
Check if this is an ancestor of another page.

```js
var accessories = site.page("products/iphone/accessories");
var val1 = accessories.isAncestorOf(accessories);
var val2 = site.page("products/iphone").isAncestorOf(accessories);
var val3 = site.page("products").isAncestorOf(accessories);
//=>
val1.should.be.false;
val2.should.be.true;
val3.should.be.true;
```

<a name="cms-page-isdescendantdofsiteactivepage"></a>
### #isDescendantdOf(site.activePage)
Check if this is a descendant of the active page.

```js
site._activePage = site.page("products/iphone");
var val1 = site.page("products/iphone").isDescendantOf(site.activePage);
var val2 = site.page("products/iphone/accessories").isDescendantOf(site.activePage);
//=>
val1.should.be.false;
val2.should.be.true;

site._activePage = site.page("products");
var val3 = site.page("products/iphone/accessories").isDescendantOf(site.activePage);
//=>
val3.should.be.true;
```

<a name="cms-page-isopen"></a>
### #isOpen
check if this is page is active or ancestor of the active page.

```js
site._activePage = site.page("products/iphone/accessories");
var val1 = site.page("products/iphone/accessories").isOpen;
var val2 = site.page("products/iphone").isOpen;
var val3 = site.page("products").isOpen;
var val4 = site.page("categories").isOpen;
//=>
val1.should.be.true;
val2.should.be.true;
val3.should.be.true;
val4.should.be.false;

site._activePage = site.page("products/iphone");
var val5 = site.page("products/iphone/accessories").isOpen;
var val6 = site.page("products/iphone").isOpen;
var val7 = site.page("products").isOpen;
//=>
val5.should.be.false;
val6.should.be.true;
val7.should.be.true;
```

<a name="cms-page-files"></a>
### #files
Return all files of the current page. This is a lodash array..

```js
var files = site.page("products/notebook").files;
//=>
files.size().should.equal(18);
```

<a name="cms-page-ifpagefilessize--0"></a>
### if(page.files.size() > 0)
Checks if the page has files.

```js
var size = site.page("products/notebook").files.size();
//=>
size.should.be.greaterThan(0);
```

<a name="cms-page-images"></a>
### #images
Return image files.

```js
var images = site.page("products/notebook").images;
//=>
images.size().should.equal(4);
```

<a name="cms-page-ifpageimagessize--0"></a>
### if(page.images.size() > 0)
checks if the page has images.

```js
var size = site.page("products/notebook").images.size();
//=>
size.should.be.greaterThan(0);
```

<a name="cms-page-videos"></a>
### #videos
Return video files.

```js
var videos = site.page("products/notebook").videos;
//=>
videos.size().should.equal(8);
```

<a name="cms-page-documents"></a>
### #documents
Return document files.

```js
var documents = site.page("products/notebook").documents;
//=>
documents.size().should.equal(4);
```

<a name="cms-page-sounds"></a>
### #sounds
Return sound files.

```js
var sounds = site.page("products/notebook").sounds;
//=>
sounds.size().should.equal(2);
```

<a name="cms-files"></a>
## files
Files of the page.

```js

```

<a name="cms-files-size"></a>
### #size()
Number of files.

```js
var size = files.size();
//=>
size.should.equal(18);
```

<a name="cms-files-findfilenamedoc2xls"></a>
### #find({filename:'doc2.xls'})
Find a file by name.

```js
var  file = files.find({ filename: "doc2.xls" });
//=>
file.filename.should.equal("doc2.xls");
```

<a name="cms-files-yourvar"></a>
### #yourvar
Return the field yourvar of the file.

```js
var author = files.find({ filename: "doc1.ppt" }).author;
//=>
author.should.equal("Chakib Ouhajjou");
```

<a name="cms-files-whereauthor-chakib-ouhajjou"></a>
### #where({author: 'Chakib Ouhajjou'})
Filter files by author.

```js
var myFiles = files.where({ author: "Chakib Ouhajjou" });
//=>
myFiles.size().should.equal(2);
```

<a name="cms-file"></a>
## #file
A file of type image, document, sound, video or sound .

```js

```

<a name="cms-file-filename"></a>
### #filename
Filename of the file.

```js
var filename = files.find({ filename: "doc2.xls" }).filename;
//=>
filename.should.equal("doc2.xls");
```

<a name="cms-file-name"></a>
### #name
Name of the file without the extension.

```js
var name = files.find({ filename: "doc2.xls" }).name;
//=>
name.should.equal("doc2");
```

<a name="cms-file-extension"></a>
### #extension
Extension of the file.

```js
var  extension = files.find({ filename: "doc2.xls" }).extension;
//=>
extension.should.equal(".xls");
```

<a name="cms-file-uri"></a>
### #uri
Uri of the file.

```js
var uri = files.find({ filename: "doc2.xls" }).uri;
//=>
uri.should.equal("products/notebook/doc2.xls");
```

<a name="cms-file-type"></a>
### #type
the type of the file: image, document, sound, video or sound.

```js
files.find({ filename: "doc1.ppt" }).type.should.equal("document");
files.find({ filename: "doc2.xls" }).type.should.equal("document");
files.find({ filename: "doc3.doc" }).type.should.equal("document");
files.find({ filename: "doc4.pdf" }).type.should.equal("document");
files.find({ filename: "image1.jpg" }).type.should.equal("image");
files.find({ filename: "image2.jpeg" }).type.should.equal("image");
files.find({ filename: "image3.gif" }).type.should.equal("image");
files.find({ filename: "image4.png" }).type.should.equal("image");
files.find({ filename: "sound1.m4a" }).type.should.equal("sound");
files.find({ filename: "sound2.mp3" }).type.should.equal("sound");
files.find({ filename: "vid1.mov" }).type.should.equal("video");
files.find({ filename: "vid2.avi" }).type.should.equal("video");
files.find({ filename: "vid3.ogg" }).type.should.equal("video");
files.find({ filename: "vid4.webm" }).type.should.equal("video");
files.find({ filename: "vid5.flv" }).type.should.equal("video");
files.find({ filename: "vid6.swf" }).type.should.equal("video");
files.find({ filename: "vid7.mp4" }).type.should.equal("video");
files.find({ filename: "vid8.ogv" }).type.should.equal("video");
```

<a name="cms-file-next"></a>
### #next
Return the next file.

```js
var doc1 = files.find({ filename: "doc1.ppt" });
var doc2 = doc1.next;
var doc3 = doc1.next.next;
var doc4 = doc1.next.next.next;
var image1 = doc1.next.next.next.next;
//=>
doc2.filename.should.equal("doc2.xls");
doc3.filename.should.equal("doc3.doc");
doc4.filename.should.equal("doc4.pdf");
image1.filename.should.equal("image1.jpg");
```

<a name="cms-file-prev"></a>
### #prev
Return the previous file.

```js
var image1 = files.find({ filename: "image1.jpg" });
var doc4 = image1.prev;
var doc3 = image1.prev.prev;
var doc2 = image1.prev.prev.prev;
var doc1 = image1.prev.prev.prev.prev;
//=>
doc4.filename.should.equal("doc4.pdf");
doc3.filename.should.equal("doc3.doc");
doc2.filename.should.equal("doc2.xls");
doc1.filename.should.equal("doc1.ppt");
```

