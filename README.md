What it does.

1. Decrypts shellcode which is an AES-256-CBC encrypted payload by HellShell which will decrypt at runtime using a hardcoded key and IV  

2. Spawns a suspended legitimate process, svchost.exe (a trusted Windows system process) in a suspended state to use as a host for the malicious code.  

3. Injects the shellcode which is the decrypted payload, written into the memory of the suspended svchost.exe process using VirtualAllocEx / WriteProcessMemory, then marked executable.  

4. Executes via APC injection which uses QueueUserAPC to queue execution of the shellcode, then resumes the thread, causing the shellcode to run inside svchost.exe.
