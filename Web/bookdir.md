BookDir
=====
* Tools used: Google Chrome Developer Console
* If we take a look at resources that are loading on the home page, we fill find the scripts `books.js` and `booklist.php`. The AJAX call from Javascript file reveals us the header `X-Dir: .`. If we change it to `X-Dir: ../` we could list upper directory files and after few tricky inputs tried on `booklist.php` we found that  the source code is like a open book: `view-source:http://89.38.210.129:8012/books/booklist.php?f=....//4o4_fl4g_n0t_f0und.php`.
