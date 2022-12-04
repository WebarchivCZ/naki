# NAKI informační stránka

## Plynulé nasazování
Push do repozitáře vytvoří Docker images webarchiv/vyvoj:naki. 
- Commit do větve main nasadí obsah na [https://app.webarchiv.cz/vyvoj](https://app.webarchiv.cz/vyvoj)
- PR do větve production nasadí docker image 'webarchiv/vyvoj:naki' prvně na
    - [https://app.webarchiv.cz/vyvoj](https://app.webarchiv.cz/vyvoj)
    - a po potvrzení v jenkins na [https://webarchiv.cz/vyvoj](https://webarchiv.cz/vyvoj)