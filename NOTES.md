ΣΗΜΕΙΩΣΕΙΣ – hocusphotus.com (ενημέρωση Οκτώβριος 2026)

ΣΤΟΙΧΕΙΑ
- Site: https://hocusphotus.com (Jekyll 3.8, θέμα Stackbit Fresh)
- GitHub: achillesn/cool-spinach, branch master (δημόσιο repo)
- Hosting & DNS: Netlify. Το domain είναι αγορασμένο στο GoDaddy,
  αλλά το DNS διαχειρίζεται το Netlify.
- CMS: Sveltia, https://hocusphotus.com/admin/

ΓΕΝΙΚΟΙ ΚΑΝΟΝΕΣ
- Κάθε commit (GitHub ή Sveltia) κάνει πλέον αυτόματα deploy.
  Αν μια αλλαγή δεν φαίνεται: GitHub (έγινε commit;) → Netlify Deploys
  (Published;) → αν όχι: Trigger deploy → ιδιωτικό παράθυρο (cache).
- Ο editor του GitHub χαλάει τις εσοχές όταν επικολλάς YAML πολλών
  γραμμών. Λύσεις: αντικατάσταση ΟΛΟΥ του αρχείου (Cmd+A, Delete,
  επικόλληση) ή ρυθμίσεις σε μία γραμμή { ... }.
- Μέσα σε { ... } ΜΗΝ βάζεις κόμμα σε ετικέτες χωρίς εισαγωγικά.
- Αρχεία .md: στο GitHub πάτα "Code" (όχι Preview) για να δεις τον κώδικα.
- Εικόνες: το όνομα ΔΕΝ πρέπει να ξεκινά με _ (το Jekyll τις αγνοεί).
  Προσοχή σε .jpg / .JPG (είναι διαφορετικά). Έλεγχος:
  https://hocusphotus.com/images/ΟΝΟΜΑ
- Ημερομηνία άρθρου: το Jekyll δεν δημοσιεύει μελλοντικές. Το Netlify
  μετράει σε UTC (3 ώρες πίσω). Βάζε ώρα 00:00 ή χθεσινή ημερομηνία.
- github.dev (πάτα . στο repo): μαζική αναζήτηση/αντικατάσταση.
  ΠΡΟΣΟΧΗ: αν βγει μήνυμα 50 MB, η αναζήτηση μπορεί να είναι ελλιπής.

ΙΣΤΟΡΙΚΟ ΕΠΙΛΥΣΗΣ
- Το Forestry (παλιό CMS) έκλεισε το 2022 → αντικαταστάθηκε με Sveltia.
- Παλιότερα είχε ανέβει στο repo το χτισμένο site ("restore full build").
  Σβήσαμε τα παγωμένα αντίγραφα: studium/, about/, contact/,
  hocus-contents/, blog/index.html, posts/, index.html (ρίζα).
  ΜΗΝ ξανανεβάσεις ποτέ χτισμένο site (_site ή .html με όλο το μενού).
  Μένουν παγωμένα (εκτός μενού): feed.xml, style-guide/.
- Build: netlify.toml command = "bundle exec jekyll build".
  Αν σπάσει με σφάλμα Ruby/jekyll-menus:
  RUBY_VERSION=2.7.8 και gem "ffi", "< 1.17".

CMS (Sveltia) – admin/config.yml
- Login: fine-grained token GitHub, Only select repositories →
  cool-spinach, Contents: Read and write. Όταν λήξει, φτιάχνεις νέο.
- Αριστερή στήλη = ΦΑΚΕΛΟΙ του _posts (με ανακατεμένα άρθρα).
  Το όνομα που φαίνεται αλλάζει στο label: (ΟΧΙ name: ή folder:).
  Για να βρεις άρθρο: αναζήτηση του Sveltia (πάνω πάνω).
  Νέα άρθρα: καλύτερα στο "Γενικά (διάφορα)". Η κατηγορία ορίζεται
  από το Category, όχι από τον φάκελο.
- Ενότητες: Κατηγορίες (Blogus Contentus), Σελίδες (About,
  Hocus Contents, Upcoming Events), Αρχική σελίδα (index.md).
- Τα name στο config.yml πρέπει να είναι μοναδικά.
- Παλιά άρθρα με HTML: επεξεργασία καλύτερα σε λειτουργία Markdown.
- Excerpt = σύντομη περιγραφή στις λίστες. Κείμενο = πλήρες άρθρο.

ΜΕΝΟΥ
- Σελίδες στο μενού: το όνομα = Title της σελίδας. Για άλλο όνομα μόνο
  στο μενού: στο .md (GitHub), κάτω από menu: main: weight: →
  title: ΟΝΟΜΑ (με τα ίδια κενά). Π.χ. about.md: HOCUS ABOUTUS.
- Εξωτερικά/επιπλέον links: _data/menus.yml (weight = σειρά,
  δεκαδικά επιτρέπονται). Photo Games → https://photogames.eu/ (5),
  Αναζήτηση → /search/ (6.5).
- Εξωτερικά links ανοίγουν σε νέα καρτέλα (_includes header, '://').
- Tagline κάτω από το logo: _config.yml → header → tagline.
- Footer (© χρονιά): _config.yml (footer content) ή _includes/footer.html.

BLOGUS CONTENTUS (αυτόματα περιεχόμενα)
- hocus-contents.md → layout: contents → _layouts/contents.html
- Οι κατηγορίες ρυθμίζονται ΑΠΟ ΤΟ SVELTIA:
  Κατηγορίες (Blogus Contentus) → Λίστα κατηγοριών
  (αρχείο _data/contents.yml, ξεκινά με groups:)
- Πεδία κάθε κατηγορίας:
  Όνομα = αυτό που διαλέγεις στο Category των άρθρων
  Θέση = σειρά στη σελίδα (1 = πρώτη, δεκαδικά για ενδιάμεσα, π.χ. 5.5)
  Περιγραφή = π.χ. Hocus PoetUs (μικρά πλάγια δίπλα στον τίτλο)
  Αυτόματη αναγνώριση = λέξεις από τίτλο/διεύθυνση/φάκελο (κόμμα).
    Για νέες κατηγορίες: κενό.
  Ταξινόμηση = date (σειρά δημοσίευσης) ή title (π.χ. e-PhotoGames)
  Αρίθμηση = 1, 2, 3… στη λίστα
  Κρυφή = δεν εμφανίζεται στο Contents (StudiUm, News, Post)
- ΝΕΑ ΚΑΤΗΓΟΡΙΑ: Λίστα κατηγοριών → Add (στο τέλος) → Όνομα, Θέση,
  Περιγραφή → Save. Εμφανίζεται στο Category των άρθρων και στη
  σελίδα μόλις έχει 1 άρθρο.
- ΜΗΝ αλλάζεις τη σειρά των κουτιών στη λίστα: η θέση στη σελίδα
  ορίζεται μόνο από τη "Θέση". Η σειρά των κουτιών είναι η
  προτεραιότητα της αυτόματης αναγνώρισης.
- Ένα άρθρο πάει: (1) στην κατηγορία του Category του, αλλιώς
  (2) στην πρώτη κατηγορία της λίστας που ταιριάζει η αναγνώριση,
  αλλιώς (3) στα "Διάφορα · Hocus RantomUs".
- Category των άρθρων: πεδίο "relation" που διαβάζει τη Λίστα κατηγοριών.
  Αν ποτέ χαλάσει, εναλλακτικά: widget: select με options: [...].
- Σειρά: 1 Φωτογραφικά Παιχνίδια - Live, 2 Εκθέσεις, 3 e-PhotoGames,
  4 Παράλληλοι Κόσμοι, 5 Virtual Connections, 6 Virtual Connections III,
  7 ΕΙΚΟΝΟΛΟΓΟΙ, 8 Ελεγεία της Ανόδου, 9 Συνοδευτική Επιστολή,
  10 Στη Ρωγμή του Χρόνου, 11 Το καπάκι της Αβύσσου,
  12 Κορώνα - Γράμματα, 13 Αναζητώντας τη χαμένη Μαγεία,
  14 Το Μάτι του Κύκλωπα, 15 Iconic Hacks, 16 Movies, 17 Music,
  18 Sing Your Soul Out, τέλος: Διάφορα.

UPCOMING EVENTS
- studium.md → _layouts/studium.html: τίτλος, υπότιτλος, εικόνα,
  κείμενο από το Sveltia + λίστα άρθρων με Category: StudiUm
  (ακριβώς έτσι, κεφαλαία S και U).

ΑΝΑΖΗΤΗΣΗ
- search.json (ευρετήριο, αυτόματο) + search.html (σελίδα /search/).
- Αγνοεί τόνους/κεφαλαία. Τίτλος, υπότιτλος, εικόνα (img_path) και
  κείμενο (σε <p><em>…</em></p>) στο search.html (GitHub, όχι Sveltia,
  γιατί έχει κώδικα).

PHOTOGAMES LINKS
- Τα παλιά photogames.tk μέσα στα άρθρα γίνονται αυτόματα photogames.eu
  κατά το build: _layouts/body.html →
  {{ content | replace: 'photogames.tk', 'photogames.eu' }}

ΜΕΤΑΦΡΑΣΗ
- Κουμπί EN/ΕΛ πάνω δεξιά (Google Translate, translate.goog):
  στην αρχή του header στο _includes.
- _layouts/base.html: lang="el", αφαιρέθηκε το notranslate.
- Η αγγλική εκδοχή ενημερώνεται με καθυστέρηση (cache της Google).
  Λέξεις με λατινικούς χαρακτήρες (HOCUS ABOUTUS) δεν μεταφράζονται.

ΣΤΑΤΙΣΤΙΚΑ
- GoatCounter: https://hocusphotus.goatcounter.com (δωρεάν, χωρίς cookies)
- Κώδικας: πριν το </body> στο _layouts/base.html.

EMAIL info@hocusphotus.com
- Λήψη: ImprovMX (δωρεάν), alias info@ → προσωπικό Gmail.
- Gmail φίλτρο: To: info@hocusphotus.com → Never send to Spam.
- Αποστολή από Gmail: "Send mail as" μέσω Brevo (δωρεάν, 300/ημέρα)
  SMTP: smtp-relay.brevo.com, port 587, TLS
  Username: SMTP Login του Brevo (...@smtp-brevo.com)
  Password: SMTP key (Brevo → SMTP & API → SMTP). Αν χαθεί, νέο.
- Αποστολή από Yahoo: info@ ως "Send-only email address"
  (Settings → Mailboxes). Χωρίς DKIM του domain. Αν αρχίσουν
  προβλήματα παράδοσης, στέλνε από το Gmail.
- smtp.gmail.com ΔΕΝ αρκεί: η Yahoo απορρίπτει χωρίς DKIM του domain.

DNS (Netlify → Domain management → hocusphotus.com → DNS)
- Οι εγγραφές δεν επεξεργάζονται: Delete και Add new record.
- ΜΗΝ σβήσεις τις 2 εγγραφές τύπου NETLIFY (είναι το site).
  MX   @  mx1.improvmx.com (10)
  MX   @  mx2.improvmx.com (20)
  TXT  @  v=spf1 include:spf.improvmx.com include:spf.brevo.com include:_spf.google.com ~all
  TXT  @  brevo-code:84fe9d2d162bda343ea1f6649d567bf3
  CNAME brevo1._domainkey → b1.hocusphotus-com.dkim.brevo.com
  CNAME brevo2._domainkey → b2.hocusphotus-com.dkim.brevo.com
  CNAME k2._domainkey → dkim2.mcsv.net   (Mailchimp)
  CNAME k3._domainkey → dkim3.mcsv.net   (Mailchimp)
  TXT  _dmarc  v=DMARC1; p=none; rua=mailto:rua@dmarc.brevo.com
- ΜΟΝΟ μία εγγραφή v=spf1 και ΜΟΝΟ μία _dmarc. Νέες υπηρεσίες
  προστίθενται ως include: στην ίδια γραμμή SPF.

NEWSLETTER (Mailchimp)
- Domain hocusphotus.com Authenticated.
- Αποστολέας: Hocus Photus <info@hocusphotus.com>
  (Audience → Settings → Audience name and defaults)
- Footer & permission reminder (δίγλωσσο): Audience → More options →
  Audience settings → Required email footer content.

ΕΚΚΡΕΜΟΤΗΤΕΣ (προαιρετικά)
- Substack στα social: χρειάζονται _data/social.json,
  _includes/social.html και η διεύθυνση του Substack
  (δικό του εικονίδιο SVG, η βιβλιοθήκη εικονιδίων δεν το έχει).
- Λάθος διεύθυνση στα social: _data/social.json (αλλάζεις μόνο μέσα
  στα εισαγωγικά).
- feed.xml παγωμένο (RSS δεν ενημερώνεται).
- © στο footer → αυτόματη χρονιά ({{ 'now' | date: '%Y' }}).
- Διπλό άρθρο 2022ii_05_4. Άρθρο "06." χωρίς πλήρη τίτλο.
- Canonical URL με τιμή εικόνας σε κάποια παλιά άρθρα.
