Deploying the Swift Poems Project collation engine
====================

(work in progress)


linux requirements
------------------

- nginx
- git
- mongodb
- redis
- rbenv (ruby ~2.4? should be fine)
- pyenv (python 2.7.11)
- nvm (node lts (~6.4?) should be fine)


swift-encode (ruby)
-------------------

### setup

```
$ git clone https://github.com/swift-poems-project/swift-encode
$ cd swift-encode
$ bundle install
```

### usage

```
# syncs NB files w/ those in Google Drive
$ bundle exec thor swift:sync_poems

# encodes NB files in TEI
$ bundle exec thor swift:encode_poems
```

### notes

- be sure to fill in `config/client_secret.json` w/ GoogleDrive API keys after
  cloning / installing
- set up these tasks as a cron (`0 0 * * *` and `0 4 * * *`, respectively)



swift-transcribe (ruby)
-----------------------

### setup

```
$ git clone https://github.com/swift-poems-project/swift-transcribe
$ cd swift-transcribe
$ bundle install
$ cp config/server.conf.default config/server.conf
```


### usage

```
$ bundle exec rackup
```

### notes

- edit `config/client_secret.json` with GoogleDrive API keys


swift-collate (python)
----------------------

### setup

```
$ git clone https://github.com/swift-poems-project/swift-collate
$ cd swift-collate
$ pip install -r requirements.txt
$ python setup.py install
```


swift-edition (python)
----------------------

### setup

```
$ git clone https://github.com/swift-poems-project/swift-edition
$ cd swift-edition
$ pip install -r requirements.txt
$ python server.py
```

### notes

- run using nohup


swift-ui (nodejs)
-----------------

### setup

```
$ git clone https://github.com/swift-poems-project/swift-ui
$ cd swift-ui
$ npm install
$ npm run build
```

### notes

- uses [foreverjs](https://github.com/foreverjs/forever)

TO-DO
-----

- [ ] write boot service for swift-transcribe
- [ ] write boot service for swift-edition
- [ ] write boot service for swift-ui
- [ ] draft up nginx config