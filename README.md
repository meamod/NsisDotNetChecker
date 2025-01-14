# .NET Framework Checker NSIS plugin
The .NET Framework Checker NSIS plugin is used to detect if the required .NET Framework is installed and if it is not - plugin will download and install the required package. The plugin's C++ source code is based on the [work of Aaron Stebner](http://blogs.msdn.com/b/astebner/archive/2009/06/16/9763379.aspx).

## Structure:
 - `bin` - compiled NSIS plugin (ready-to-use)
 - `plugin` - contains source code for building DotNetChecker plugin in Visual Studio 2010
 - `nsis` - contains CheckNetFramework macros (DotNetChecker.nsh and DotNetCheckerOnly.nsh) and example NSIS installation file

## Installation

### All Users
1. Copy `DotNetChecker.dll` to NSIS plugins directory (usually `C:\Program Files\Nsis\Plugins\` or `C:\Program Files (x86)\Nsis\Plugins\`)
2. Add to your installer project `DotNetChecker.nsh` or `DotNetCheckerOnly.nsh` file
3. Reference `DotNetChecker.nsh` or `DotNetCheckerOnly.nsh` in your main NSI file like this:
		`!include "DotNetChecker.nsh"` or or `!include "DotNetCheckerOnly.nsh"`
4. Insert macros with the version of required .NET framework.

### Local
1. Copy the whole project in to the same folder as your NSIS Script.
2. Refrence the Plugin DLL like this: `!addplugindir "NsisDotNetChecker\bin"`
3. Reference `DotNetChecker.nsh` or `DotNetCheckerOnly.nsh` in your main NSI file like this: `!include "NsisDotNetChecker\nsis\DotNetChecker.nsh"` or `!include "NsisDotNetChecker\nsis\DotNetCheckerOnly.nsh"`

## Usage

The Plugin and its Macro(s) can be invoked by any Function or within any Section of the NSI script.
Only one macro needs to be used:
`CheckNetFramework` will reboot if required in the middle of the macro
`CheckNetFrameworkDelayRestart` overrides a reboot, and returns "true" if an installer was run.

### .NET 4.8.1

	!insertmacro CheckNetFramework 481
	!insertmacro CheckNetFrameworkDelayRestart 481 $0 ; Returns if an install was performed

### .NET 4.8

	!insertmacro CheckNetFramework 48
	!insertmacro CheckNetFrameworkDelayRestart 48 $0 ; Returns if an install was performed

### .NET 4.7.2

	!insertmacro CheckNetFramework 472
	!insertmacro CheckNetFrameworkDelayRestart 472 $0 ; Returns if an install was performed

### .NET 4.7.1

	!insertmacro CheckNetFramework 471
	!insertmacro CheckNetFrameworkDelayRestart 471 $0 ; Returns if an install was performed

### .NET 4.7

	!insertmacro CheckNetFramework 47
	!insertmacro CheckNetFrameworkDelayRestart 47 $0 ; Returns if an install was performed

### .NET 4.6.2

	!insertmacro CheckNetFramework 462
	!insertmacro CheckNetFrameworkDelayRestart 462 $0 ; Returns if an install was performed

### .NET 4.6.1

	!insertmacro CheckNetFramework 461
	!insertmacro CheckNetFrameworkDelayRestart 461 $0 ; Returns if an install was performed
	
### .NET 4.6

	!insertmacro CheckNetFramework 46
	!insertmacro CheckNetFrameworkDelayRestart 46 $0 ; Returns if an install was performed

### .NET 4.5.2

	!insertmacro CheckNetFramework 452
	!insertmacro CheckNetFrameworkDelayRestart 452 $0 ; Returns if an install was performed

### .NET 4.5.1

	!insertmacro CheckNetFramework 451
	!insertmacro CheckNetFrameworkDelayRestart 451 $0 ; Returns if an install was performed

### .NET 4.5

	!insertmacro CheckNetFramework 45
	!insertmacro CheckNetFrameworkDelayRestart 45 $0 ; Returns if an install was performed

### .NET 4.0 Client

	!insertmacro CheckNetFramework 40Client
	!insertmacro CheckNetFrameworkDelayRestart 40Client $0 ; Returns if an install was performed

### .NET 4. Full

	!insertmacro CheckNetFramework 40Full
	!insertmacro CheckNetFrameworkDelayRestart 40Full $0 ; Returns if an install was performed

### .NET 3.5

	!insertmacro CheckNetFramework 35 ; if your application targets .NET 3.5 Framework
	!insertmacro CheckNetFrameworkDelayRestart 35 $0 ; Returns if an install was performed

### .NET 3.0

	!insertmacro CheckNetFramework 30 ; if your application targets .NET 3.0 Framework
	!insertmacro CheckNetFrameworkDelayRestart 30 $0 ; Returns if an install was performed

### .NET 2.0

	!insertmacro CheckNetFramework 20 ; if your application targets .NET 2.0 Framework
	!insertmacro CheckNetFrameworkDelayRestart 20 $0 ; Returns if an install was performed

### .NET 1.1

	!insertmacro CheckNetFramework 11 ; if your application targets .NET 1.1 Framework
	!insertmacro CheckNetFrameworkDelayRestart 11 $0 ; Returns if an install was performed

### .NET 1.0

	!insertmacro CheckNetFramework 10 ; if your application targets .NET 1.0 Framework
	!insertmacro CheckNetFrameworkDelayRestart 10 $0 ; Returns if an install was performed

---

*NB:* Script will download .NET 3.5 for both .NET 3.0 and .NET 3.5 requirements. The same rule applies to .NET 1.1 and .NET 1.0. If you want to change this behavior - feel free to edit DotNetChecker.nsh.

*NB2:* Plugin is also capable of detecting Framework Service Pack Level. To use this functionality, just call one of the corresponding functions (i.e. DotNetChecker::GetDotNet11ServicePack). 

The return value (Pop $0) will be:

- -2 if framework is not installed

- -1 if no service pack installed for this framework

- some positive int value otherwise

*NB3:* Plugin works not only in UNICODE but also in ANSI scripts.

*NB4:* The plugin can be called more than once for installing two (or more) different versions of framework.
