Access the minimal C64 compression tool with: <https://martinpiper.github.io/C64WasmCompressionTool/C64CompressToolExample.html>

The actual work is done by function compressFile()

Access the old Wasm test page with: <https://martinpiper.github.io/C64WasmCompressionTool/hello.html>

The original CPP code is in: <https://github.com/martinpiper/C64Public/tree/master/Compression>

This was compiled on Windows (note the paths) with emscripten using:
```
emcc -O3 -o hello.html -s EXPORTED_RUNTIME_METHODS=["callMain"] -s INVOKE_RUN=0 -s STACK_SIZE=1048576 -sALLOW_MEMORY_GROWTH -sASSERTIONS c:\work\c64\Compression\main.cpp c:\work\c64\Common\ParamToNum.cpp c:\work\c64\Compression\Compress.cpp c:\work\c64\Compression\CompressE.cpp c:\work\c64\Compression\CompressRLE.cpp c:\work\c64\Compression\CompressU.cpp c:\work\c64\Compression\CompressV.cpp c:\work\c64\Compression\Decompress.cpp c:\work\c64\Compression\DecompressE.cpp c:\work\c64\Compression\DecompressU.cpp
```

Since INVOKE_RUN=0 is used this stops the Wasm main being called on page load. Note the STACK_SIZE is quite large and may need to be larger if large prg files or expensive compression options are used.

When the Wasm test page (hello.html) loads, open the browser debug console and execute commands to test the compression tool.

File data can be created by the page, main called with arguments, and the output file data read with javascript like:
```
	FS.createDataFile("/","foo.txt","test data that can be compressed because it uses test data and that can be compressed",true,true,true)
	Module.callMain(["-cu", "foo.txt" , "foo.cmp"])
	FS.readFile("foo.cmp")
```

To display help use command line arguments: -h

For best (compression size and decompression speed) self extraction prg options use:
```
 -c64mu <input file> <outfile file> <run address> [start address] [skip start bytes]
```
For example this will compress a foo.prg to foocompressed.prg and call the start address at hex $400:
```
 -c64mu "foo.prg" "foocompressed.prg" $400
```

There are other options for setting the processor port, choosing border flash, setting top of memory etc.
