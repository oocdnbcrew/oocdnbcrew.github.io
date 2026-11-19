# Baut alle Seiten der OoC-Hülle (oocdnbcrew.github.io). Ausführen: python _bau.py  – danach git commit + push.
# Jede Seite = Rahmen um eine Google-Web-App (ohne Google-Hinweisbalken). Feste Parameter + alles aus der Adresse wird durchgereicht.
import io, os
D = os.path.dirname(os.path.abspath(__file__)) + '/'
EXEC = {
  'L': 'https://script.google.com/macros/s/AKfycbx552LcTqfXFuHeSxBn1WwPfJy15F6I3NYEInOVAgFdlubQTM0dIbcf8TqJg6ZKuXwdig/exec',
  'K': 'https://script.google.com/macros/s/AKfycbwK4-FEERWvd1Cl60Jf-xxvhFnpdp99utJSITKwSqn7WCsE-QO1Qe26vRXTneKgNMM_/exec',
  'F': 'https://script.google.com/macros/s/AKfycbyaWBpl5r15zo1fiaNOlAWwAo3I6nUwL5EoqW_i1iSXLGvbCC1D9nYrSeCem9sa3KR8vQ/exec',
}
# Pfad -> (App, feste Parameter, Titel). '' = Startseite.
SEITEN = {
  '':                    ('L', '', 'Out of Control'),
  'l':                   ('L', '', 'Out of Control'),
  'k':                   ('K', '', 'OoC Getränke'),
  'f':                   ('F', '', 'Out of Control – Photos'),
  'dnb-crew-all-infos':  ('L', '', 'Out of Control'),
  'links-qr':            ('L', 'src=qr', 'Out of Control'),
  'links-admin':         ('L', 'admin=1', 'OoC Infomanagement'),
  'hub':                 ('L', 'hub=1', 'OoC Zentrale'),
  'kassenbuch':          ('L', 'kb=1', 'OoC Kassenbuch'),
  'artist-archive':      ('L', 'artists=1', 'OoC Artist-Archiv'),
  'artist-upload':       ('L', 'djs=1&k=rbt2ds7ctp', 'Out of Control – Artist Upload'),
  'gig-calendar':        ('L', 'gigs=1', 'OoC Gig-Kalender'),
  'gig-calendar-crew':   ('L', 'gigcrew=1&k=fkmwpj4r4r', 'OoC Gig-Kalender'),
  'press-kit':           ('L', 'press=1', 'Out of Control – Press'),
  'micronox':            ('L', 'press=1&dj=Micronox&src=presskit', 'Micronox – Press'),
  'promo-material':      ('L', 'promo=1', 'OoC Promo-Material'),
  'promo-for-artists':   ('L', 'promo=1&k=ts978u79b7', 'Out of Control – Promo'),
  'promoters-worldwide': ('L', 'vs=1', 'OoC Veranstalter'),
  'volunteers':          ('L', 'helfer=alle', 'Out of Control – Volunteers'),
  'volunteers-admin':    ('L', 'vol=1', 'OoC Volunteers'),
  'volunteer-events':    ('L', 'helfer=gruppe-andere', 'Out of Control – Volunteers'),
  'volunteer-kabelsalat':('L', 'helfer=gruppe-kabelsalat', 'Kabelsalat – Volunteers'),
  'volunteer-openair':   ('L', 'helfer=gruppe-openair', 'Out of Control – Volunteers'),
  'posters':             ('L', 'helfer=gruppe-plakate', 'Out of Control – Posters'),
  'drinks-manager':      ('K', '', 'OoC Getränke'),
  'drinks-bar-1':        ('K', 'theke=Theke%201', 'Theke 1'),
  'drinks-bar-2':        ('K', 'theke=Theke%202', 'Theke 2'),
  'drinks-bar-3':        ('K', 'theke=Theke%203', 'Theke 3'),
  'photo-upload':        ('F', '', 'Out of Control – Share your photos'),
  'picture-gallery':     ('F', 'galerie=1', 'Out of Control – Gallery'),
  'photo-admin':         ('F', 'admin=1', 'Foto-Admin'),
}
SEITE = '''<!doctype html>
<html lang="de">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#000000">
<meta name="robots" content="noindex">
<link rel="preconnect" href="https://script.google.com">
<link rel="preconnect" href="https://script.googleusercontent.com">
<link rel="dns-prefetch" href="https://lh3.googleusercontent.com">
<title>%(titel)s</title>
<meta property="og:title" content="%(titel)s">
<meta property="og:image" content="https://oocdnbcrew.github.io/icon.jpg">
<link rel="icon" href="/icon.jpg">
<link rel="apple-touch-icon" href="/icon.jpg">
<style>
  html, body { margin: 0; height: 100%%; background: #000; overflow: hidden; }
  iframe { position: fixed; inset: 0; width: 100%%; height: 100%%; border: 0; display: block; background: #000; }
</style>
</head>
<body>
<!-- Out of Control: Rahmen um die Google-Web-App (ohne Google-Hinweisbalken). Inhalt + Daten kommen weiter von Google. -->
<iframe id="app" title="%(titel)s" allow="clipboard-read; clipboard-write; camera; microphone; fullscreen" allowfullscreen></iframe>
<script>
  var fest = '%(fest)s';
  var q = location.search.replace(/^\\?/, '').replace(/(^|&)h=1(?=&|$)/g, '').replace(/^&/, '');
  var alle = [fest, q, 'h=1'].filter(function (x) { return x; }).join('&');
  document.getElementById('app').src = '%(exec)s?' + alle + location.hash;
  // 18.11.2026: Runterziehen in der App -> Nachricht -> ganze Seite neu laden (wie Chrome-Aktualisieren)
  window.addEventListener('message', function (e) {
    var o = String(e.origin || '');
    if (o.slice(-22) !== '.googleusercontent.com' && o !== 'https://script.google.com') return;
    if (e.data && e.data.ooc === 'neuladen') location.reload();
  });
</script>
</body>
</html>
'''
for pfad, (app, fest, titel) in SEITEN.items():
    ordner = D + pfad + ('/' if pfad else '')
    os.makedirs(ordner, exist_ok=True)
    io.open(ordner + 'index.html', 'w', encoding='utf-8', newline='\n').write(SEITE % {'titel': titel, 'fest': fest, 'exec': EXEC[app]})
io.open(D + '404.html', 'w', encoding='utf-8', newline='\n').write(
  '<!doctype html><html lang="de"><head><meta charset="utf-8"><meta name="robots" content="noindex"><title>Out of Control</title>'
  '<meta http-equiv="refresh" content="0; url=/"></head><body style="background:#000"></body></html>\n')
print(len(SEITEN), 'Seiten gebaut')
