These python files are wrappers on the ELTK python2 library (sofarrar/e-linguistics):

http://uakari.ling.washington.edu/e-linguistics/eltk.html

They are intended to convert between LaTeX files with IPA unicode characters (for xelatex compilation) and LaTeX files with TIPA codes (for pdflatex compilation).

# Install

* Ensure you have a distribution of python2
* Install eltk
* Put files somewhere in your `$PATH`
* Make them executable

# Usage

`tipafy` and `detipafy` are small wrappers on ELTK's character conversion functions. They can be used as command line tools, either with an argument or reading stdin:

~~~
$ tipafy bɔ̃ʒuʁ
\textipa{b\~O ZuK}
$ detipafy "\textipa{b\~O ZuK}"
bɔ̃ʒuʁ
$ tipafy bɔ̃ʒuʁ | detipafy
bɔ̃ʒuʁ
~~~

`tipafy_file` takes a LaTeX file and applies the transformation and normalizes all tokens (except in comments):

* longer than two characters and bounded by two "/" as in: "/bɔ̃ʒuʁ/" (but not "/bɔ̃/"). Be careful, this might mess with with URLS !
* or containing characters from the following unicode blocks:

~~~
   0080..00FF; Latin-1 Supplement <- from 128
   0100..017F; Latin Extended-A
   0180..024F; Latin Extended-B
   0250..02AF; IPA Extensions
   02B0..02FF; Spacing Modifier Letters
   0300..036F; Combining Diacritical Marks    <- to 879
   2C60..2C7F; Latin Extended-C  <- (11360, 11391)
   A720..A7FF; Latin Extended-D  <- (42784, 43007)
~~~

If not present, it adds "\\usepackage{tipa}" at the end of the document head.


`detipafy_file` does the opposite transformation for any token inside “\\textipa{(.+?)}”, and adds comments with the original textipa code.
