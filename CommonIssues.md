# Common issues

*Windows XP / Vista are no longer supported.*

1. The program crashes near the end of a simulation, right before the report is open. 
> Try adding     decorated_tooltips=0   to your simulation. There are some overzealous "internet security" and VPN programs that crash Simulationcraft during the report generation for currently unknown reasons.
 
2. api-ms-win-crt-runtime-l1-1-0.dll is missing!
>  Run windows update and grab everything, or download this - https://support.microsoft.com/en-us/kb/2999226.

3. If you are on Windows 7, make sure to install Service Pack 1. The GUI will crash every time without it.

4. While importing any character: BCP API: Unable to download player from '(Website)' reason: Internal server error.**
> If this happens, unfortunately there is nothing that can be done. It is an internal server error somewhere between blizzard and your computer, and may fix itself with time.

5. Error message when loading program that includes 'Qt(something).dll'
> There have been a few cases that we haven't been able to fix, but a majority of the time this is from antivirus software detecting it as a threat and deleting it. If downloaded from the official links on our site, we can assure you there are no viruses in the program, just tell your antivirus software to ignore it and re-download the file.

If you are still having issues with the program, please submit an issue ticket, and we will try our best to help you out.