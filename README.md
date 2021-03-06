# UMDH Visualizer - Memory profile viewer
UMDH Visualizer helps you read the user memory heap dump reports more easily.
(NOTE: UMDH is a memory profiler tool provided by Microsoft.)
![Screen shot](http://i.imgur.com/1WV3cBB.png)

[UMDH(User-mode Dump Heap)](http://code.logos.com/blog/2009/04/how_to_use_umdh_to_find_native_memory_leaks.html) is a nice tool for capturing and 
analyzing memory status of Windows process. Example usage is:

1. Download and install UMDH. You can get it by installing [Debugging Tools for Windows or Windows SDK](https://msdn.microsoft.com/en-us/library/windows/hardware/ff551063%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396).
2. Run `MyApp.exe`.
3. Run `gflags -i MyApp.exe +ust` for start memory allocation tracing.
4. Set symbol path variable. UMDH needs it. Specify both Windows symbol download location, symbol cache and the symbol path of your program where pdb files reside. For example,
```
set _NT_SYMBOL_PATH=C:\Users\imays\works\MyApp\Release;srv*c:\symbols*https://msdl.microsoft.com/download/symbols
```
5. Run `umdh -pn:MyApp.exe -f:A.txt` for storing memory status into a text file A.
6. Run `umdh -pn:MyApp.exe -f:B.txt` again for storing another memory status into a text file B after `MyApp.exe` takes more memory.
7. Run `umdh -d A.txt B.txt > Diff.txt` for creating a diff file between A and B. It is successful if nothing is printed when this execution is finished.

After opening the diff file, you might be frustrated because it cannot tell you where hotspot of memory allocation lies concisely, because UMDH diff text does not accumulate same call stacks. UMDH Visualizer does it, so you can find the hot spot easily.

How to use
==========
[Download](https://github.com/Nettention/UmdhViz/releases) and Run UmdhViz.exe. Latest version of .Net Framework may be needed if you are using old version of Windows.

Click File => Open and select your UMDH Diff file.

Select the hot spot allocation at left pane and enjoy seeing its call stack at right pane!
![Screen shot](http://i.imgur.com/1WV3cBB.png)

Etc.
=======
Don't forget to click "[*Do you know ProudNet?*](http://www.nettention.com)" if you are interested to developing a game where a cutting edge networking and server technology is needed. :)

License 
========
Copyright Nettention Co., Ltd.

Lesser GPL.

