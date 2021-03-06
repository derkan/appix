# Maintainers

## Pull Requests

When merging Pull Requests on GitHub, use the [squash and merge](https://github.com/blog/2141-squash-your-commits) button, so that our timeline of master branch is linear.

## Travis-CI

We use Travis for generating our executables automatically. To successfully build it, we need to make sure these environment variables are set there:

```
export TRAVIX_FIREBASE_API_KEY=""
export TRAVIX_FIREBASE_AUTH_DOMAIN=""
export TRAVIX_FIREBASE_DATABASE_URL=""
export TRAVIX_FIREBASE_STORAGE_BUCKET=""
export TRAVIX_FIREBASE_MESSAGING_SENDER_ID=""
export TRAVIX_LOGGER_URL=""

export TRAVIX_DEVELOPER_PROFILE_URL=""
```

You can set them here: [https://travis-ci.org/Travix-International/appix/settings](https://travis-ci.org/Travix-International/appix/settings)

## Releases

Our Travis pipeline automatically releases a new version if we tag a commit. The version number is going to be the value of the tag.

We are using semantic versioning, so the version number is set manually. When we want to release, have to decide on the [next version number](https://github.com/Travix-International/appix/releases).  
To publish a new release, push a new tag to the commit you want to release (typically after merging a PR to master).

```
$ git checkout master
$ git pull origin master

$ git tag 1.4.2
$ git push origin master --tags
```

After pushing the tag, Travis will pick it up automatically, and deploy it to [GitHub Releases](https://github.com/Travix-International/appix/releases), from which our install scripts always pick up the latest version.

## Changelogs

Changelogs are generated using the `github_changelog_generator` gem.

Make sure you have Ruby v2.2+:

```
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
$ curl -sSL https://get.rvm.io | bash -s stable

$ rvm install 2.2.2
```

Then install the gem:

```
$ gem install github_changelog_generator
```

Now you can generate `CHANGELOG.md` file automatically by running:

```
$ make changelog GITHUB_API_TOKEN="YOUR_GITHUB_TOKEN"
```

You can generate a token [here](https://github.com/settings/tokens/new?description=GitHub%20Changelog%20Generator%20token)

Since this is a public repository, you only need `public_repo` access for the token.
