# Text processing

# Find non-printing characters

* Instead of making assumptions about the byte range of non-ASCII characters, as most of the above solutions do, it's slightly better IMO to be explicit about the actual byte range of ASCII characters instead.  
   `grep --color='auto' -P -n '[^\x00-\x7F]' file.xml`  
   (which basically greps for any character outside of the hexadecimal ASCII range: from \x00 up to \x7F)
* On Mountain Lion that won't work (due to the lack of PCRE support in BSD grep), but with pcre installed via Homebrew, the following will work just as well:
   `pcregrep --color='auto' -n '[^\x00-\x7F]' file.xml`
* `grep --color='auto' -P -n "[\x80-\xFF]" file.xml`
* `grep --color='auto' -P -n "[^\x00-\x7F]" file.xml`
* Above require `pcre`, not native on macOS
* `ag "[\x80-\xFF]" file`
* `brew install pcre` then `pcregrep --color='auto' -n "[\x80-\xFF]" file.xml`

