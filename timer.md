# Timer

```c

#include <reg51.h>
sbit led = P1 ^ 0;
void delay();
void main() {
    unsigned int i;
    while (1)
    {
        led = ~led;
        for (i = 0; i < 1000; i++)
            delay();
    }
}

void delay() {
    TMOD = 0x01;
    TH0 = 0xFC;
    TL0 = 0x66;
    TR0 = 1;
    while (TF0 == 0)
        ;
    TR0 = 0;
    TF0 = 0;
}

```


```a
org 0h
mov p0, #00h
test:
    setb p0.1
    acall timer
    clr p0.1
    call timer
    jmp test
timer:
    mov tmod, #01h
    mov th0, #04h
    mov tl0, #04h
    setb tr0
    jnb tr0
    jnb tf0, $
    clr tf0
    ret
end
```

# Timer Mode 2

```c
#include <reg51.h>
sbit led = P1 ^ 0; // LED connected to 1st pin of port P1
void delay();
void main() {
    unsigned int i;
    while (1) {
        led = ~led; // Toggle LED
        for (i = 0; i < 1000; i++)
            delay(); // Call delay
    }
}

void delay() {
    TMOD = 0x02; // Mode2 of Timer0
    TH0 = 0xA2;  // Initial value loaded to Timer
    TR0 = 1;     // Start Timer
    while (TF0 == 0)
        ;    // Polling for flag bit
    TR0 = 0; // Stop Timer
    TF0 = 0; // Clear flag
}
```

```a
org 0h
test:
    mov p1, #00h
    call inter
timer:
    mov tmod, #01h
    mov th0, #04h
    mov tl0, #04h
    setb tr0
    jnb tf0, $
    clr tf0
    ret
inter:
    jnb ie.0, $
    setb p1.0
    call timer
    clr p1.0
    jmp inter
end
```