---
date: "2022-10-24"
sections:
- block: about.avatar
  content:
    text: null
    username: admin
  id: about
- block: collection
  content:
    filters:
      featured_only: false
      folders:
      - publication
    title: Publicaciones
  design:
    columns: "2"
    view: card
  id: featured
- block: portfolio
  content:
    buttons:
    - name: All
      tag: '*'
    - name: Deep Learning
      tag: Deep Learning
    - name: Other
      tag: Demo
    default_button_index: 0
    filters:
      folders:
      - project
    title: Proyectos
  design:
    columns: "1"
    flip_alt_rows: false
    view: showcase
  id: projects
- block: accomplishments
  content:
    date_format: Jan 2006
    items:
    - certificate_url: https://www.udemy.com/certificate/UC-fba3a144-48dd-4715-9107-47ec7a76c77c/
      date_end: ""
      date_start: "2023-01-22"
      description: ""
      organization: Udemy
      organization_url: https://www.udemy.com/
      title: Learn Data Science and Machine Learning with R from A-Z Course
      url: ""
    - certificate_url: https://www.udemy.com/certificate/UC-b9e93965-eb71-4da8-ae4a-b7986c5cb80b/
      date_end: ""
      date_start: "2021-01-01"
      description: ""
      organization: Udemy
      organization_url: https://www.udemy.com/
      title: Adobe Illustrator CC - Essentials Training Course.
      url: ""
    - certificate_url: uploads/chea-certificado.pdf
      date_end: "2021-09-08"
      date_start: "2021-07-19"
      description: ""
      organization: Chea-UdelaR-CSIC
      organization_url: https://www.chea.edu.uy/
      title: Manejo y uso de animales no tradicionales en investigación.
      url: ""
    - certificate_url: https://www.datacamp.com/statement-of-accomplishment/course/19d39f6315199339c467c5fb68b66882c3ea1ac3
      date_end: ""
      date_start: "2021-12-06"
      description: ""
      organization: DataCamp
      organization_url: https://www.udemy.com/
      title: Introduction to R
      url: ""
    - certificate_url: uploads/alianza-certificado.pdf
      date_end: ""
      date_start: "2016-12-21"
      description: ""
      organization: Alianza
      organization_url: https://www.alianza.edu.uy/es/
      title: Teens high-intermediate course - Independent User at B2
      url: ""
    subtitle: null
    title: Logros
  design:
    columns: "2"
  id: accomplishments
- block: contact
  content:
    address:
      city: Canelones
      region: Uruguay &#x1F1FA;&#x1F1FE;
    contact_links:
    - icon: twitter
      icon_pack: fab
      link: https://twitter.com/nicof_7
      name: "@nicof_7"
    email: nfernandez@fcien.edu.uy
    subtitle: null
    text: ""
    title: Contacto
  design:
    columns: "2"
  id: contact
title: null
type: landing
---
