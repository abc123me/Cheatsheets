# Basic IO
- `std::istream` specifies an input stream
- `std::ostream` specifies an output stream
- `std::iostream` specifies an input/output stream
## Stream operators
Stream operators can be used to read/write data into a stream

| Operator       | Description                 |
|----------------|-----------------------------|
| stream << data | Writes data to stream       |
| stream >> data | Reads from stream into data |
|                |                             |
```cpp
using namespace std;
cout << "Hello world!" //Writes "Hello world!" to terminal output
int x = 0;
cin >> x; //Reads an integer from terminal input and writes it to variable x
```
## Terminal IO
- Comes from `#include <iostream>`
- `std::cout/cerr` Specifies an `ostream` redirecting to output/error
- `std::cin` Specifies an `istream` redirecting to terminal input
- `std::endl` references to the newline character of the OS
## File streams
- Comes from `#include <fstream>`
- Created using [std::fstream::open](http://www.cplusplus.com/reference/fstream/fstream/open/)
