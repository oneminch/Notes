- **CR** aka **_Carriage Return_** (`\r`), moves cursor to the beginning of a line.
    - e.g. Download progress bars on terminals.
- **LF** aka **_Line Feed_** or **_newline_** (`\n`), moves cursor down to the next line.
- **CRLF** (`\r\n`) moves the cursor down to the beginning of the next line.

> [!NOTE]
> **CRLF** is considered to be redundant in today's systems. As long as the meaning of a **LF** is defined by the OS to indicate the next line starts at the beginning, there is no need for the use of both **CR** and **LF**; The job can be done with one symbol.
