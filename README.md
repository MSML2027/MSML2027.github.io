# MSML 2027 - Jekyll Site

Mathematical and Scientific Machine Learning (MSML) 2027 conference website, built with Jekyll.

Live site: https://msml2027.github.io/

## Setup

1. Install Ruby and Bundler if you haven't already
2. Install dependencies:
   ```bash
   bundle install
   ```

## Local Development

To run the site locally:

```bash
bundle exec jekyll serve
```

Then visit `http://localhost:4000` in your browser.

## Build for Production

To build the static site:

```bash
bundle exec jekyll build
```

The generated site will be in the `_site` directory.

## GitHub Pages Deployment

This repository deploys to GitHub Pages from the `main` branch (`https://msml2027.github.io/`).

1. Push changes to `main`
2. GitHub Pages builds and deploys automatically
3. Site settings: Settings → Pages → Source = Deploy from a branch (`main`)

## Editing Content

Most content is managed through YAML files in `_data/` and page templates in the repo root.

### Conference Information

Edit `_data/conference.yml`:

```yaml
name: "MSML 2027"
short_name: "MSML 2027"
dates: "To be announced"
venue: "To be announced"
email: "TBD"
about: "Conference description..."
```

### Important Dates

Edit `_data/dates.yml`.

### Committee Members

Edit `_data/committees.yml` (`international_organizing`, `local_organizing`).

### Registration Fees

Edit `_data/registration.yml`.

### Organizer Logos

Edit `_data/organizers.yml`. Logo images go in `assets/images/`.

## Directory Structure

```
.
├── _config.yml
├── _data/
│   ├── conference.yml
│   ├── dates.yml
│   ├── committees.yml
│   ├── registration.yml
│   └── organizers.yml
├── _layouts/
├── _includes/
├── assets/
├── index.html
├── speakers.html
├── dates.html
├── registration.html
├── submission.html
├── venue.html
└── program.html
```

## Conference Information

- **Name:** MSML 2027
- **Dates:** To be announced
- **Venue:** To be announced
- **Site:** https://msml2027.github.io/
