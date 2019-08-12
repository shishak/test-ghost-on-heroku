# [Ghost 2.X](https://github.com/TryGhost/Ghost) on [Heroku](http://heroku.com)

Ghost is a free, open, simple blogging platform. Visit the project's website at <http://ghost.org>, or read the docs on <http://support.ghost.org>.

## Disclaimer

This is a fork with some improvements from https://github.com/cobyism/ghost-on-heroku. I have forked and improved this repository as the original developer seemed to have abandoned his repo recently. In this repository I have upgraded ghost to ghost 2.X and added cloudinary as a free storage alternative to amazon's s3. If you are still interested with the ghost 1.0 version please visit the original repository.

## Ghost version 2.X

The latest release of Ghost is now supported! Changes include:

  * Requires MySQL database, available through either of two add-ons:
    * [JawsDB](https://elements.heroku.com/addons/jawsdb) (deploy default)
    * [ClearDB](https://elements.heroku.com/addons/cleardb)
  * `PUBLIC_URL` config var renamed to `APP_PUBLIC_URL` to give it alphabetical precedence
  * The app is configured to use `Cloudinary File Storage` by default.

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

### step-by-step tutorial

The following video is a step by step tutorial:

[![thumbnail](https://img.youtube.com/vi/cODvhXMHgYI/0.jpg)](https://www.youtube.com/watch?v=cODvhXMHgYI)

### Things you should know

After deployment,
- First, visit Ghost at `https://YOURAPPNAME.herokuapp.com/ghost` to set up your admin account
- The app may take a few minutes to come to life
- Your blog will be publicly accessible at `https://YOURAPPNAME.herokuapp.com`
- If you subsequently set up a [custom domain](https://devcenter.heroku.com/articles/custom-domains) for your blog, you’ll need to update your Ghost blog’s `APP_PUBLIC_URL` environment variable accordingly
- If you create a lot of content or decide to scale-up the dynos to support more traffic, a more substantial, paid database plan will be required.

#### 🚫🔻 Do not scale-up beyond a single dyno

[Ghost does not support multiple processes.](https://docs.ghost.org/faq/clustering-sharding-multi-server/)

If your Ghost app needs to support substantial traffic, then use a CDN add-on:

  * [Fastly](https://elements.heroku.com/addons/fastly)
  * [Edge](https://elements.heroku.com/addons/edge).


### How this works

This repository is a [Node.js](https://nodejs.org) web application that specifies Ghost as a dependency, and makes a deploy button available.

  * Ghost and Casper theme versions are declared in the Node app's [`package.json`](package.json)
  * Versions are locked and managed using [yarn](https://yarnpkg.com)
  * Scales across processor cores in larger dynos via [Node cluster API](https://nodejs.org/dist/latest-v10.x/docs/api/cluster.html)

## Updating source code

Optionally after deployment, to push Ghost upgrades or work with source code, clone this repo (or a fork) and connect it with the Heroku app:

```bash
git clone https://github.com/snathjr/ghost-on-heroku
cd ghost-on-heroku

heroku git:remote -a YOURAPPNAME
heroku info
```

Then you can push commits to the Heroku app, triggering new deployments:

```bash
git add .
git commit -m "Important changes"
git push heroku master
```

Watch the app's server-side behavior to see errors and request traffic:

```bash
heroku logs -t
```

See more about [deploying to Heroku with git](https://devcenter.heroku.com/articles/git).

### Upgrading Ghost

This repository locks Ghost to the "last tested good version" using the standard `yarn.lock` file. If you want to upgrade Ghost on your own,
you will need to clone or fork this repo as described above. You will then be able to run:

```bash
yarn upgrade ghost
git add package.json yarn.lock
git commit -m 'Update dependencies'
git push heroku master
```

If you're worried about packages beyond the root `ghost` server being outdated, you can check using `yarn outdated`.

## Problems?

If you have problems using your instance of Ghost, you should check the [official documentation](http://support.ghost.org/) or
open an issue on [the official issue tracker](https://github.com/TryGhost/Ghost/issues). If you discover an issue with the
deployment process provided by *this repository*, then [open an issue here](https://github.com/snathjr/ghost-on-heroku).

## License

Released under the [MIT license](./LICENSE), just like the Ghost project itself.
