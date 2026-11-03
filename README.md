# Tr3umPHant Designs Website

Trey Hope's 2014 graphic design portfolio site. Visitors browse flyers, logos and illustrations Trey designed, read about him, and order a custom design through a request form that emails the order (with an optional reference image attached) straight to him.

The layout is built on the [Business Casual](https://startbootstrap.com/theme/business-casual) Bootstrap theme from Start Bootstrap, with custom pages, a lightbox gallery and PHP forms added on top.

## Features

- **Portfolio gallery** (`index.html`, duplicated as `graphicwork.html`): three sections of thumbnails, Flyers (`img/flyers/`), Logos (`img/logos/`) and Illustrations (`img/illustrations/`). Clicking a thumbnail opens it full size in a Bootstrap modal.
- **About page** (`about.html`): Trey's bio, photo, social links and skill bars (Photoshop, Illustrator, HTML, CSS, MySQL, JavaScript, PHP, jQuery).
- **Design request form** (`requests.php`):
  - Name, email and phone, plus the design type with prices: Illustration $30, Flyer $25, Logo $20.
  - A "date needed" picker (bootstrap-datetimepicker). Picking a date within two days shows a notice that rush orders cost $15 extra and flags `extraCharge` in the email.
  - An optional image upload that's saved to `uploads/` and sent as a MIME attachment.
  - A free-text description of the design.
- **Contact form** (`contact.php`): name, email, phone and message, sent with PHP `mail()`.

## How it works

The gallery and about pages are static HTML. The two forms post back to their own PHP page, which validates the fields, builds the email body (and for requests, a multipart message with the uploaded file base64-encoded), sends it with `mail()` and prints a green success or red error message above the form.

## Tech stack

- HTML, CSS and Bootstrap 3 (Start Bootstrap "Business Casual" theme, `css/business-casual.css`)
- jQuery and bootstrap-datetimepicker
- PHP for the contact and request forms

## Getting started

### Prerequisites

- PHP with a working `mail()` setup (sendmail or SMTP) for the forms to send email.
- A writable `uploads/` folder next to `requests.php` for image attachments (it isn't in the repo, so create it).

### Running locally

```bash
git clone https://github.com/trey-a-hope/website-tr3umphant-designs.git
cd website-tr3umphant-designs
mkdir uploads
php -S localhost:8000
```

Then open <http://localhost:8000/index.html>.

### Configuration

Recipient addresses are hard-coded: the request form emails the address in `$to` in `requests.php`, and the contact form emails the address in the `mail()` call in `contact.php`. Update both before deploying.

## Project structure

```
website-tr3umphant-designs/
├── index.html         # Home / portfolio gallery with modal viewer
├── graphicwork.html   # Same gallery (identical to index.html)
├── about.html         # Bio and skills
├── requests.php       # Design order form with pricing, rush fee and file upload
├── contact.php        # Contact form
├── css/               # Bootstrap, Business Casual theme and plugin styles
├── jquery/            # jQuery 1.8.3
├── img/               # Portfolio images, backgrounds, social icons
├── audio/             # onandon.mp3 (not referenced by any page)
└── fonts/             # Glyphicons
```

## Known limitations

- The pages load `js/jquery.js`, `js/bootstrap.min.js` and `js/jquery-1.11.1.min.js`, but there's no `js/` folder in the repo, so the modal gallery, navbar toggle and date picker won't work until those files are added (or swapped for CDN links).
- `contact.php` sends the form with GET, so messages end up in the URL and server logs.
- Uploaded files keep their original names in `uploads/` with no type or size checks.
- Dreamweaver sync folders (`_notes/`) are committed and can be removed.

## License

The Business Casual theme is © Iron Summit Media Strategies and released under the Apache 2.0 license (see [`LICENSE`](LICENSE)). The portfolio artwork belongs to Trey Hope.
