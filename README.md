<div align="center">

## Find all Files on harddrive, MFC and non\-MFC editon\!


</div>

### Description

With this code you can seek all files in a directory plus subdirs with your search critica , (e.g *.* or *.exe)

Sorry for the dutch comment, but i think you will get it
 
### More Info
 
FindFiles("*.*","C:/Windows")

Use C:/path/anotherdir instead of C:\path\anotherdir (do NOT use C:/path/anotherdir/ )


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[pinhead](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/pinhead.md)
**Level**          |Intermediate
**User Rating**    |4.0 (12 globes from 3 users)
**Compatibility**  |C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+
**Category**       |[Files](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/files__3-2.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/pinhead-find-all-files-on-harddrive-mfc-and-non-mfc-editon__3-3705/archive/master.zip)

### API Declarations

```
string.h
windows.h
```


### Source Code

```

//Code Start MFC Edition-->
void FindFiles(CString FileMask,CString StartDir)
{
//Findfile test
//Ex: FindFiles ("*.*,"C:\windows\");
CString CompletePath;
CString strFile;
char een = 92;
char twee = 47;
HANDLE hFind;
WIN32_FIND_DATA FindInfo;
WIN32_FIND_DATA *FindInfoPoint = &FindInfo;
//StartDir en Mask samenvoegen en eerste file vragen
//Vervang \ naar / om \n chars etc te voorkomen
StartDir.Replace(een,twee);
CompletePath = StartDir + FileMask;
hFind = FindFirstFile(CompletePath ,FindInfoPoint);
//SetWindowText(FindInfo.cFileName);
if ( hFind == NULL ) return;
while ( hFind != NULL )
{
//returned 0 als zoeken klaar is
if ( FindNextFile(hFind,FindInfoPoint) == 0 ) { break;}
strFile = FindInfo.cFileName;
//kijken of we een dir hebben, niet reageren op . of ..
if (FindInfo.dwFileAttributes = FILE_ATTRIBUTE_DIRECTORY && strFile.Left(1) != "." )
{
//We hebben een directory!
	if ( strFile.Right(1) != twee )
	{	// / toevoegen
		strFile = strFile + twee;
	}
//Nieuwe pad maken OudeDir + NieuweDir
strFile = StartDir + strFile;
FindFiles(FileMask,strFile);
//eoi
}
if ( FindInfo.dwFileAttributes = FILE_ATTRIBUTE_NORMAL)
{
	strFile = StartDir + FindInfo.cFileName;
	SetWindowText(strFile);
}
//eow
}
FindClose(hFind);
return;
//MessageBox("Done");
}
//End Code MFC Edition-->
//Code Start Non-MFC Edition-->
void FindFiles(char FileMask[300],char StartDir[300])
{
//Findfile test
//Ex: FindFiles ("*.*,"C:\windows\");
LPCTSTR CompletePath ="";
LPCTSTR strFile = "";
char chrOrginalDir[300];
char chrNewDir[300];
char chrFile[300];
char chrDisplay[600];
char een[1];
char tmp[2];
const char twee = 47;
int Pathlen =0;
int x =0;
LPCTSTR Twee = "\0x2F";
HANDLE hFind;
WIN32_FIND_DATA FindInfo;
WIN32_FIND_DATA *FindInfoPoint = &FindInfo;
Pathlen = strlen((LPCTSTR)StartDir);
sprintf(tmp,"%d",Pathlen);
//Orginele dir bewaren voordat we /*.* toevoegen
strcpy(chrOrginalDir,StartDir);
//Extentie toevoegen , voor de zekerheid nog een /
strcat(StartDir, "/*.*");
hFind = FindFirstFile(StartDir ,FindInfoPoint);
if ( hFind == NULL ) return;
while ( hFind != NULL )
{
if ( FindNextFile(hFind,FindInfoPoint) == 0 ) { break;}
strcpy(chrFile,FindInfoPoint->cFileName);
if ( FindInfoPoint->dwFileAttributes == FILE_ATTRIBUTE_DIRECTORY )
{
//We hadden .. of .
if ( chrFile[0] == '.' ) { continue; }
strcpy(chrNewDir,chrOrginalDir);
strcat(chrNewDir,"/");
strcat(chrNewDir,FindInfoPoint->cFileName);
//MSGBox is alleen voor debug
//if ( MessageBox(hwndWindow,chrNewDir,chrNewDir,MB_OKCANCEL) == IDCANCEL ) { return;}
FindFiles(FileMask,chrNewDir);
}
else
{
//We hebben alles behalve een directory
strcpy(chrDisplay,chrOrginalDir);
strcat(chrDisplay,"/");
strcat(chrDisplay,FindInfoPoint->cFileName);
SetWindowText(hwndWindow,chrDisplay);
}
//eow
}
FindClose(hFind);
return;
}
//End Code non-MFC Edition-->
```

