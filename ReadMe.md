Access this with: https://martinpiper.github.io/C64WasmCompressionTool/hello.html

The original CPP code is in: https://github.com/martinpiper/C64Public/tree/master/Compression

This was compiled on Windows (note the paths) with emscripten using:
emcc -o hello.html -s EXPORTED_RUNTIME_METHODS=["callMain"] -s INVOKE_RUN=0 -s STACK_SIZE=1048576 c:\work\c64\Compression\main.cpp c:\work\c64\Common\ParamToNum.cpp c:\work\c64\Compression\Compress.cpp c:\work\c64\Compression\CompressE.cpp c:\work\c64\Compression\CompressRLE.cpp c:\work\c64\Compression\CompressU.cpp c:\work\c64\Compression\CompressV.cpp c:\work\c64\Compression\Decompress.cpp c:\work\c64\Compression\DecompressE.cpp c:\work\c64\Compression\DecompressU.cpp

Since INVOKE_RUN=0 is used this stops the Wasm main being called on page load. Note the STACK_SIZE is quite large and may need to be larger is large prg files or expensive compression options are used.

When the page loads, open the browser debug console and execute commands to test the compression tool.

File data can be created by the page, main called with arguments, and the output file data read with javascript like:
	FS.createDataFile("/","foo.txt","test data",true,true,true)
	Module.callMain(["-c", "foo.txt" , "foo.cmp"])
	FS.readFile("foo.cmp")

