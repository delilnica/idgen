# `idgen` - izdelava enoličnih identifikatorjev

`idgen` je enostavna podstoritev Delilnice, ki ustvarja oznake, pripete
vsakemu fragmentu. Oznake so dolge šest znakov in pridelane naključno.

Za pridobitev oznake služi enostaven GET klic na URL podstoritve. Vrnjen
niz bo dolg točno 6 znakov in na svojem koncu ne bo imel nove vrstice.

`idgen` deluje po principu funkcija-kot-storitev z orodjem OpenFaaS,
v svoji notranjosti pa uporablja Alpine Linux in program `pwgen`.

**URL**: <http://nuks.bertoncelj.eu.org:8080/function/delilnica-idgen>.


## Izgradnja in pogon

`idgen` nadzira [`faasd`](https://github.com/openfaas/faasd), ki se ga
administrira z orodjem `faas-cli`. Namestitev je sledeča:

```
cd
git clone --depth=1 https://github.com/openfaas/faasd
faasd/hack/install.sh
```

`faasd` bi sedaj moral delovati (`systemctl status faasd`).

Sledi izgradnja storitve (pazi na vmešavanje požarnega zidu):

```
cd ~/delilnica/idgen
sudo cat /var/lib/faasd/secrets/basic-auth-password | faas-cli login --password-stdin
faas-cli build -f delilnica-idgen.yml
faas-cli deploy -f delilnica-idgen.yml
```

Pričakujemo odziv `200 OK`. Delovanje preverimo z ukazom
`curl -v http://localhost:8080/function/delilnica-idgen && echo`
