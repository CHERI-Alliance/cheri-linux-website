# Website for CHERI Alliance collaboration around Linux

This repository contains the static website for [cheri-linux.org](https://cheri-linux.org)

## Set up

This site is built using [Hugo](https://gohugo.io), a static site generator. On
Debian, you can install Hugo with:

```
 sudo apt install hugo
```

On FreeBSD, you can install Hugo with:

```
 sudo pkg install gohugo
```

For other build environments, see the general [install
guide](https://gohugo.io/getting-started/installing).

## Test build

To preview your changes to the website locally on your laptop, you can spin up a
small local webserver with the command:

```
 hugo server
```

The output from the command includes the URL to preview the test site in your
browser (the port will change randomly):

```
Web Server is available at http://localhost:1313/
```

## Production deployment

If the site is hosted on GitHub Pages or Netlify, the hosting environment will
automatically rebuild and publish the static site every time you push a change
to the `main` branch of the git repository.

For an old-school manual deployment, build the static site locally by running
the command:

```
 hugo
```

This will build the static site in the `public/` directory, which you can then
copy over to the server. (Generating the static site locally is also a useful
debugging technique.)
