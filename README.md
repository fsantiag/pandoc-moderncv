# Pandoc-ModernCV

Pandoc-ModernCV uses [Pandoc](https://pandoc.org/) facilities to allow you to write curriculums vitae in markdown. Inspired by the well known Latex ModernCV,
it is fairly customizable, allowing you to use predefined themes and to define your own style by changing colors, fonts, etc.

## Features

- Write your CV in markdown
- Choose between themes
- Customize your style
- Export to HTML5
    + responsive layout (mobile, tablet, desktop)
    + print layout
- Export to PDF
    + A4 format ready
    + PDF tags (title, author, etc.)
- Publish public & private CV

## Requirements & Installation

For building your CV in html you need:
- [Compass](http://compass-style.org/) (>= 1.0) `gem install compass`
- [Susy](http://susy.oddbird.net/) (>= 2.2) `gem install susy`
- [Pandoc](http://johnmacfarlane.net/pandoc/) (>= 1.13) `sudo dnf install pandoc`
- [RSync](http://rsync.samba.org/)

For exporting to pdf, you need:
- [exiftool](https://exiftool.org/) (>= 11.70) `sudo dnf install perl-Image-ExifTool`
- [wkhtmltopdf](https://wkhtmltopdf.org/) (>= 0.12.5) `sudo dnf install wkhtmltopdf`

## Getting Started

The simplest way to get started with *pandoc-moderncv* is to use the provided scaffold. In a terminal just do:

    $ make scaffold
    $ make html

It creates a scaffold *cv* located in the /cv directory and builds an html version of it. Use your favorite broser to open the generate cv, for instance:

    $ firefox dist/cv.html

To export the CV to pdf just do:

    $ make pdf

### Metadata

Your CV can be customized with metadata. Metadata are located between two --- separators at the top of the cv.md file and are formated using the YAML format:

    ---
    lang: en
    title: Résumé Title
    firstname: Firstname
    lastname: Lastname
    photo: images/picture.png
    email: contact@yoursite.com
    mobile: '+1 (234) 567 890'
    address:
      city: City
      country: Country
    settings:
      protect-mobile: true
      protect-email: true
    ---

    put here your *CV* data

Currently Pandoc-MordernCV supports the following metadata:

| key                     |  type    | value                          |
| :---------------------- | :------: | :----------------------------- |
| lang                    | string   | en                             |
| title                   | string   | Résumé Title                   |
| firstname               | string   | Firstname                      |
| lastname                | string   | Lastname                       |
| photo                   | url      | path/to/photo.png              |
| qrcode                  | url      | images/qrcode.png              |
| contact                 | url      | http://contact.yoursite.com    |
| homepage                | url      |  http://yoursite.com           |
| email                   | email    | contact@yoursite.com           |
| mobile                  | string   | '+1 (234) 567 890'             |
| phone                   | string   | '+2 (345) 678 901'             |
| fax                     | string   | '+3 (456) 789 012'             |
| footer                  | markdown | **custom** *markdown* text     |
| **address**             | map      |                                |
|   city                  | string   | City                           |
|   country               | string   | Country                        |
| **settings**            | map      |                                |
| protect-email           | boolean  | true/false (default: false)    |
| protect-mobile          | boolean  | true/false (default: false)    |
| protect-phone           | boolean  | true/false (default: false)    |
| protect-fax             | boolean  | true/false (default: false)    |
| protect-address         | boolean  | true/false (default: false)    |
| display-lastupdate      | boolean  | true/false (default: false)    |

### Private & Public CV

It is often handy to hide/show specific informations in your CV depending on where it is published/sent. Pandoc-ModernCV supports **public** and **private** cv:
* when **public**:
    - protected metadata are removed.
    - *cv/public.md* is displayed just after the header and before the CV body.
* when **private**:
    - protected metadata are displayed.
    - *cv/private.md* is displayed just after the header and before the CV body.

#### Protecting Metadata

Currently Pandoc-ModernCV can protect the following metadata:
* email
* mobile
* phone
* fax
* address

Metadata can be (un)protected independently as follow:

    ---
    ...
    settings:
      protect-mobile: true # this protect *mobile*
      protect-email: false # this unprotect *email*
    ---


#### Building Private/Public CV

To build a public CV just do:

    $ make html public-cv=true
    or
    $ make pdf public-cv=true

To build a private CV just do:

    $ make html private-cv=true
    or
    $ make pdf private-cv=true

### Themes

Currently pandoc-moderncv supports a two themes: classic and alternative.

You can chose a theme by setting the `THEME` varible. For instance:
```
$ make html THEME=alternative
```

### Colors, Fonts, Icons

All themes can be customized through variables defined in *stylesheets/_settings.scss*.
