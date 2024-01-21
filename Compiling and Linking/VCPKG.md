1. Clone `vcpkg` into your repository. 
2. cd `vcpkg` and run for windows `.\bootstrap-vcpkg.bat` or for linux `./bootstrap-vcpkg.sh` 
3. `./vcpkg integrate install` (visual studio related) - not needed
4. `./vcpkg.exe install` (`.\vcpkg\vcpkg install [packages to install] --triplet=x64-windows`)
5. Tell Cmake where to find `vcpkg\scripts\build`

File dependencies go in a `vcpkg.json` file at root. 



