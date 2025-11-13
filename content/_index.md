---
# Leave the homepage title empty to use the site title
title: 'Courses'
publishDate: 2025-09-22
type: landing

design:
  # Default section spacing
  spacing: '6rem'


sections:
  # - block: resume-biography-3
  #   content:
  #     # Choose a user profile to display (a folder name within `content/authors/`)
  #     username: admin
  #     text: ''
  #     # Show a call-to-action button under your biography? (optional)
  #     headings:
  #       about: 'About me'
  #       education: 'Education'
  #       interests: 'Interests'
  #   design:
  #     # Apply a gradient background
  #     css_class: hbx-bg-gradient
  #     # Avatar customization
  #     avatar:
  #       size: medium # Options: small (150px), medium (200px, default), large (320px), xl (400px), xxl (500px)
  #       shape: circle # Options: circle (default), square, rounded
  # - block: resume-biography-3
  #   content:
  #     # Choose a user profile to display (a folder name within `content/authors/`)
  #     username: celmo
  #     text: ''
  #     # Show a call-to-action button under your biography? (optional)
  #     button:
  #       text: die bitch
  #       url: uploads/resume.pdf
  #     headings:
  #       about: I'm such a dick
  #       education: ''
  #       interests: ''
  #   design:
  #     # Apply a gradient background
  #     css_class: hbx-bg-gradient
  #     # Avatar customization
  #     avatar:
  #       size: medium # Options: small (150px), medium (200px, default), large (320px), xl (400px), xxl (500px)
  #       shape: circle # Options: circle (default), square, rounded
  # - block: markdown
  #   content:
  #     title: '📚 My Research'
  #     subtitle: ''
  #     text: |-
  #       Use this area to speak to your mission. I'm a research scientist in the Moonshot team at DeepMind. I blog about machine learning, deep learning, and moonshots.

  #       I apply a range of qualitative and quantitative methods to comprehensively investigate the role of science and technology in the economy.

  #       Please reach out to collaborate 😃
  #   design:
  #     columns: '1'
  # - block: collection
  #   id: papers
  #   content:
  #     title: Featured Publications
  #     filters:
  #       folders:
  #         - publication
  #       featured_only: true
  #   design:
  #     view: article-grid
  #     columns: 2
  # - block: collection
  #   content:
  #     title: Recent Publications
  #     text: ''
  #     filters:
  #       folders:
  #         - publication
  #       exclude_featured: false
  #   design:
  #     view: citation
  # - block: collection
  #   id: talks
  #   content:
  #     title: Recent & Upcoming Talks
  #     filters:
  #       folders:
  #         - event
  #   design:
  #     view: card
  - block: markdown
    content:
      title: '📚 Why this tutorial ?'
      subtitle: ''
      text: |-
        This workshop develops practical competencies in modern research workflows that enhance rigor, transparency, and efficiency. Contemporary scholarship depends on programmable tools and reproducible methods; participants will learn to employ version control ([Git](https://git-scm.com/)), scientific scripting ([Python](https://www.python.org/)), containerization ([Docker](https://www.docker.com/)), and scholarly typesetting ([LaTeX](https://www.latex-project.org/)) to support collaborative and auditable research.

        The workshop does not train software engineers. Its objective is to enable doctoral researchers to:

          - Reduce time lost to environment inconsistency and disorganized project structures
          - Maintain robust version histories and provenance for manuscripts and code (no more `final_v3_revised_REAL_final.tex`)
          - Collaborate effectively through clear review practices and manageable change tracking
          - Reuse configurations, automate routine tasks, and streamline analysis-to-publication pipelines

        Emphasis is placed on a minimal, coherent digital workflow that improves reproducibility and reduces friction in day-to-day research activities throughout the PhD and beyond. Participants will leave with a concise toolkit and evidence-based practices for sustainable, reproducible research.
    design:
      columns: '1'
  
  - block: markdown
    content:
      title: 'Doctoral school support'
      subtitle: ''
      text: |
        This training is organized by the [SIE Doctoral School](https://www.univ-smb.fr/edsie/) of [Université Savoie Mont Blanc (USMB)](https://www.univ-smb.fr/). It is part of SIE’s commitment to equipping doctoral candidates with practical, modern research skills that support rigorous, collaborative, and reproducible work across disciplines. 

    design:
      columns: '1'
  # - block: collection
  #   id: news
  #   content:
  #     title: Recent News
  #     subtitle: ''
  #     text: ''
  #     # Page type to display. E.g. post, talk, publication...
  #     page_type: post
  #     # Choose how many pages you would like to display (0 = all pages)
  #     count: 5
  #     # Filter on criteria
  #     filters:
  #       author: ''
  #       category: ''
  #       tag: ''
  #       exclude_featured: false
  #       exclude_future: false
  #       exclude_past: false
  #       publication_type: ''
  #     # Choose how many pages you would like to offset by
  #     offset: 0
  #     # Page order: descending (desc) or ascending (asc) date.
  #     order: desc
  #   design:
  #     # Choose a layout view
  #     view: card
  #     # Reduce spacing
  #     spacing:
  #       padding: [0, 0, 0, 0]
  # - block: cta-card
  #   demo: true # Only display this section in the Hugo Blox Builder demo site
  #   content:
  #     title: 👉 Build your own academic website like this
  #     text: |-
  #       This site is generated by Hugo Blox Builder - the FREE, Hugo-based open source website builder trusted by 250,000+ academics like you.

  #       <a class="github-button" href="https://github.com/HugoBlox/hugo-blox-builder" data-color-scheme="no-preference: light; light: light; dark: dark;" data-icon="octicon-star" data-size="large" data-show-count="true" aria-label="Star HugoBlox/hugo-blox-builder on GitHub">Star</a>

  #       Easily build anything with blocks - no-code required!

  #       From landing pages, second brains, and courses to academic resumés, conferences, and tech blogs.
  #     button:
  #       text: Get Started
  #       url: https://hugoblox.com/templates/
  #   design:
  #     card:
  #       # Card background color (CSS class)
  #       css_class: 'bg-primary-700'
  #       css_style: ''
---
