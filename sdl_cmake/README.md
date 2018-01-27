م# Prerequisites
## Linux
run this command in terminal:
```
sudo apt-get install libsdl2-gfx-dev‬‬
```

## Mac
first install brew.
then run this command in terminal:
```
brew install sdl2_gfx
```

## Windows
Download windows folder(Preferably put it in your project folder)

# Cmake
Consider we have a c/c++ project with cmake and it's Executable name is 'project'.

## Linux
put this code in your CmakeLists.txt:
```
INCLUDE_DIRECTORIES(/usr/include/SDL2)
TARGET_LINK_LIBRARIES(project m SDL2 SDL2_gfx)
ADD_DEFINITIONS(-D_REENTRANT)
```

## Mac
put this code in your CmakeLists.txt
```
LINK_DIRECTORIES(/usr/local/lib)
INCLUDE_DIRECTORIES(/usr/local/include/SDL2)
TARGET_LINK_LIBRARIES(project m SDL2 SDL2_gfx)
ADD_DEFINITIONS(-D_REENTRANT)
```

## Windows 
put this code in your CmakeLists.txt(use path of 'x' instead of /path/to/x):
```
set(SDL2_GFX_INCLUDE_DIR "/path/to/sdl2-gfx-include")
set(SDL2_GFX_LibDir "/path/to/sdl2-gfx-lib")
set(SDL2_Flags "-mwindows -Wl,--no-undefined -static-libgcc")
set(SDL2_Includes "/path/to/sdl2-include")
set(SDL2_LibDir   "/path/to/sdl2-lib")
add_library(SDL2     STATIC IMPORTED)
add_library(SDL2main STATIC IMPORTED)
add_library(SDL2_GFX STATIC IMPORTED)
set_property(TARGET SDL2     PROPERTY IMPORTED_LOCATION "${SDL2_LibDir}/libSDL2.a")
set_property(TARGET SDL2main PROPERTY IMPORTED_LOCATION "${SDL2_LibDir}/libSDL2main.a")
set_property(TARGET SDL2_GFX PROPERTY IMPORTED_LOCATION "${SDL2_GFX_LibDir}/libsdl-gfx.a")
set(SDL2_Libs SDL2 SDL2main SDL2_GFX m dinput8 dxguid dxerr8 user32 gdi32 winmm imm32 ole32 oleaut32 shell32 version uuid)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 ${SDL2_Flags}")
target_link_libraries(project ${SDL2_Libs})
include_directories(${SDL2_Includes} ${SDL2_GFX_INCLUDE_DIR})
```

if you got this error:
```
undefined reference to WinMain
```
put this code at the top of your main function:
```
#ifdef main
# undef main
#endif /* main */
```
and define your main like this:
```
int main(int argc, char** argv){
...
return 0;
}
```
