---
title: Home
sections:
- type: heroblock
  template: heroblock
  section_id: hero
  component: hero_block.html
  content: This section can contain a subtitle or tagline. The recommended length
    is one to three sentences, but can be changed as you prefer.
  title: ''
  actions: []
- type: contentblock
  template: contentblock
  title: About
  section_id: about
  actions:
  - label: Contact Me
    url: "/contact"
  component: content_block.html
  content: Το Δίκτυο Τεχνών κι Επιστημών-Hocus Photus, είναι μια νεοσύστατη αστική
    μη κερδοσκοπική εταιρία, της οποίας το όραμα είναι η συνένωση και σύμπραξη καλλιτεχνών,
    ερασιτεχνών και επιστημόνων σε παγκόσμια κλίμακα. Προτείνει ειδικά σχεδιασμένες
    δράσεις οι οποίες αποβλέπουν στη δημιουργία πρωτοτύπων ομαδικών εικαστικών έργων
    τα οποία διαμορφώνονται και ολοκληρώνονται συνεργατικά.
  image: ''
- type: postsblock
  template: postsblock
  title: Recent Posts
  section_id: recent-posts
  actions:
  - label: View Blog
    url: blog/index.html
  component: posts_block.html
  num_posts_displayed: 4
- template: heroblock
  component: hero_block.html
  type: heroblock
  title: ''
  section_id: ''
  actions: []
  content: ''
layout: home
menu:
  main:
    weight: 1

---
