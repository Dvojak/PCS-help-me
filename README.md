# NAT STATIC Pokračování
Zápis z 14.2. 2022
------------------------
***NAT (Network address translation)*** - většinou používá pro přístup více počítačů z lokální sítě do Internetu prostřednictvím jediné veřejné IP adresy 


1. Zapnutí služby pro překlad: (Na hraničním Routeru)
``` 
	ip nat inside source ?
		a) list - používáme když chceme vnitřní adresy do vnější 
					##jaké jsme nadefinovali pravidla?##
				1) <1-199>
					#) 1-99 basic access list  
					(rozlišuje se podle source ip)
						||) interface - ptá se kdo to bude překládat
							<) overload - udělá dynamickou tabulku NATu
							>) <cr> - 
						&&) pool - 
					&) 100- 99 advanced access list
					(rozlišuje podle source ip a destination) 			  
				2) WORD -
				## Mezi nimi není žádný rozdíl ##
		b) static - používáme když chceme vnější do vnitřní
```

c) použili jsme:
```
ip nat inside source list 33 interface g0/0 overload
```
Popis každé části:
 ```	
		ip nat - (překlad)
		inside -  (směr)
		source - 
		list 33 -   (access-list kdo může ven)
		interface g0/0 -(překlad aplikacím na povrch)
		overloaded - Udělá indentifikátory v do sh ip nat !!!!!
```
e) Access-list:
```
	Basic 1-99 - Omezuji Source IP (IP NET)
	Advanced 100-199 - Omezuji Source + Destination (IP/IP NET)
								(Popřípadě TCP/UDP)
```
```
	Access-list 33 ? 
		a) deny - Zakazuje celý blok (dáváme adresu sítě)
			1)A.B.C.D
				#)Wildcard
				&)<cr>
			2)any
			3)host
		b) permit - Povoluje celý blok ()
		c) remark -
		 
```	
Použili jsme  :
```
Access-list 33 deny 192.168.0.0  0.0.1.255
Do sh access-list
Access-list 33 permit any
Do sh access-list
```
Nejspíš to nebude vůbec k něčemu a možně chybné
--------------------------------------------------------------
Nespoléhejte se na to. Dělám to jenom abych dával pořádný pozor.											
				 	
			
