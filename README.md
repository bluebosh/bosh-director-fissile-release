# KUBE CPI BOSH Director fissile release

This repository contains the files necessary to run a KUBE CPI BOSH Director using fissile.
It is roughly equivalent to doing the same with BOSH.

### fissile

[fissile] is required to build the docker images and configuration.

[fissile]: https://github.com/suse/fissile

### direnv
[direnv] is recommended, but manually sourcing the `.envrc` should work just as
well.

[direnv]: https://github.com/direnv/direnv/

### Ruby
Ruby 2.3 is needed to install some of the releases.  Using [rbenv] with
[ruby-build] should work, but if you have issues [ruby-install] is also an
option.

[rbenv]: https://github.com/sstephenson/rbenv
[ruby-build]: https://github.com/rbenv/ruby-build
[ruby-install]: https://github.com/postmodern/ruby-install/

### BOSH cli
The Ruby version of the [BOSH cli] is required as of writing, as fissile is not
yet compatible with the golang BOSH v2.

[BOSH cli]: https://rubygems.org/gems/bosh_cli

### certstrap
Required to create certificates. Requires golang.
```sh
go get github.com/square/certstrap
```
## Building

1. Get all submodules:
  ```sh
    git submodule update --init --recursive
  ```
  If you cannot create Kubernetes CPI release successfully becase of golang blobstore issue, you can download it first by using:
  ```sh
    ./git-init.sh
  ```  

1. Load needed environment variables (optional, only if you don't use direnv):

   ```sh
     . .envrc
   ```

1. Deploy bu using helm:

   ```sh
     make deploy cluster_name=<cluster name> init=<if re-create image>
   ```

1. Deploy by using kube config:

   ```sh
     make deploy_kube cluster_name=<cluster_name>
   ```
   There is an issue that cannot generate secret correctly, need it COPY by yourself

Note, the specified stemcell is an example. Change it to suit.  The
alternative command uses the definition of `FISSILE_STEMCELL` in
`.envrc` for this.
