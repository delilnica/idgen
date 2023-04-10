# `idgen` - izdelava enoličnih identifikatorjev

`idgen` je enostavna podstoritev Delilnice, ki ustvarja oznake, pripete
vsakemu fragmentu. Oznake so dolge šest znakov in pridelane naključno.

Za pridobitev oznake služi enostaven GET klic na URL podstoritve. Vrnjen
niz bo dolg točno 6 znakov in na svojem koncu ne bo imel nove vrstice.

`idgen` deluje po principu funkcija-kot-storitev (FaaS) z orodjem OpenFaaS,
v svoji notranjosti pa uporablja Alpine Linux in program `pwgen`.

**URL** (delovanje ni zagotovljeno): 
<http://nuks.bertoncelj.eu.org:8080/function/delilnica-idgen>.

