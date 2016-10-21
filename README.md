Steps to deploy static site to heroku

# Prerequisites


- A Heroku account. Signup is free and instant.
- The Heroku CLI installed
- Ruby and the Bundler gem installed

## Create directory structure

```
$ mkdir -p site/public/{images,js,css}
$ touch site/{config.ru,public/index.html}
$ cd site && bundle init
```

## This will create the following directory structure:

```
- site
  |- config.ru
  |- Gemfile
  |- public
    |- index.html
    |- images
    |- js
    |- css
```


## In the Gemfile file add the following:

source 'https://rubygems.org'   
gem 'rack'


## run the bundle command to download and resolve the rack dependency.

```
$ bundle install
```

## editing the config.ru file so it contains the following:

```
use Rack::Static,
  :urls => ["/images", "/js", "/css"],
  :root => "public"

run lambda { |env|
  [
    200,
    {
      'Content-Type'  => 'text/html',
      'Cache-Control' => 'public, max-age=86400'
    },
    File.open('public/index.html', File::RDONLY)
  ]
}
```

## start app locally 

```
$ rackup
```
## heroku 

```
$ git init 
$ heroku create 
$ git add . 
$ git commit -m "Initial static site template app" 
```
## Use git to deploy to Heroku as well.

```
$ git push heroku master
$ heroku app:{given name} {old name}
$ heroku open
```
