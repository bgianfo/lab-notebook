# Git Commit Signing with Keybase

I already have a [keybase](https://keybase.io/bjg) account.
I've been interested in getting git commit signing setup with my keybase pgp key.
I quickly found a nice guide that worked well.
See: [https://meedamian.com/post/keybase-signed-github](https://meedamian.com/post/keybase-signed-github/)

After following the guide, git now shows my commits as signed.
Example:

```diff
bgianf@LMAO:~/src/lab-notebook/src$ git log --show-signature -1
commit be372efa95c64ef4a71e2b06e69baf47d275923f (HEAD -> main, origin/main, origin/HEAD)
gpg: Signature made Tue Dec 29 21:14:34 2020 PST
gpg:                using RSA key 899C11E2EEAA2EEE43775D148802D4B232E81AFA
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
gpg: Good signature from "Brian Gianforcaro (http://bjg.io) <b.gianfo@gmail.com>" [ultimate]
gpg:                 aka "keybase.io/bjg <bjg@keybase.io>" [ultimate]
Author: Brian Gianforcaro <b.gianfo@gmail.com>
Date:   Tue Dec 29 21:12:47 2020 -0800

    Notes: Add note about signing commits with keybase pgp keys
```

GitHub displays these with the **VERIFIED** qualifier.

See: [https://github.com/bgianfo/lab-notebook/commit/be372efa95c64ef4a71e2b06e69baf47d275923f](https://github.com/bgianfo/lab-notebook/commit/be372efa95c64ef4a71e2b06e69baf47d275923f)


Nice!
