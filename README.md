# DeepSpeechLV

Mozilla DeepsSpeech latviešu valodas atpazīšanas modelis.

Modeļa datnes pieejams https://drive.google.com/drive/folders/1o_tu-d5T4OWi8xyfgd_KYv29SXF8Gfw2 

Lai atbalstītu latviešu valodas runas atpazīšau, ierakstiet savu balsi https://commonvoice.mozilla.org/lv


## Izmantošana

Šo modeli latviešu valodas runas atpazīšanai var izmantot dažādos veidos un sistēmās. 
Viena no sistēmām ir [Rhasspy](https://rhasspy.readthedocs.io), ko var izmantot [Home Assistant](https://www.home-assistant.io/)
gudrās mājas un automatizācijas rīkā. 

Testa režīmā Rhasspy ar latviešu valodas atbalstu var palaist sekojoši:

1. Lejupielādējiet `rhasspy-profile` ar latviešu valodas atbalstu
```commandline
git clone git@github.com:raivisdejus/rhasspy-profile.git
```
2. Izveidojiet `docker-compose.yml` datni ar Rhasspy konfigurāciju.
   Ņemiet vērā, ka iespējams jums šajā konfigurācijā `~/rhasspy-profile` jāsamaina pret vietu, 
   kur iepriekšējā soļa komanda saglabāja profila datnes.
```commandline
rhasspy:
    image: "rhasspy/rhasspy"
    container_name: rhasspy
    restart: unless-stopped
    volumes:
        - "$HOME/.config/rhasspy/profiles:/profiles"
        - "/etc/localtime:/etc/localtime:ro"
        - "~/rhasspy-profile:/usr/lib/rhasspy/rhasspy-profile"
    ports:
        - "12101:12101"
    devices:
        - "/dev/snd:/dev/snd"
    command: --user-profiles /profiles --profile lv
```
3. Palaidiet Docker konteinerus
```commandline
docker-compose up
```
4. Rhasspy būs pieejams http://localhost:12101/
5. Ieslēdziet visus noklusētos jeb rekomendētos servisus.

Sīkāka informācija par Phasspy https://rhasspy.readthedocs.io/en/latest/#learn-more