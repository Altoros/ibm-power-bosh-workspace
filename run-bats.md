# Run BATs

### Commands to run:

```
cd ~/workspace
./generate_manifest bat.yml

cd ~
git clone https://github.com/Altoros/bosh.git
cd ~/bosh
git checkout power-2915
bundle install
vi .envrc  # see following description
direnv allow
bundle exec rake spec:system:micro[openstack,ubuntu,trusty,dynamic,go,false,qcow]
```

### .direnv

```
# DNS name or IP address of the bosh director used for testing (without the scheme)
export BAT_DIRECTOR=140.211.168.50

# path to the stemcell you want to use for testing
export BAT_STEMCELL=/home/ubuntu/workspace/stemcells/stemcell.tgz

# path to the bat yaml file which is used to generate the deployment manifest (see below `bat.yml`)
export BAT_DEPLOYMENT_SPEC=/home/ubuntu/workspace/manifests/bat.yml

# password used to ssh to the stemcells
export BAT_VCAP_PASSWORD=c1oudc0w

# DNS host or IP where BOSH-controlled PowerDNS server is running, which is required for the DNS tests. For example, if BAT is being run against a MicroBOSH then this value will be the same as BAT_DIRECTOR
# export BAT_DNS_HOST=

# the full path to the private key for ssh into the bosh instances
export BOSH_KEY_PATH=/home/ubuntu/.ssh/id_rsa.pem

# the name of infrastructure that is used by bosh deployment. Examples: aws, vsphere, openstack, warden.
export BAT_INFRASTRUCTURE=openstack

# the type of networking being used: `dynamic` or `manual`.
export BAT_NETWORKING=dynamic

# the path to ssh key, if set bosh ssh will use gateway host and user (optional; required when deployed to vpc)
#export BAT_VCAP_PRIVATE_KEY=
```
