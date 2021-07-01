OCCT WebGL Viewer sample {#occt_samples_webgl}
================== 

This sample demonstrates simple way of using OCCT libraries in Web application written in C++ and translated into WebAssembly module using Emscripten SDK (emsdk):
https://emscripten.org/

Sample consists of the Open CASCADE 3D Viewer with a button for opening a model in BREP format.
The sample requires a WebGL 2.0 capable browser supporting WebAssembly 1.0 (Wasm).

Installation and configuration:

 **1.** Install Emscripten SDK and activate minimal configuration (Python, Java and CLang) following *emsdk* documentation. Activate also MinGW when building sample on Windows host.

 **2.** Build (using *emsdk*) or download FreeType static library.
~~~~~
    > https://stackoverflow.com/questions/61049517/build-latest-freetype-with-emscripten
~~~~~

 **3.** Configure CMake for building Open CASCADE Technology (OCCT) static libraries (BUILD_LIBRARY_TYPE="Static").
    For this, activate *emsdk* command prompt, configure CMake for building OCCT using cross-compilation toolchain, disable *BUILD_MODULE_Draw*. 

 **4.** Perform building and installation steps.
~~~~~
    > ${EMSDK}/fastcomp/emscripten/cmake/Modules/Platform/Emscripten.cmake
~~~~~

 **5.** Configure CMake for building this WebGL sample using *emsdk* with paths to OCCT and FreeType. Perform building and installation steps.
~~~~~
    Command prompt emscripten :
    > emcmake cmake-gui
    Check "Advanced"
    Press "Configure"
    - specify toolchaine file : C:/Users/User/emsdk/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake
    - freetype_DIR : C:\dev\freetype\freetype-master\install-wasm\lib\cmake\freetype
    - CMAKE_INSTALL_PREFIX : C:/build-folder-location
    - CMAKE_BUILD_TYPE : release
    Press "Configure"
    - OpenCASCADE_DIR : C:\OpenCASCADE-7.5.0-vc14-64\opencascade-7.5.0\install-wasm\lib\cmake\opencascade
    Press "Configure"
    Press "Generate"
    Close CMake-Gui
    Command prompt emscripten :
    > cd "C:/build_folder_location"
    > emmake make install
~~~~~

 **6.** Install Apache Lounge (for the local server):
~~~~~
    > https://www.apachelounge.com/download/
~~~~~

 **7.** Open "httpd.conf" (C:\Apache24\conf).
~~~~~
    Line 251 and 252, replace the base path with your build folder location  :
    > DocumentRoot "build_folder_location"
    > <Directory "build_folder_location">
~~~~~

 **8.** If you want to block all caching and not compress the .wasm file every time (for all attempts until the project is complete), create an .htaccess file at the root of your apache server and paste the code at the end of ReadMe.md into it (and skip step 7).

 **9.** For the compression of the end .wasm file (in build folder) :
 * In "httpd.conf" :
~~~~~
    Line 416, remove the "#" and add ".wasm" : 
    > AddEncoding x-gzip .gz .tgz .wasm
~~~~~
 * Compress the .wasm file :
~~~~~
    > https://gzip.swimburger.net/  
~~~~~
 * Put the .gz file in the build folder location, delete the original .wasm, and rename the .gz file to .wasm :
~~~~~
    "wasm-openfile.wasm.gz" -> "wasm-openfile.wasm"
~~~~~

 **10.** Run "httpd.exe" (C:\Apache24\bin), open compatible browser and enter path taking into account your web server settings :
~~~~~
    > http://localhost/wasm-openfile.html
~~~~~

# Code .htaccess

~~~~~
# Prevent all caching because of a caching bug in iOS6 - run in directory with pache (github.com/devinrhode2/pache)
# ------------------------------------------------------------------------------
# | Expires headers (for better cache control)                                 |
# ------------------------------------------------------------------------------

<IfModule mod_expires.c>

    ExpiresActive on
    ExpiresDefault                                      "access plus 0 seconds"

  # CSS
    ExpiresByType text/css                              "access plus 0 seconds"

  # Data interchange
    ExpiresByType application/json                      "access plus 0 seconds"
    ExpiresByType application/xml                       "access plus 0 seconds"
    ExpiresByType text/xml                              "access plus 0 seconds"

  # Favicon (cannot be renamed!)
    ExpiresByType image/x-icon                          "access plus 0 seconds"

  # HTML components (HTCs)
    ExpiresByType text/x-component                      "access plus 0 seconds"

  # HTML
    ExpiresByType text/html                             "access plus 0 seconds"

  # JavaScript
    ExpiresByType application/javascript                "access plus 0 seconds"

  # Manifest files
    ExpiresByType application/x-web-app-manifest+json   "access plus 0 seconds"
    ExpiresByType text/cache-manifest                   "access plus 0 seconds"

  # Media
    ExpiresByType audio/ogg                             "access plus 0 seconds"
    ExpiresByType image/gif                             "access plus 0 seconds"
    ExpiresByType image/jpeg                            "access plus 0 seconds"
    ExpiresByType image/png                             "access plus 0 seconds"
    ExpiresByType video/mp4                             "access plus 0 seconds"
    ExpiresByType video/ogg                             "access plus 0 seconds"
    ExpiresByType video/webm                            "access plus 0 seconds"

  # Web feeds
    ExpiresByType application/atom+xml                  "access plus 0 seconds"
    ExpiresByType application/rss+xml                   "access plus 0 seconds"

  # Web fonts
    ExpiresByType application/font-woff                 "access plus 0 seconds"
    ExpiresByType application/vnd.ms-fontobject         "access plus 0 seconds"
    ExpiresByType application/x-font-ttf                "access plus 0 seconds"
    ExpiresByType font/opentype                         "access plus 0 seconds"
    ExpiresByType image/svg+xml                         "access plus 0 seconds"

</IfModule>
~~~~~

# Gallery

<img src="doc/GifOCCTGITHUB.gif"/>
