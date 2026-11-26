# Tema ASC

26/11/2026

Elcu Adrian

## tema.s

```asm
.data
    v: .long 6, 35, 10, 9, 14
    n: .long 5

.text

cmmdc:
    pushl %ebp
    mov %esp, %ebp
    movl 8(%ebp), %eax
    movl 12(%ebp), %ecx
    cmpl $0, %eax
    je et_a_zero
    cmpl $0, %ecx
    je et_final_cmmdc

et_while:
    cmpl %ecx, %eax
    je et_final_cmmdc
    jg et_mare
    subl %eax, %ecx
    jmp et_while

et_mare:
    subl %ecx, %eax
     jmp et_while

et_a_zero:
    movl %ecx, %eax

et_final_cmmdc:

    popl %ebp
    ret


numara:

    pushl %ebp
    mov %esp, %ebp

    pushl %ebx
    pushl %esi
    pushl %edi

    movl 8(%ebp), %esi
    movl 12(%ebp), %ecx

    xorl %ebx, %ebx
    xorl %edi, %edi


    cmpl $1, %ecx
    jle et_final_numara

    decl %ecx

et_for:
    movl (%esi,%edi,4), %eax
    pushl %ecx
    incl %edi
    movl (%esi,%edi,4), %ecx
    decl %edi



    pushl %ecx
    pushl %eax
    call cmmdc
    addl $8, %esp
    popl %ecx



    cmpl $1, %eax
    jne et_cont
    incl %ebx

et_cont:
    incl %edi
    loop et_for

et_final_numara:

    movl %ebx, %eax
    popl %edi
    popl %esi
    popl %ebx
    popl %ebp
    ret


.global main
main:
    pushl n
    pushl $v
    call numara
    addl $8, %esp

et_exit:
    movl $1, %eax
    xorl %ebx, %ebx
    int $0x80

```

## tema_ex2.s

```asm
.data
    v: .long 0, 5, 0, 3, 4
    n: .long 5

.text

interschimba:
    pushl %ebp
    mov %esp, %ebp

    pushl %ebx

    movl 8(%ebp), %eax
    movl 12(%ebp), %ecx

    movl (%eax), %ebx
    movl (%ecx), %edx

    movl %edx, (%eax)
    movl %ebx, (%ecx)

    popl %ebx
    popl %ebp
    ret


compact:
    pushl %ebp
    mov %esp, %ebp

    pushl %ebx
    pushl %esi
    pushl %edi

    movl 8(%ebp), %esi
    movl 12(%ebp), %ecx

    xorl %ebx, %ebx
    xorl %edi, %edi

    cmpl $0, %ecx
    jle et_final_compact

et_for:
    movl (%esi,%edi,4), %eax
    cmp $0, %eax
    je et_next

    cmpl %ebx, %edi
    je et_increment

    pushl %ecx

    lea (%esi,%edi,4), %eax
    pushl %eax

    lea (%esi,%ebx,4), %eax
    pushl %eax

    call interschimba
    addl $8, %esp
    popl %ecx

et_increment:
    incl %ebx

et_next:
    incl %edi
    loop et_for

et_final_compact:
    popl %edi
    popl %esi
    popl %ebx
    popl %ebp
    ret


.global main
main:
    pushl n
    pushl $v
    call compact
    addl $8, %esp

et_exit:
    movl $1, %eax
    xorl %ebx, %ebx
    int $0x80

```
