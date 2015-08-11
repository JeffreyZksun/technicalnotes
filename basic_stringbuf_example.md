# basic\_stringbuf example #

```
Get area access
eback(), gptr(), egptr()

Put area access
pbase(), pptr(), epptr()
```


```
#include <iostream>
#include <sstream>

using namespace std;

int main (int argc, const char * argv[])
{
    {
        basic_string<char> strData = "0123456789abcdef";
        basic_stringbuf<char> istrBuffer(strData); // Copy the existing data to initialize the buffer.
        
        cout << "************************************************************" << endl << endl;
        
        cout << "Initial buffer: " << istrBuffer.str() << endl;
        cout << "Input buffer size: " << istrBuffer.in_avail() << endl << endl;
        
        cout << "sbumpc (Increment the input pointer, read a char before changing input pointer): " << (char)istrBuffer.sbumpc() << endl;
        cout << "Input buffer size: " << istrBuffer.in_avail() << endl << endl;
        
        
        cout << "sgetc (NOT Increment the input pointer, read a char): " << (char)istrBuffer.sgetc() << endl; 
        cout << "Input buffer size: " << istrBuffer.in_avail() << endl << endl;
        
        cout << "snextc (call sbumpc then sgetc)(Increment the input pointer, read a char afeter changing input pointer): " << (char)istrBuffer.snextc() << endl;
        cout << "Input buffer size: " << istrBuffer.in_avail() << endl << endl;
        char tmpBuffer[5] = {'\0'};
        istrBuffer.sgetn(tmpBuffer, 4);
        cout << "sgetn (Increment the input pointer, read many chars): " << tmpBuffer << endl;
        cout << "Input buffer size: " << istrBuffer.in_avail() << endl << endl;
        
        cout << "sungetc (Decrement the input pointer, put back the previous char): " << (char)istrBuffer.sungetc() << endl; 
        cout << "Input buffer size: " << istrBuffer.in_avail() << endl << endl;
        
        
        cout << "sputbackc (Decrement the input pointer, put back a specified char): " << (char)istrBuffer.sputbackc('M') << endl; 
        cout << "Input buffer: " << istrBuffer.str() << endl;
        cout << "Input buffer size: " << istrBuffer.in_avail() << endl << endl;
    }
    
    {
        basic_stringbuf<char> ostrBuffer;
        
        cout << "************************************************************" << endl << endl; 
        cout << "Output buffer: " << ostrBuffer.str() << endl;
        
        cout << "sputc (Increase the output pointer, output a specified char): " << (char)ostrBuffer.sputc('A') << endl; 
        cout << "Output buffer: " << ostrBuffer.str() << endl;
        
        char tempBuffer[5] = "BCDE";
        cout << "sputn (Increase the output pointer, output many chars): " << ostrBuffer.sputn(tempBuffer, 4) << endl; 
        cout << "Output buffer: " << ostrBuffer.str() << endl;
        
        
    }
    
    
    return 0;
}
```

Output from Xcode
```
************************************************************

Initial buffer: 0123456789abcdef
Input buffer size: 16

sbumpc (Increment the input pointer, read a char before changing input pointer): 0
Input buffer size: 15

sgetc (NOT Increment the input pointer, read a char): 1
Input buffer size: 15

snextc (call sbumpc then sgetc)(Increment the input pointer, read a char afeter changing input pointer): 2
Input buffer size: 14

sgetn (Increment the input pointer, read many chars): 2345
Input buffer size: 10

sungetc (Decrement the input pointer, put back the previous char): 5
Input buffer size: 11

sputbackc (Decrement the input pointer, put back a specified char): M
Input buffer: 0123M56789abcdef
Input buffer size: 12

************************************************************

Output buffer: 
sputc (Increase the output pointer, output a specified char): A
Output buffer: A
sputn (Increase the output pointer, output many chars): 4
Output buffer: ABCDE
```