---
title: 'Home'
date: 2024-11-18
type: landing
sections:
  - block: collection
    content:
      title: 'Flows of Mountain, Depths of Time'
    design:
      background:
    # Choose a color such as from https://html-color-codes.info
        image:
      # Name of image in `assets/media/`.
          filename: background.jpg
          filters:
              # Darken the image? Range 0-1 where 1 is transparent and 0 is opaque.
              brightness: 0.6
              size: cover
              position: center
  - block: resume-biography
    design:
      spacing:
        padding: [0, 0, 0, 0]
      biography:
        style: 'text-align: justify; font-size: 0.8em;'
  - block: collection
    content:
      title: 'Recent Update'
      filters:
        folders:
          - blog
    design:
      spacing:
        padding: ['3rem', 0, '6rem', 0]
---
