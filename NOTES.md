ΣΥΝΟΨΗ ΕΠΙΛΥΣΗΣ – hocusphotus.com (Οκτώβριος 2026)

ΣΤΟΙΧΕΙΑ
- Site: https://hocusphotus.com (Jekyll 3.8, θέμα Stackbit Fresh)
- GitHub: achillesn/cool-spinach, branch master (δημόσιο repo)
- Hosting: Netlify
- CMS: Sveltia, στο https://hocusphotus.com/admin/

ΣΥΜΠΤΩΜΑΤΑ
1. Το /admin/ δεν λειτουργούσε από το 2022 (Forestry.io, έκλεισε).
2. Οι αλλαγές δεν φαίνονταν στο site.

ΑΙΤΙΕΣ
1. Το admin/index.html ήταν του Forestry.
2. Πέρσι ανέβηκε στο repo ολόκληρο το χτισμένο site (commit «Fix site
   structure: restore full build with images and styles»). Τα παγωμένα
   HTML αντίγραφα έκρυβαν τις ζωντανές σελίδες στις ίδιες διευθύνσεις.

ΤΙ ΑΛΛΑΞΑΜΕ
Α. Build (Netlify)
   - netlify.toml: command = "bundle exec jekyll build", απλά εισαγωγικά.
   - Το build πέτυχε χωρίς αλλαγές σε Gemfile ή Ruby. ΔΕΝ πειράξαμε
     Gemfile, Gemfile.lock ή RUBY_VERSION. Αν κάποτε σπάσει το build με
     σφάλμα Ruby/jekyll-menus, δες την προηγούμενη σύνοψη:
     RUBY_VERSION=2.7.8 και gem "ffi", "< 1.17".
   - Αν ένα commit δεν ξεκινά deploy: Netlify → Deploys → Trigger deploy.

Β. CMS
   - admin/index.html: φορτώνει το Sveltia από unpkg.
   - admin/config.yml: backend github, media_folder images.
     Συλλογές: μία ανά υποφάκελο του _posts (ICONIC HACKS, NEVI, RANDOM,
     StudiUm κ.λπ.), «Σελίδες» (about.md, hocus-contents.md, studium.md),
     «Αρχική σελίδα» (index.md, ενότητες contentblock/postsblock/heroblock).
   - Login: fine-grained token GitHub, Only select repositories →
     cool-spinach, Contents: Read and write. Όταν λήξει, φτιάχνεις νέο.

Γ. Σβήσαμε τα παγωμένα αντίγραφα
   - studium/index.html, about/index.html, contact/index.html,
     hocus-contents/index.html, blog/index.html (ΚΡΑΤΗΣΑΜΕ blog/index.md),
     ολόκληρο τον φάκελο posts/ (ΚΡΑΤΗΣΑΜΕ _posts/), index.html της ρίζας
     (ΚΡΑΤΗΣΑΜΕ index.md).
   - Όλα επαναφέρονται από το History του GitHub αν χρειαστεί.

Δ. Άλλες αλλαγές
   - _data/menus.yml: Photo Games → https://photogames.eu/
   - _includes/ (header): τα εξωτερικά links του μενού ανοίγουν σε νέα
     καρτέλα: {% if item.url contains '://' %} target="_blank" rel="noopener"{% endif %}
   - studium.md: τίτλος «Upcoming Events» (ο τίτλος γίνεται και όνομα στο μενού).

ΠΩΣ ΛΕΙΤΟΥΡΓΟΥΝ ΤΑ ΠΡΑΓΜΑΤΑ
- Upcoming Events (/studium/): δείχνει αυτόματα τα άρθρα με Category
  «studium». Για να μπει/βγει άρθρο, αλλάζεις το Category του.
- Excerpt = σύντομη περιγραφή στις λίστες. Κείμενο = πλήρες άρθρο.
- Date: το Jekyll ΔΕΝ δημοσιεύει άρθρα με μελλοντική ημερομηνία.
  Το Netlify μετράει σε ώρα UTC (3 ώρες πίσω). Αν άρθρο δεν εμφανίζεται,
  βάλε ώρα 00:00 ή χθεσινή ημερομηνία.
- Παλιά άρθρα με HTML: επεξεργασία καλύτερα σε λειτουργία Markdown.

ΛΑΘΗ ΔΡΟΜΟΥ (να αποφευχθούν)
- Ο editor του GitHub χαλάει τις εσοχές όταν επικολλάς YAML πολλών
  γραμμών, και το Sveltia βγάζει «Αδυναμία ανάλυσης του αρχείου ρυθμίσεων».
  Λύσεις: αντικατάσταση ΟΛΟΥ του αρχείου (Ctrl+A, Delete, επικόλληση)
  ή ρυθμίσεις σε μία γραμμή { ... }.
- Τα ονόματα (name) στο config.yml πρέπει να είναι μοναδικά.
- ΜΗΝ ξανανεβάσεις ποτέ χτισμένο site (φάκελο _site ή αρχεία .html
  με όλο το μενού μέσα) στο repo.
- Αν μια αλλαγή δεν φαίνεται: έλεγξε GitHub (έγινε commit;) → Netlify
  (Published;) → ιδιωτικό παράθυρο (cache) → μήπως υπάρχει παγωμένο
  index.html στον φάκελο της σελίδας.

ΕΚΚΡΕΜΟΤΗΤΕΣ (προαιρετικά)
- feed.xml: παγωμένο, το RSS δεν ενημερώνεται.
- style-guide/: παγωμένος φάκελος (υπάρχει και style-guide.md), εκτός μενού.
- Contact, μενού, social, author: εκτός CMS, αλλάζουν από το GitHub.
- Canonical URL: σε κάποια άρθρα έχει τιμή μια εικόνα. Καλό είναι να αδειάσει.
- Παλιά links photogames.tk μέσα σε άρθρα.

EMAIL info@hocusphotus.com (Οκτώβριος 2026)
- DNS: στο Netlify (Domain management → hocusphotus.com → DNS).
  Οι εγγραφές δεν επεξεργάζονται, μόνο Delete και Add new record.
  ΜΗΝ σβήσεις τις 2 εγγραφές τύπου NETLIFY (είναι το site).
- Λήψη: ImprovMX (δωρεάν), alias info@ → προσωπικό Gmail.
  MX: mx1.improvmx.com (10), mx2.improvmx.com (20)
- Αποστολή: Gmail "Send mail as" μέσω Brevo (δωρεάν, 300/ημέρα)
  SMTP: smtp-relay.brevo.com, port 587, TLS
  Username: το SMTP Login του Brevo (...@smtp-brevo.com)
  Password: SMTP key (Brevo → SMTP & API → SMTP). Αν χαθεί, φτιάχνεις νέο.
- Λοιπές εγγραφές DNS:
  TXT  @        v=spf1 include:spf.improvmx.com include:spf.brevo.com include:_spf.google.com ~all
  TXT  @        brevo-code:84fe9d2d162bda343ea1f6649d567bf3
  CNAME brevo1._domainkey → b1.hocusphotus-com.dkim.brevo.com
  CNAME brevo2._domainkey → b2.hocusphotus-com.dkim.brevo.com
  TXT  _dmarc   v=DMARC1; p=none; rua=mailto:rua@dmarc.brevo.com
- Επιτρέπεται ΜΟΝΟ μία εγγραφή v=spf1. Νέες υπηρεσίες προστίθενται
  ως include: στην ίδια γραμμή.
- Smtp.gmail.com ΔΕΝ αρκεί: η Yahoo απορρίπτει χωρίς DKIM του domain.

- - Yahoo: info@ προστέθηκε ως "Send-only email address"
  (Yahoo Mail → Settings → Mailboxes). Στέλνει από διακομιστές Yahoo,
  χωρίς DKIM του domain. Αν αρχίσουν προβλήματα παράδοσης,
  στέλνε από το Gmail (μέσω Brevo).
- Gmail φίλτρο: To: info@hocusphotus.com → Never send to Spam.
  (Χωρίς αυτό, η επιβεβαίωση του Yahoo είχε πάει στα Spam.)

  NEWSLETTER (Mailchimp)
- Domain hocusphotus.com επαληθευμένο (Authenticated) στο Mailchimp.
  DNS: CNAME k2._domainkey → dkim2.mcsv.net
       CNAME k3._domainkey → dkim3.mcsv.net
  (το DMARC υπάρχει ήδη, ΜΗΝ προστεθεί δεύτερο)
- Αποστολέας καμπανιών: Hocus Photus <info@hocusphotus.com>
- Footer & permission reminder (δίγλωσσο): Audience → More options →
  Audience settings → Required email footer content

ΣΤΑΤΙΣΤΙΚΑ (GoatCounter)
- https://hocusphotus.goatcounter.com (δωρεάν, χωρίς cookies)
- Κώδικας: τελευταία γραμμή πριν το </body> στο _layouts/base.html
- Ο παλιός κώδικας Google Analytics (UA) αφαιρέθηκε (δεν λειτουργούσε από 2023).

ΑΛΛΕΣ ΑΛΛΑΓΕΣ ΣΤΟ SITE
- Tagline κάτω από το logo: _config.yml → header → tagline
- Κουμπί EN/ΕΛ πάνω δεξιά (Google Translate): στην αρχή του header
  στο _includes. Στο base.html: lang="el", αφαιρέθηκε το notranslate.
- Νέα εξωτερικά links στο μενού: _data/menus.yml (weight = σειρά).

- - Τα παλιά links photogames.tk μέσα στα άρθρα μετατρέπονται αυτόματα
  σε photogames.eu κατά το build: _layouts/body.html →
  {{ content | replace: 'photogames.tk', 'photogames.eu' }}
