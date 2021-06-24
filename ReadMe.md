OCCT WebGL Viewer sample {#occt_samples_webgl}
================== 

This sample demonstrates simple way of using OCCT libraries in Web application written in C++ and translated into WebAssembly module using Emscripten SDK (emsdk):
https://emscripten.org/

Sample consists of the Open CASCADE 3D Viewer with a button for opening a model in BREP format.
The sample requires a WebGL 2.0 capable browser supporting WebAssembly 1.0 (Wasm).

Installation and configuration:
 1. Install Emscripten SDK and activate minimal configuration (Python, Java and CLang) following *emsdk* documentation. Activate also MinGW when building sample on Windows host.
 2. Build (using *emsdk*) or download FreeType static library.
~~~~~
    > https://stackoverflow.com/questions/61049517/build-latest-freetype-with-emscripten
~~~~~
 3. Configure CMake for building Open CASCADE Technology (OCCT) static libraries (BUILD_LIBRARY_TYPE="Static").
    For this, activate *emsdk* command prompt, configure CMake for building OCCT using cross-compilation toolchain, disable *BUILD_MODULE_Draw*. 
 4. Perform building and installation steps.
~~~~~
    > ${EMSDK}/fastcomp/emscripten/cmake/Modules/Platform/Emscripten.cmake
~~~~~
 5. Configure CMake for building this WebGL sample using *emsdk* with paths to OCCT and FreeType. Perform building and installation steps.
 6. Navigate to installation folder and start web server from it; Python coming with *emsdk* can be used for this purpose:
~~~~~
    > python -m http.server
~~~~~
 8. Open compatible browser and enter path taking into account your web server settings:
~~~~~
    > http://localhost:8000/occt-webgl-sample.html
~~~~~

![](GifOCCTGITHUB.gif)
