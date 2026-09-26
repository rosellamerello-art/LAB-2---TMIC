.include "m328pdef.inc"
.cseg
.org 0x0000
rjmp RESET
RESET:
; Stack
ldi r16, HIGH(RAMEND)
out SPH, r16
ldi r16, LOW(RAMEND)
out SPL, r16
; LEDs 0-5: D2-D7 = PD2-PD7
sbi DDRD, PD2
sbi DDRD, PD3
sbi DDRD, PD4
sbi DDRD, PD5
sbi DDRD, PD6
sbi DDRD, PD7
; LEDs 6-7: D8-D9 = PB0-PB1
sbi DDRB, PB0
sbi DDRB, PB1
; Todo apagado
ldi r16, 0
out PORTD, r16
out PORTB, r16
; USART 9600 baud - 8N1
ldi r16, 0
sts UBRR0H, r16
ldi r16, 103
sts UBRR0L, r16
; Solo receptor
ldi r16, (1<<RXEN0)
sts UCSR0B, r16
ldi r16, (1<<UCSZ01)|(1<<UCSZ00)
sts UCSR0C, r16
MAIN:
rcall USART_RX
cpi r16, 0
breq LED0
cpi r16, 1
breq LED1
cpi r16, 2
breq LED2
cpi r16, 3
breq LED3
cpi r16, 4
breq LED4
cpi r16, 5
breq LED5
cpi r16, 6
breq LED6
cpi r16, 7
breq LED7
rjmp MAIN
APAGAR:
push r16
ldi r16, 0
out PORTD, r16
out PORTB, r16
pop r16
ret
LED0:
rcall APAGAR
sbi PORTD, PD2
rjmp MAIN
LED1:
rcall APAGAR
sbi PORTD, PD3
rjmp MAIN
LED2:
rcall APAGAR
sbi PORTD, PD4
rjmp MAIN
LED3:
rcall APAGAR
sbi PORTD, PD5
rjmp MAIN
LED4:
rcall APAGAR

sbi PORTD, PD6
rjmp MAIN
LED5:
rcall APAGAR
sbi PORTD, PD7
rjmp MAIN
LED6:
rcall APAGAR
sbi PORTB, PB0
rjmp MAIN
LED7:
rcall APAGAR
sbi PORTB, PB1
rjmp MAIN
USART_RX:
ESPERAR_RX:
lds r17, UCSR0A
sbrs r17, RXC0
rjmp ESPERAR_RX
lds r16, UDR0
ret
