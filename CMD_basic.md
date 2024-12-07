# Windows Command Prompt (CMD) Basic Tutorial


## Introduction

The Windows Command Prompt (CMD) is a powerful command-line interface that provides direct interaction with the Windows operating system. It's a versatile tool that allows users to perform administrative tasks, automate operations, and manage system configurations through text-based commands.

### Why Learn CMD?
- Faster execution of tasks compared to GUI
- Automation capabilities through batch scripts
- Better control over system operations
- Essential for IT professionals and power users
- Valuable debugging and troubleshooting tool

## Getting Started

### Multiple Ways to Access CMD

1. **Using Run Dialog**:
   - Press `Windows + R`
   - Type `cmd`
   - Press `Enter`

2. **Through Start Menu**:
   - Click Start or press Windows key
   - Type "Command Prompt"
   - Click on "Command Prompt" or press Enter

3. **Quick Access Methods**:
   - Right-click Start Button → Windows Terminal (Admin)
   - Press `Windows + X` → Windows Terminal (Admin)
   - In File Explorer's address bar, type `cmd` and press Enter

4. **From File Explorer**:
   - Hold `Shift` + Right-click in any folder
   - Select "Open command window here" or "Open PowerShell window here"

### Understanding the CMD Interface

The command prompt window displays:
```
C:\Users\YourUsername>
```
This is called the "prompt" and shows:
- Current drive (C:)
- Current directory path (\Users\YourUsername)
- Greater than symbol (>) indicating ready for input

## Basic Navigation

### Essential Navigation Commands

1. **Directory Listing**:
```batch
dir                     # List contents of current directory
dir /a                 # Show hidden files
dir /s                 # List contents including subdirectories
dir /w                 # Wide list format
dir *.txt              # List only .txt files
dir /a:h               # List only hidden files
dir /o:s               # Sort by size
dir /b                 # Bare format (names only)
```

2. **Changing Directories**:
```batch
cd [directory]         # Change to specific directory
cd ..                  # Move up one level
cd \                   # Move to root of current drive
cd /d D:              # Change drive and directory
cd.                    # Display current directory path
```

3. **Drive Navigation**:
```batch
D:                     # Switch to D: drive
cd /d D:\folder       # Change drive and directory in one command
```

## File and Directory Management

### Working with Files

1. **File Creation and Editing**:
```batch
type nul > file.txt    # Create empty file
echo Hello > file.txt  # Create file with content
copy con file.txt      # Create file and input content (Ctrl+Z to save)
```

2. **File Operations**:
```batch
copy source.txt dest.txt           # Copy file
move source.txt D:\destination     # Move file
rename oldname.txt newname.txt     # Rename file
del file.txt                       # Delete file
del /f /q file.txt                # Force delete without confirmation
```

3. **File Attributes**:
```batch
attrib +r file.txt     # Make read-only
attrib -r file.txt     # Remove read-only
attrib +h file.txt     # Make hidden
attrib -h file.txt     # Remove hidden
```

### Directory Management

1. **Creating Directories**:
```batch
mkdir NewFolder                    # Create directory
md "My Documents\New Folder"      # Create with spaces in name
mkdir "folder1" "folder2"         # Create multiple folders
```

2. **Removing Directories**:
```batch
rmdir folder                      # Remove empty directory
rd /s /q folder                  # Remove directory and contents without confirmation
```

## System Commands

### System Information

1. **Hardware Info**:
```batch
systeminfo                        # Detailed system information
wmic cpu get name                # CPU information
wmic memorychip get capacity     # RAM information
wmic diskdrive get size          # Disk drive sizes
```

2. **Operating System Info**:
```batch
ver                              # Windows version
winver                          # Windows version with GUI
hostname                        # Computer name
whoami                          # Current user
```

### Environment Variables

1. **Viewing Variables**:
```batch
set                             # List all variables
echo %PATH%                     # View PATH variable
echo %USERPROFILE%             # View user profile path
```

2. **Modifying Variables**:
```batch
setx VARIABLE "value"          # Set permanent variable
set TEMP_VAR=value            # Set temporary variable
```

## Network Commands

### Network Diagnostics

1. **Connection Testing**:
```batch
ping google.com                # Test connection
ping -t google.com            # Continuous ping
tracert google.com            # Trace route
pathping google.com           # Detailed path analysis
```

2. **Network Configuration**:
```batch
ipconfig                      # Basic IP configuration
ipconfig /all                # Detailed network information
ipconfig /release            # Release IP address
ipconfig /renew             # Renew IP address
ipconfig /flushdns          # Clear DNS cache
```

3. **Network Statistics**:
```batch
netstat                      # Network statistics
netstat -an                 # All connections and listening ports
netstat -b                  # Show executable involved (admin)
```

## Process Management

### Viewing Processes

1. **Process Lists**:
```batch
tasklist                    # List all running processes
tasklist /v                # Verbose list with more details
tasklist /fi "USERNAME eq NT AUTHORITY\SYSTEM"  # Filter by username
```

2. **Specific Process Info**:
```batch
tasklist /fi "IMAGENAME eq chrome.exe"   # Find specific process
tasklist /fi "MEMUSAGE gt 100000"       # Find memory-heavy processes
```

### Managing Processes

1. **Terminating Processes**:
```batch
taskkill /IM "process.exe"              # Kill by process name
taskkill /PID 1234                      # Kill by process ID
taskkill /IM "process.exe" /F           # Force kill
```

2. **Starting Processes**:
```batch
start notepad.exe                       # Start program
start "" "C:\Program Files\App\App.exe" # Start with path
start /min program.exe                 # Start minimized
```

## Batch Scripting

### Basic Script Structure

1. **Simple Batch File**:
```batch
@echo off
rem This is a comment
echo Hello, World!
pause
```

2. **Variables and User Input**:
```batch
@echo off
set /p name=Enter your name: 
echo Hello, %name%!
pause
```

3. **Conditional Statements**:
```batch
@echo off
if exist "file.txt" (
    echo File exists
) else (
    echo File not found
)
```

### Advanced Scripting

1. **Loops**:
```batch
@echo off
for %%i in (1,2,3,4,5) do (
    echo Number: %%i
)

for /l %%x in (1,1,5) do (
    echo Count: %%x
)
```

2. **Functions (Labels)**:
```batch
@echo off
call :MyFunction
exit /b

:MyFunction
echo This is a function
goto :eof
```

## Advanced Techniques

### Redirection and Pipes

1. **Output Redirection**:
```batch
dir > directory_list.txt           # Save output to file
dir >> directory_list.txt         # Append output to file
dir 2> error_log.txt             # Redirect errors
dir > output.txt 2>&1            # Redirect both output and errors
```

2. **Pipes**:
```batch
dir | find "txt"                 # Filter dir output
sort < input.txt > output.txt    # Sort file contents
```

### Command Chaining

1. **Multiple Commands**:
```batch
command1 && command2             # Run command2 if command1 succeeds
command1 || command2             # Run command2 if command1 fails
command1 & command2             # Run both commands
```

## Security and Permissions

### File Permissions

1. **Viewing Permissions**:
```batch
icacls file.txt                 # View permissions
```

2. **Modifying Permissions**:
```batch
icacls file.txt /grant Users:F  # Grant full access
icacls file.txt /deny Users:W   # Deny write access
```

### Running as Administrator

1. **Elevation Methods**:
```batch
runas /user:administrator cmd   # Run as different user
powershell Start-Process cmd -Verb RunAs  # Run as admin
```

## Tips and Tricks

### Keyboard Shortcuts

- `↑` / `↓` - Navigate command history
- `Tab` - Auto-complete file/folder names
- `Ctrl + C` - Cancel current command
- `Ctrl + A` - Move to start of line
- `Ctrl + E` - Move to end of line
- `F7` - Display command history
- `Alt + F7` - Clear command history

### Command History

```batch
doskey /history              # View command history
F7                          # Show command history window
```

### Screen Management

```batch
cls                         # Clear screen
mode con cols=100 lines=50  # Resize window
color 0A                    # Change colors (0=background, A=text)
title Custom Window         # Change window title
```

## Troubleshooting

### Common Issues and Solutions

1. **Access Denied**
   - Run CMD as Administrator
   - Check file/folder permissions
   - Verify user account privileges

2. **Command Not Found**
   - Check PATH environment variable
   - Verify command spelling
   - Ensure proper installation

3. **Path Issues**
   - Use quotes for paths with spaces
   - Use proper path separators
   - Check current directory

## Best Practices

1. **Security**
   - Don't run as admin unless necessary
   - Be careful with system-modifying commands
   - Back up before major changes

2. **Efficiency**
   - Use tab completion
   - Learn keyboard shortcuts
   - Create aliases for common commands

3. **Organization**
   - Comment your batch scripts
   - Use meaningful variable names
   - Structure complex scripts with functions

## Additional Resources

### Official Documentation
- [Microsoft Command-Line Reference](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)
- [Windows CMD Documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/cmd)


## Command Reference Table

| Command | Description |
|---------|------------|
| `dir` | Lists files and directories in the current directory |
| `dir /a` | Shows all files including hidden ones |
| `dir /s` | Lists files in current directory and all subdirectories |
| `dir /w` | Displays files in wide list format |
| `dir *.txt` | Lists only files with .txt extension |
| `cd` | Changes directory |
| `cd ..` | Moves up one directory level |
| `cd \` | Moves to root of current drive |
| `cd /d D:` | Changes drive and directory |
| `mkdir` or `md` | Creates a new directory |
| `rmdir` or `rd` | Removes an empty directory |
| `rd /s /q` | Removes directory and all contents without confirmation |
| `type nul >` | Creates an empty file |
| `echo` | Displays messages or turns command echoing on/off |
| `copy` | Copies files |
| `move` | Moves files |
| `rename` | Renames files |
| `del` | Deletes files |
| `attrib` | Displays or changes file attributes |
| `systeminfo` | Displays detailed system information |
| `wmic` | Windows Management Instrumentation Command |
| `ver` | Shows Windows version |
| `winver` | Shows Windows version with GUI |
| `hostname` | Displays computer name |
| `whoami` | Shows current user account |
| `set` | Displays or sets environment variables |
| `setx` | Sets environment variables permanently |
| `ping` | Tests network connectivity |
| `tracert` | Shows route to a network host |
| `pathping` | Shows route with detailed latency and packet loss |
| `ipconfig` | Displays network configuration |
| `ipconfig /all` | Shows detailed network configuration |
| `ipconfig /release` | Releases IP address |
| `ipconfig /renew` | Renews IP address |
| `ipconfig /flushdns` | Clears DNS cache |
| `netstat` | Displays network statistics |
| `tasklist` | Lists running processes |
| `taskkill` | Terminates processes |
| `start` | Starts a program or command |
| `cls` | Clears the screen |
| `color` | Changes console colors |
| `title` | Sets window title |
| `mode con` | Sets console window size |
| `doskey /history` | Shows command history |
| `runas` | Runs program as different user |
| `shutdown /s` | Shuts down computer |
| `shutdown /r` | Restarts computer |
| `icacls` | Displays or modifies file permissions |
| `find` | Searches for text string in files |
| `sort` | Sorts input |
| `pause` | Pauses batch file execution |
| `call` | Calls one batch file from another |
| `goto` | Directs batch processing to labeled line |
| `if` | Performs conditional processing |
| `for` | Runs command for each item in set |

## 👤 Author

Leo Gama
- GitHub: [@LeoGamaJ](https://github.com/LeoGamaJ)
- Email: leo@leogama.cloud 
- LinkedIn: (https://www.linkedin.com/in/leonardo-gama-jardim/)
