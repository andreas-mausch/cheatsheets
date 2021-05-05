# Cheatsheets

## Run locally

```bash
bundle install
bundle exec jekyll serve --host=0.0.0.0
```

## Add logo

Add this section to the markdown:

```
logo: data:image/svg+xml;base64,XXXX
```

Replace *XXXX* by the output of this command:

```bash
base64 --wrap=0 logo.svg
```
