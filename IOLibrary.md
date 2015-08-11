
```
get == input == read
put == output == write
```

  * iso\_base
    * Maintains state information that reflects the integrity of the stream buffer.
    * Implement the functions regarding the state flags.
  * basic\_ios
    * Maintains the pointer to the stream buffer. It doesn't own the buffer (don't need to delete the buffer).
    * Implement the functions to get and set the stream buffer. It overloads the <</>> operators to manage the underlying data.
    * Implement the functions regarding the state flags.
    * It is the only virtual base class in the io library.
  * basic\_istream and basic\_ostream
    * Implements all the input and output functions on the stream buffer.
  * basic\_iostream
    * It just merges the input and output stream in a single class. It doesn't implement any extra functions.
  * The basic\_istringstream level classes
    * Maintain the stream buffer and set the buffer address to basic\_ios in constructor.
    * Implement the functions to manipulate the stream buffer. They don't implement any i/o functions to the stream.


  * basic\_streambuf
    * serves as an abstract base class for deriving various stream buffers whose objects each control two character sequences
    * Maintains the pointer to the buffer area. It doesn't own the actual buffer. (Don't need to delete the buffer)
    * Defines the input and output functions on the buffer.
  * basic\_stringbuf and basic\_filebuf
    * Maintains the actual buffer area. They are responsible to create and release the area.
    * Override the i/o functions on the distinct buffer area.

  * Usage
    * If pass a basic\_string object to the constructor of basic\_stringbuf or string stream, the data will be copied. The subsequent changes to the basic\_string don't affect the basic\_stringbuf or stream.

![http://i.stack.imgur.com/9wUHa.gif](http://i.stack.imgur.com/9wUHa.gif)

```
iso_base
    ^
    |-basic_ios<...>
         ^
         |-basic_istream<...>
         |       ^
         |       |-basic_istringstream<...>
         |       |-basic_ifstream<...>
         |
         |-basic_ostream<...>
                 ^
                 |-basic_ostringstream<...>
                 |-basic_ofstream<...>


basic_istream<...>    basic_ostream<...>
       ^                                            ^
       |                                             |
        -----------------------------------
                              |
                 basic_iostream<...>
                              ^
                              |-basic_stringstream<...>
                              |-basic_fstream<...>

basic_streambuf<�>
    ^
    |-basic_stringbuf<...>
    |-basic_filebuf<...>


    basic_string<char> str = "ABCD EFG";
    basic_stringbuf<char> strbuf(str);
    
    streamsize howmanyc = strbuf.in_avail();
    int getc = strbuf.snextc();
    int ret = strbuf.sputc('a');
```