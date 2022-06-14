# Serial Transmit

```c
#include <reg51.h>
void main() {
    TMOD = 0x20;
    TH1 = 0xFD; // Baud rate = 9600
    SCON = 0x50;
    TR1 = 1;
    while (1) {
        SBUF = 'A';
        while (TI == 0);
        TI = 0;
    }
}

```


```a
org 0h
mov scon, #50h
mov tmod, #20h
mov th1, #-3
setb tr1
repeat:
    mov sbuf, #"Y"
    acall tran
    mov sbuf, #"E"
    acall tran
    mov sbuf, #"S"
    acall tran
    sjmp repeat
tran:
    jnb ti, $
    clr ti
    ret
end
```


# Serial Receive

```c
#include <reg51.h>
void main() {
    unsigned char t; // Declare here first else results error in Keil
    TMOD = 0x20;
    TH1 = 0xFD; // Baud rate = 9600
    SCON = 0x50;
    TR1 = 1;
    while (1) {
        while (RI == 0);
        t = SBUF;
        P1 = t;
        RI = 0;
    }
}
```


``` a
org 0h
mov scon, #50h
mov p0, #00h
mov tmod, #20h
mov th1, #-3
setb tr1
here:
    jnb ri, $
    mov a, sbuf
    mov p0, a
    clr ri
    sjmp here
en
```