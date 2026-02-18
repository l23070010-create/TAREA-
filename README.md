option casemap:none

includelib msvcrt.lib
includelib legacy_stdio_definitions.lib

extern printf:proc
extern getchar:proc

.data
    num1    dq 4
    num2    dq 6
    formato db "La suma de %lld + %lld es: %lld", 10, 0

.code
main PROC

    ; Alinear pila (requerido en x64)
    sub rsp, 28h

    ; Cargar primer número
    mov rax, [num1]

    ; Sumar segundo número
    add rax, [num2]

    ; Preparar parámetros para printf
    lea rcx, formato      ; 1er parámetro
    mov rdx, [num1]       ; 2do parámetro
    mov r8,  [num2]       ; 3er parámetro
    mov r9,  rax          ; 4to parámetro (resultado)

    call printf

    ; Pausa para que no se cierre
    call getchar

    ; Restaurar pila
    add rsp, 28h

    ret

main ENDP
END
