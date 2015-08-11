
```
locale 1<>---* locale::facet
                        ^
                        |
                        |--ctype<> ---> locale::id
                        |--num_get<>
                        |--num_put<>
```

```
#include <iostream>
#include <sstream>

using namespace std;

int main()
{
    const locale& rLc = locale::classic();

    basic_stringbuf<char> strBuf;

    // Construct the output stream with the un-cached buffer.
    basic_ostringstream<char> oStream;
    static_cast<basic_ios<char>&>(oStream).rdbuf(&strBuf);
    ostreambuf_iterator<char> oIterator(static_cast<basic_ios<char>&>(oStream).rdbuf());

    // Insert numeric to output stream.
    // Get the facet from the locale with the specified category.
    const num_put<char>& nPut = use_facet<num_put<char>>(rLc);
    long insertedValue = 123;
    nPut.put(oIterator, oStream, oStream.fill(), insertedValue);
    cout << "Inserted value: " << strBuf.str().c_str() << endl;

    // Construct the input stream with the un-cached buffer.
    basic_istringstream<char> iStream;
    static_cast<basic_ios<char>&>(iStream).rdbuf(&strBuf);
    istreambuf_iterator<char> iIterator(static_cast<basic_ios<char>&>(iStream).rdbuf());

    // Extract numeric from input stream.
    const num_get<char>& nGet = use_facet<num_get<char>>(rLc);
    long exactedValue = 0;
    ios_base::iostate _State = ios_base::goodbit;
    nGet.get(iIterator, istreambuf_iterator<char>(0), iStream, _State, exactedValue);
    cout << "Extracted value: " << exactedValue << endl;

    // Output the result.
    if(exactedValue == insertedValue)
        cout << "SUCCESS: Inserter and extractor" << endl;
    else
        cout << "FAIL: Inserter and extractor" << endl;

    return 0;
}

```

A facet, informally, is a class interface for a service that may be obtained from a locale object. For example, the Standard C++ library facet num\_put<> formats numeric values, and collate<> provides an ordering for string values. A facet is also an object contained in a locale.

Each locale object contains a set of facet objects to provide these services. A C++ locale can be treated as a container of facets.
![http://stdcxx.apache.org/doc/stdlibug/images/locfig5.gif](http://stdcxx.apache.org/doc/stdlibug/images/locfig5.gif)
