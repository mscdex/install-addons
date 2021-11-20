Description
===========

`install-addons` downloads and installs prebuilt node addons (when possible)
from Github. It is the companion node module to the [build-addons][] Github
Action.

How to Use
==========

1. Make sure you have [build-addons][] correctly providing binaries for
   downloading.

2. Add the following to your **package.json**:

    ```js
    "install-addons": {
      "binaryRepo": "<user>/<repoName>",
      "binaryOutPath": "build/Release/<bindingName>.node"

      "buildCommand": "<command>",
      "preBuildCommand": "<command>",
      "buildDependencies": {
        "<packageName>": "<packageVersion>"
      },

      "usesNapi": <boolean>,
    }
    ```

    * `binaryRepo` - A **required** string containing the user and repository
      name of where prebuilt versions of this node addon can be found.

    * `binaryOutPath` - A **required** string containing the path where prebuilt
      binaries should be downloaded to. Typically this will be something like
      `'build/Release/mybinding.node'`.

    * `buildCommand` - A **required** string that contains the command to
      build the addon. Typically this will simply be `'node-gyp rebuild'` for
      most addons.

    * `preBuildCommand` - An optional string containing a command to execute
      before executing `buildCommand`. This is useful if you have an additional
      step to configure/prepare things first (e.g. generate .gypi files).

    * `buildDependencies` - An optional object containing dependencies that need
      to be installed before a local build can take place. For example, you
      would put `nan` or similar npm packages here.

    * `usesNapi` - An optional boolean that indicates whether this addon
      utilizes napi/node-api. This is used when checking for compatible prebuilt
      addons.


3. Call `node-install-addons` from an install script:

    ```js
      "scripts": {
        "install": "node-install-addons"
      },
    ```

4. You're done!


CLI Parameters
==============

* `--fallback-to-build` - Attempts to build the addon locally if a binary cannot
  be found.

* `--build-from-source` - 

* `--silent-build` - 

* `--override-arch` - 

* `--override-libc` - name or {name}_{major.minor}

* `--override-platform` - name or {name}_{major.minor}


[build-addons]: https://github.com/mscdex/build-addons
