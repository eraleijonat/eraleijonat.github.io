# Helsingin Erä-Leijonien nettisivut

Staattiset sivut -> ei tarvetta webhotellille tai julkaisujärjestelmän päivityksille. Minimaalinen, nollasta kyhätty suhteellisen responsiivinen design. Mukana ei ole ainuttakaan JS-kirjastoa. :)

## Kehitysprosessi

Asenna wintersmith ja plugarit.

```bash
$ npm install wintersmith -g
$ npm install wintersmith-sitemap -g
```

Aja sivua lokaalisti.

```bash
$ wintersmith preview -p <portti>
```

## Deploy

```bash
$ wintersmith build
```

Tee push masteriin, niin sivut päivittyvät @ http://erä-leijonat.fi/.
