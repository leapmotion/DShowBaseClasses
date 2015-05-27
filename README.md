DirectShow Base Classes
=====

This file just contains the Microsoft DirectShow base classes wrapped up in a nice CMakeLists.txt for use with projects that use CMake but still rely on these old libraries.  Some modifications have been made to make these source compile without errors on the latest platform SDK, other than that they are provided more or less as they came with the Windows 7.1 SDK Samples.

Configuration
---
To configure, build, and package:

    cmake . -G "Visual Studio 12 2013 Win64"
    cmake . --build . --config Release
    cpack

The packaged result will be called `baseclasses-<version>-win64.zip`.  32 bit builds are configured the same way, just omit the `Win64` statement.

Usage
---
This project was built with the intention of being found with CMake's [`find_package`](http://www.cmake.org/cmake/help/v3.2/command/find_package.html) command.  Usage is as follows:

```CMake
find_package(baseclasses 1.0 REQUIRED)
target_link_libraries(MyDShowProject BaseClasses::BaseClasses)
```

You shouldn't need to reference any include directories explicitly.  They will be added for you by the `target_link_libraries` command.  To include BaseClasses in your project:

```C++
#include <baseclasses/Streams.h>

class CMyFilter:
  public CTransformFilter
{
public:
  CMyFilter(void);

  HRESULT CheckMediaType(const CMediaType* pmt) override;
  HRESULT DoRenderSample(IMediaSample* pSample) override;
};
```
