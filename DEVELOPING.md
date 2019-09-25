# Project Development

For general information about contributing changes, see the
[Contributor Guidelines](https://github.com/titan-data/.github/blob/master/CONTRIBUTING.md).

## Running the site

## Running the site locally

To run the website locally, first make sure you have Ruby 2.1.0 or higher installed.

1. Install the [`bundler`](https://bundler.io/) gem if it's not already installed:

```shell
gem install bundler
```

2. Install Jekyll and other dependencies defined in the Gemfile:

```shell
bundle install --path vendor/bundle
```

3. Run your Jekyll site locally:

```shell
bundle exec jekyll serve --livereload
```

4. Preview the site in your web browser at http://localhost:4000.

### Running the site locally using Docker

To run the website locally using Docker, run the command:

```shell
docker run -it -v $(pwd):/srv/jekyll -p 4000:4000 jekyll/jekyll jekyll serve --watch --incremental
```

Alternatively, use Docker Compose with:

```shell
docker-compose up
```

Preview the site in your web browser at http://localhost:4000.

Describe the internal mechanisms necessary for developers to understand how
to get started making changes.

## Releasing

To deploy your changes all you have to do is push to `master` and Github pages
will automatically run `jekyll build` and deploy the generated files.
