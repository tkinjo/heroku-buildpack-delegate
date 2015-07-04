heroku-buildpack-delegate
===



Example
---


Clone the sample application.

```
$ git clone https://github.com/heroku/node-js-getting-started.git
$ cd node-js-getting-started
```




Create an app on Heroku.

```
$ heroku create
```





Using a custom Buildpack.

```
$ heroku buildpacks:set https://github.com/heroku/heroku-buildpack-node
$ heroku buildpacks:add https://github.com/tkinjo/heroku-buildpack-delegate
```



Setup delegated buildpack scripts.



`./node-js-getting-started/bin/compile`

```
#!/usr/bin/env bash
# bin/compile <build-dir> <cache-dir> <env-dir>

### Configure directories

BUILD_DIR=${1:-}
CACHE_DIR=${2:-}
ENV_DIR=${3:-}

mkdir $BUILD_DIR/public/test
cp $BUILD_DIR/public/node.svg $BUILD_DIR/public/test
```





`./node-js-getting-started/bin/detect`


```
#!/usr/bin/env bash
# bin/detect <build-dir>

echo "Node.js"
exit 0
```




`./node-js-getting-started/bin/release`


```
#!/usr/bin/env bash
# bin/release <build-dir>

cat << EOF
addons: []
EOF
```




Deploy your code.

```
$ git push heroku master
```




Access `[app-name].herokuapp.com/test/node.svg`.



Forked from
---

forked from [k-kinzal/heroku-buildpack-delegate](https://github.com/k-kinzal/heroku-buildpack-delegate)
