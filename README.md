What it does.
Decrypts shellcode which is an AES-256-CBC encrypted payload by HellShell which will decrypt at runtime using a hardcoded key and IV
Spawns a suspended legitimate process, svchost.exe (a trusted Windows system process) in a suspended state to use as a host for the malicious code.
Injects the shellcode which is the decrypted payload, written into the memory of the suspended svchost.exe process using VirtualAllocEx / WriteProcessMemory, then marked executable.
Executes via APC injection which uses QueueUserAPC to queue execution of the shellcode, then resumes the thread, causing the shellcode to run inside svchost.exe.
