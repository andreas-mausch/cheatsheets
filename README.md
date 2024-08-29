# Cheatsheets

## Run locally

```bash
bundle install
bundle exec jekyll serve --host=0.0.0.0
```

via docker:

```bash
docker run -it --rm --volume=.:/srv/jekyll -p 4000:4000 jekyll/jekyll:3.8 jekyll serve
```

## Templates

Jekyll uses the [Liquid](https://shopify.github.io/liquid/) templating language to process templates.

## Commands

Commands can either be a key-value pair like this:

```yaml
section:
  - name: my-program
    commands:
      Show help: my-program --help
```

or an object with additional fields:

```yaml
section:
  - name: my-program
    commands:
      - title: Show help
        command: my-program -h
        description: This shows the usage of the program
        options:
          -h: --help
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
