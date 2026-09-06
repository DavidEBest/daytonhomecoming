# Dayton Homecoming

Static site for [daytonhomecoming.com](https://www.daytonhomecoming.com), rebuilt from the
former Wix site. Plain HTML/CSS, no build step, hosted on GitHub Pages. Follows the same
model as the Cars4Work site.

## Pages

| File | Purpose |
| --- | --- |
| `index.html` | Home: mission, evangelist definition, story video and quotes, partners, Collaboratory |
| `about.html` | About Dayton Homecoming, Why/How/What |
| `evangelists.html` | Dayton Evangelists and Connectors |
| `connection.html` | Opportunity Connections: talent connection, job and community resources |
| `testimonials.html` | Testimonial video (Joe Pieroni) and how to submit one |
| `registration.html` | Evangelist / Connector registration form |
| `contact.html` | Contact form |
| `insights.html` | Evangelist follow-up survey form (not in the nav; link it from a thank-you email) |

Dropped from the Wix site: the Privacy and Accessibility pages (both were unedited Wix
template text) and the old Resources page (superseded by Opportunity Connections).

## Forms

All three forms (registration, contact, insights) post to [FormSubmit](https://formsubmit.co),
which is free, needs no account, and delivers straight to `hello@daytonhomecoming.com`.
Each form carries a hidden `_subject` so you can tell submissions apart, uses the `table`
email template, and redirects to `thanks.html` after submitting.

**One-time activation:** the first time a form is submitted, FormSubmit emails
`hello@daytonhomecoming.com` asking you to confirm the address. Click the link once and
every form on the site is live. Until then, submissions are held.

After activation FormSubmit also gives you a random string you can use in place of the
email address in the `action` URL, which keeps bots from scraping the address from the
page source. To switch, replace `hello@daytonhomecoming.com` in the three form actions:

```sh
sed -i '' 's#formsubmit.co/hello@daytonhomecoming.com#formsubmit.co/<random-string>#' registration.html contact.html insights.html
```

Spam protection: FormSubmit shows a reCAPTCHA page by default, and each form has a
`_honey` honeypot field.

## Deploying

1. Create a GitHub repo and push this directory.
2. In the repo settings, enable GitHub Pages from the `main` branch root.
3. `CNAME` already contains `daytonhomecoming.com`. Point the domain's DNS at GitHub Pages
   (A records to GitHub's Pages IPs, plus a `www` CNAME to `<user>.github.io`) and turn on
   "Enforce HTTPS" once the certificate is issued.
4. Cancel the Wix plan after DNS has propagated and the forms have been tested.

## Media

`images/` holds every logo and photo pulled from the Wix site. `videos/` holds the two
Wix-hosted videos: the home page story video (re-encoded from 1080p to 720p, 17 MB) and
Joe Pieroni's testimonial (7 MB). Poster frames for both are in `images/`.

## Local preview

```sh
python3 -m http.server 8000
```

Then open http://localhost:8000.
