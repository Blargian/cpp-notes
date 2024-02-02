
```c++
static void checkForCarriageReturn(ReadBuffer & in)

{

if (!in.eof() && (in.position()[0] == '\r' || (in.position() != in.buffer().begin() && in.position()[-1] == '\r')))

throw Exception(ErrorCodes::INCORRECT_DATA, "\nYou have carriage return (\\r, 0x0D, ASCII 13) at end of first row."

"\nIt's like your input data has DOS/Windows style line separators, that are illegal in TabSeparated format."

" You must transform your file to Unix format."

"\nBut if you really need carriage return at end of string value of last column, you need to escape it as \\r.");

}
```

So what the hell is going on here? 

`!in.eof()` - eof returns true if all the data was read, so if not all the data was read 
`in.position()[0] == '\r'` - if the last character of the read buffer is a return 
`in.position() != in.buffer().begin()` - 
`in.position()[-1] == '\r')` - if the second last char is not a return