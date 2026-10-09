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
