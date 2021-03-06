# Quick runner/wrapper for scholars-discovery project

Instructions:

## Import two git repositories into the base folder of this repository

1) git clone https://github.com/vivo-community/scholars-discovery.git 
2) git clone https://github.com/vivo-project/sample-data.git

NOTE: everything assumes the scholars-discovery code is checked out into the 
`scholars-discovery` directory, and `sample-data` into a `sample-data` directory
(which is the default anyway).  They are in the `.gitignore` file.

This will run off the `scholars-discovery` master branch.  Right now that might
not have a grapqhl endpoint - for the time being it may be best to switch to
the `vstf-staging` branch (e.g. `git checkout ...`).  The idea for this
project is you should be able to use it to run *any* branch in development mode.

## import some data

3) `cd data-importer`
4) `./gradlew build` (or `gradlew.bat` on Windows)
5) `./gradlew run --args='openvivo --import'`

That should (after 5-10 minutes) put data in the data-imported/openvivo
directory.  Then `cd ..` (back up to scholars-discovery-setup directory)

6) `cd ..`
7) `docker-compose up`

### or (if already imported data into TDB)

3) `docker-compose up`

This is making us of a file `application-dev.yml` to configure `scholars-discovery`
for local development mode.  It also defaults to importing data into the index 
at startup.

However, you can change `middleware.index.onStartup=false` **after the first start up** 
has finished and imported into the index succesfully - so that it doesn't rebuild the
index every time.

```yaml
# file: application-dev.yml

...
middleware:
  index:
    onStartup: true # change to false after first run
...

```

## Sample Query

Once you have running, can go this http://localhost:9000/gui and run GraphQL queries.
Sample queries can be found here:

[Wiki (see sample Graphql queries)](https://github.com/vivo-community/scholars-react/wiki)

