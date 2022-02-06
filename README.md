# Helsingin Erä-Leijonien nettisivut

Staattiset sivut -> ei tarvetta webhotellille tai julkaisujärjestelmän päivityksille. Minimaalinen, nollasta kyhätty suhteellisen responsiivinen design. Mukana ei ole ainuttakaan JS-kirjastoa. :)

## Kehitysprosessi

Asenna wintersmith ja plugarit.

```bash
$ npm install wintersmith
$ npm install wintersmith-contents
$ npm install wintersmith-sitemap
```

Aja sivua lokaalisti.

```bash
$ npm run preview -- <portti>
```

## Deploy

```bash
$ npm run build
```

Tee push masteriin, niin sivut päivittyvät @ https://eraleijonat.fi/.
