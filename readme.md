# SQL Server setup

## Hyper-V

    OS: Windows Server 1803 Standard
    Licence key: $env:WIN1803STD
    CPU: 2
    Mem: 1024 (dynamically adjust)
    drive 0 : 40GB (system)
    drive 1 : 10GB (data)
    drive 3 : DVD ROM

## OS

    DVD ROM Drive Letter: Z:
        ```PowerShell
        gwmi win32_volume -filter "driveletter = 'd:'" | set-wmiinstance -arguments @{DriveLetter='Z:'}
        ```

    D:\Drive: New Disk, create volume D:\
        ```PowerShell
        get-disk | where partitionstyle -eq 'raw' | initialize-disk -partitionstyle GPT
        $d = get-disk -number 1
        New-Volume -Disk 1 -Filesystem NTFS -DriveLetter D -FriendlyName "Data"
        ```

## SQL Server

    unattended install file generated from first install. Copy the file from its saved location into this repo.
    ```PowerShell
    copy-item 'c:\program files\Microsoft Sql Server\140\Setup Bootstrap\Log\20181015_142431\ConfigurationFile.ini' -Destination Dev:\sssql01\ -FromSession $sess
    ```
    .\Setup.exe /ConfigurationFile=MyConfigurationFile.INI  