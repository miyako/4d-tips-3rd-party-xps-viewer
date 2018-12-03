# 4d-tips-3rd-party-xps-viewer

Use [xpsview](https://github.com/codeprof/xpsview) instead of native XPS viewer for print preview.

<img width="1142" alt="2018-11-30 18 07 23" src="https://user-images.githubusercontent.com/1725068/49279428-d04bcd80-f4ca-11e8-8336-8d6312a1c998.png">

Forked version of [xpsview](https://github.com/miyako/xpsview) supports the following custom options: ``TOP``, ``LEFT``, ``WIDTH``, ``HEIGHT``, ``ACTIVATE`` and ``NOPROGRESS``

### Examples

```
If (Not(Semaphore(Storage.semaphores.printing)))
	
	$currentPrinter:=Get current printer
	
	SET PRINT PREVIEW(True)
	SET PRINT OPTION(Spooler document name option;"aaaaa")
	
	$useXpsViewer:=useXpsViewer 
	
	OPEN PRINTING JOB
	$h:=Print form("TEST")
	CLOSE PRINTING JOB
	
	If ($useXpsViewer)
		
		$xpsDocumentPath:=""
		$destination:=0
		
		GET PRINT OPTION(Destination option;$destination;$xpsDocumentPath)
		
		C_OBJECT($options)
		
		$options:=New object(\
		"debug";False;\
		"noPrint";False;\
		"noCopy";False;\
		"noSearch";False;\
		"noNavigation";False;\
		"showQuit";False;\
		"x";30;\
		"y";30;\
		"width";1000;\
		"height";1000;\
		"noProgress";True;\
		"title";"PRINT PREVIEW")
		
		  //fullScreen: start in fullscreen modec (disabled)
		  //debug: write log file to temp directory
		  //noPrint: disable printing
		  //noCopy: disable cut and copy
		  //noSearch: disable search bar
		  //noNavigation: hide up/down buttons
		  //showQuit: show quit button
		  //title: sets the text in the title bar
		  //x, y, width, height: position and size of window
		  //noProgress: hide progress
		
		openWithXpsViewer ($xpsDocumentPath;$options)
		
		SET CURRENT PRINTER($currentPrinter)
		
	End if 
	
End if 
```
