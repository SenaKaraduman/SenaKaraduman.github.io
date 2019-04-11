# Assembly Komutları
Merhaba arkadaşlar, bu yazımda sizlere x86 mimarisinde en çok kullanılan assembly komutlarını anlatmaya çalışacağım.

```sh
LDI Rd,k
LDI R16,0x27
LDI R23,56
```
* **LDI** komutu, ile elimizde bulunan k sabitini Rd registerına yükleyebiliriz. Bu işlemlerde R16 ve R24 aralığındaki registerları kullanırız.
> R16 registerına 0x27 hexadecimal değerini yani 39 sayısını atadık. R23 registerına da 56 sayısını atamış olduk.

```sh
ADD Rd,Rs
ADD R25,R9
```
* **ADD** komutu ile iki registerı toplayarak elde ettiğimiz değeri soldaki registerın içinde tutarız.
> Burda R25 ile R9 registerını toplayarak R25 registerının içine değeri atarız.

```sh
SUB Rd,Rs
SUB R25,R9
```
* **SUB** komutu ile soldaki registerın değerinden sağdaki registerın değerini çıkararak elde ettiğimiz değeri soldaki registerın içinde atarız.

```sh
INC Rd
INC R25
```
* **INC** komutu, increment yani registerın değerini 1 arttırır.

```sh
DEC Rd
DEC R25
```
* **DEC** komutu, decrement yani registerın değerini 1 azaltır.

```sh
LDS Rd,addr
LDS R25,0x60
```
* **LDS** komutu ile adreste verilen değeri registera yükleriz.

```sh
STS addr,Rd
STS 0x60,R25
```
* **STS** komutu ile registerın içindeki değeri sol tarafta belirtilen adrese atarız.

## JUMP ve CALL
 **JUMP**: Bu komut ile dallanma gerçekleştiririz. Genellikle döngü ve koşulları sağlamak için kullanırız.
 + **RJMP**: Relative Jump operand değerimiz o anki konumumuza göre değişiklik gösterir. Program Counter değeri PC= PC+ operand+ 1 dir.
 + **JMP**: PC= operand direk verilen adrese dallanır.
 + **IJMP**: PC= Z, z registerının içinde kayıtlı olan adrese dallanır.
 
 **CALL**: Komutu ile de fonksiyon çağırırız.
 > İşlemci talimatları sırayla birbiri ardına yürütür. Ama bazen bunu istemeyiz ve JUMP ve CALL komutlarını kullanırız. 

### Koşullu Dallanma Komutları
* **BRNE** komutu, not equal yani bu komuttan önce yaptığımız işlemdeki işlemin sonucu 0 'dan farklı ise Zero flagi Z=0 olur ve dallanma gerçekleşir. 
```sh
BRNE NEXT
```
* **BRCC** komutu, carry clear yani elimizde elde bitimiz yoksa C=0 ise dallanma gerçekleşir.
```sh
BRCC L1
```
* **BRCS** komutu, carry set yani elimizde elde bitimiz varsa C=1 ise dallanma gerçekleşir.
```sh
BRCS L1
```


 ```sh
 SBI PORTD, 0
 ```
* **SBI** komutu Port 'un ilgili bitini 1 yapar.
```sh
CBI PORTD, 0
```
* **CBI** komutu Port 'un ilgili bitini 0 yapar.

 ```sh
 SBIC PORTD, 0
 ```
* **SBIC** komutu, Port 'un ilgili bitine bakar ve o bit 0 ise bir sonraki komutu işletmez.
 ```sh
SBIS PORTD, 0
```
* **SBIS** komutu, Port 'un ilgili bitine bakar ve bu bit 1 ise bir sonraki komutu işletmez.
 
* **NOP** komutu, bir şey yapmaz program counter 'ın değerini 1 arttırır. İşlemciyi yorar.
* **COM** komutu, registerının değerinin 1 tümleyenini alır.
* **NEG** komutu, registerının değerinin 2 tümleyenini alır.
#### CP Karşılaştırma Komutları
Bu komutlar registerların içeriğini değiştirmez. Karşılaştırma işlemlerinde kullanılır.
```sh
CP Rd,Rr ; Rd-Rr
CPC Rd,Rr ; Rd-Rr-C
CPI Rd,k ; Rd-k
CPSE Rd,Rr
```
* **CPSE** komutu, Rd ve Rr registerlarının eşitliğine bakar registerlar eşit ise bir sonraki komutu işletmez.

* **CLC** komutu, carry bitini doğrudan 0 yapar.
* **SEC** komutu, carry bitini doğrudan 1 yapar.
* **MOV** komutu, iki registerın içeriğini birbirine kopyalamamızı sağlar.

```sh
MOV Rd,Rr
```
* **SWAP** komutu, elimizdeki 8 bitlik sayının nibble(8 bitlik sayının, 4 bitlik kısımlarına denir.) yer değiştirmesini sağlar.
```sh
LDI R16,0xAB
SWAP R16
```
> R16 registerımızın yeni değeri 0xBA olmuştur.

```sh
SBRC R0,7
```
* **SBRC** komutu, registerın belirtilen bitine bakar o bit 0 ise bir sonraki komut atlanır. R0 registerının 7. biti 0 ise bir sonraki komutu atlar.
```sh
SBRS R0,7
```
* **SBRS** komutu, registerın belirtilen bitine bakar o bit 1 ise bir sonraki komut atlanır. R0 registerının 7. biti 1 ise bir sonraki komutu atlar.

```sh
LDI R16,0xAB
SBR R16,0xF0
```
* **SBR** komutu, registerın belirtilen bitlerini set etmemize 1 yapmamıza yarar.
> R16 registerının yeni içeriği 0xFB olmuştur.

```sh
LDI R16,0xAB
CBR R16,0xF0
```
* **CBR** komutu, registerın belirtilen bitlerini clear etmemize 0 yapmamıza yarar.
> R16 registerının yeni içeriği 0x0B olmuştur.
* **ADC** komutu, 2 registerın içeriklerini toplar ve önceki işlemlerden elimizde carry varsa, carry bitini de ekler.
*  **SBC** komutu, 2 registerın içeriklerini çıkarır ve önceki işlemlerden elimizde carry varsa, carry bitini de çıkarır.

* **EOR** komutu, iki register ile XOR işlemi yapar.
```sh
EOR R16
```
> Şeklinde bir yazım olursa registerı kendi ile XOR lamış oluruz ve registerın içeriği 0 olur.

Yazım burada bitti okuduğunuz için teşekkür ederim :) Yanlış olduğunu düşündüğünüz veya anlamadığınız bir yer olursa bana sorabilirsiniz :))







