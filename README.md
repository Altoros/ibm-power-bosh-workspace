# Description

BOSH workspace for BOSH and CF deployment to Power OpenStack.

# How to use

### Deploy MicroBOSH

1. Build required assets using [power-bosh-jumpbox-bootstrap](https://github.com/Altoros/power-bosh-jumpbox-bootstrap) projects. Place stemcell to `stemcells/stemcell.tgz`, BOSH release to `releases/bosh-release.tgz` and OpenStack CPI release to `releases/cpi-release.tgz`.
1. Put your credentials to `config/secret.yml` file (you can use `secret.yml.example` as a sample);
  -  to retrieve `net_id` install the [nova Python client](https://github.com/openstack/python-novaclient) and execute:
```
nova --os-username=xxx --os-password=xxx --os-tenant-name=xxx --os-auth-url="xxx" --os-compute-api-version=2 network-list 
```
1. Put floating IP address that will be assigned to MicroBOSH instance to `config/micro-bosh-stub.yml` file.
1. Run `./generate_manifest micro-bosh` script, this will create `manifests/micro-bosh.yml` file from template in `templates/micro-bosh.yml`.
1. build `bosh-init` from [this branch](https://github.com/Altoros/bosh-init/tree/power-v0.0.51)
1. run `bosh-init deploy manifests/micro-bosh.yml`


### How to build OpenStack CPI for Power architecture
```bash
git clone --branch power https://github.com/Altoros/bosh-openstack-cpi-release.git
cd bosh-openstack-cpi-release
./scripts/vendor_gems   # ideally, you don't need to do it because necessary gems will be in repo
bosh create release --with-tarball --force
# place this release to ~/workspace/releases/cpi-release.tgz
```

### How to build BOSH for Power architecture

```bash
# place bosh release to ~/workspace/releases/bosh-release.tgz
# place cpi release to ~/workspace/releases/cpi-release.tgz
# place stemcell to ~/workspace/stemcells/stemcells.tgz
```

before runniung bosh-init be sure you have `~/.ssh/id_rsa.pub` and `~/.ssh/id_rsa.pem` files on your instance.

```
./generate_manifest micro-bosh config/micro-bosh.yml
BOSH_INIT_LOG_LEVEL=DEBUG bosh-init deploy manifests/micro-bosh.yml
```
