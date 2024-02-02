Multiple inheritance leads to new ambiguities:

```c++
class BorrowableItem
{
  public:
    void checkOut();
};

class ElectronicGadget
{
  private:
    bool checkOut() const;
};

class MP3Player : public BorrowableItem, public Electronic Gadget
{}

MP3Player mp; 
mp.checkOut();
```

In the call above for `mp.checkOut()` which function is called? The one from BorrowableItem or the one from ElectronicGadget? In this case the call is _ambiguous_ and the compiler will tell you so. This is despite the one from ElectronicGadget being private. You can resolve this by specifying the base class:

```c++
mp.BorrowableItem::checkOut()
```

MI with hierarchies that have higher-level base classes can lead to what is known as the "deadly MI diamond":

```c++
class File {};

class InputFile: public File {};

class OutputFile: public File {};

class IOFile: public InputFile, public OutputFile {}; 
```