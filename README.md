Mercurane
======

![Mercurane molecule](http://www.3quarksdaily.com/.a/6a00d8341c562c53ef01910423854b970c-250wi)

[![Build Status](https://travis-ci.org/PetroCloud/Mercurane.svg?branch=master)](https://travis-ci.org/PetroCloud/Mercurane)

Easy Node.JS Hg wrapper with support for SSH keys. By default, the Hg CLI
tool will only use the SSH key of the current user (e.g. `$HOME/.ssh/id_dsa`).

In order to be able to use Hg with an arbitrary SSH key, a wrapper shell script to invoke `ssh -i <key>` must be written and the ui.ssh option
must point to that script (--config ui.ssh=<wrapper script>).

Mercurane wraps all this plumbing for you. Simply pass the SSH private key you wish to run Hg with as a string argument and let Mercurane do the rest. Mercurane will clean up the temporary wrapper script after it is done.


Installation
============

Mercurane is available in NPM. `npm install mercurane`


Example
=======
```javascript
  var fs = require('fs')
  var mercurane = require('mercurane')
  var path = require('path')

  // Use current working dir
  var baseDir = process.cwd()
  // Read private key from ~/.ssh/id_dsa
  var privKey = fs.readFileSync(path.join(process.env.HOME, '.ssh/id_dsa'), 'utf8')

  mercurane.run(baseDir, privKey, "hg clone ssh://hg@bitbucket.org/petrocloud/test",
    function(err, stdout, stderr, exitCode) {
    if (err) {
      console.log("An error occurred: " + stderr)
      process.exit(1)
    }

    console.log("Hg clone complete!")
  })
```

Tests
=====

Mercurane comes with tests. To run, simply execute `npm test`.

License
=======

Mercurane is released under a BSD license.  It is a fork of Gitane originally written by Niall O'Higgins <niallo@beyondfog.com> (http://niallohiggins.com)

Credits
=======

Niall O'Higgins <niallo@beyondfog.com> (http://niallohiggins.com) for doing the hard work of writing Gitane.

Molecule image courtesy of http://www.3quarksdaily.com
