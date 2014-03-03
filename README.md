# Bosh release for Apache Mesos

One of the fastest ways to get [Apache Mesos](http://mesos.apache.org/) running on any infrastructure is to deploy this BOSH release.

This BOSH release includes the following [Apache Mesos](http://mesos.apache.org/) frameworks:

* [Airbnb Chronos](http://airbnb.github.io/chronos/): A distributed and fault-tolerant scheduler
* [Mesosphere Marathon](https://github.com/mesosphere/marathon): An Apache Mesos framework for long-running services
* [Apache Cassandra](http://cassandra.apache.org/): An open source distributed database management system designed to handle large amounts of data across many commodity servers, providing high availability with no single point of failure
* [Jenkins](http://jenkins-ci.org/): An extendable open source continuous integration server

## Disclaimer

This is not presently a production ready [Apache Mesos](http://mesos.apache.org/) BOSH release. This is a work in progress.

## Usage

To use this BOSH release, first upload it to your BOSH:

```
bosh target BOSH_HOST
git clone git@github.com:cloudfoundry-community/mesos-boshrelease.git
cd mesos-boshrelease
bosh upload release releases/mesos-1.yml
```

Now create a deployment file (using the files at the [examples](https://github.com/cloudfoundry-community/mesos-boshrelease/tree/master/examples) directory as a starting point) and deploy:

```
bosh deployment path/to/deployment.yml
bosh -n deploy
```

## Create new final release

To create a new final release you need to get read/write API credentials to the [@cloudfoundry-community](https://github.com/cloudfoundry-community) s3 account.

Please email [Dr Nic Williams](mailto:&#x64;&#x72;&#x6E;&#x69;&#x63;&#x77;&#x69;&#x6C;&#x6C;&#x69;&#x61;&#x6D;&#x73;&#x40;&#x67;&#x6D;&#x61;&#x69;&#x6C;&#x2E;&#x63;&#x6F;&#x6D;) and he will create unique API credentials for you.

Create a `config/private.yml` file with the following contents:

``` yaml
---
blobstore:
  s3:
    access_key_id:     ACCESS
    secret_access_key: PRIVATE
```

You can now create final releases for everyone to enjoy!

```
bosh create release
# test this dev release
git commit -m "updated mesos"
bosh create release --final
git commit -m "creating vXYZ release"
git tag vXYZ
git push origin master --tags
```
