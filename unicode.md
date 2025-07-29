The **Unicode** standard is a text encoding standard that maps characters to integer codes. It defines over $150,000$ unique characters across $168$ distinct scripts (as of Unicode 16.0).

The standard notation for a Unicode character may look something like `U+0073`, which is the Unicode representation of `s`. `s` has the code point $115$, represented as $0073$ in hexadecimal, and `U+` is the standard prefix for Unicode.

>[!tip] `ord()` and `chr()`
>In Python, the built-in `ord()`function takes in a single character argument and returns its Unicode integer representation. The `chr()` built-in takes in an integer code point and returns a string of its corresponding character.

## unicode encodings

The Unicode standard defines three encoding schemes: UTF-8, UTF-16, and UTF-32. UTF-8 is by far the most commonly used, being used by over 98% of webpages on the [[Internet]].

>[!tip] `encode()` and `decode()`
>In Python, the `encode()` and `decode()` string functions convert strings into their corresponding `<class 'bytes'>` objects, and vice versa. 

