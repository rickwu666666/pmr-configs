Certification team PMR service.
===============================

How to deploy this charm:

1. The first thing is to decide is which Launchpad user to run pmr as. The
   first config option is the username of this user.

2. You also need ssh private and public key parts that are registered on
   Launchpad for that user. Generate these with `ssh-keygen -f pmr-keys`,
   setting no passphrase so pmr can run unattended. Two files, `pmr-keys`
   and `pmr-keys.pub`, will be created, with the private and public keys,
   respectively.

3. To get the Launchpad oauth credentials for that user you can run the
   create_launchpad_credentials.py script included in the charm. This will
   create a `credentials` file.

Once you have all of these create a file called `pmr-config.yaml`
containing::

    cert-pmr:
        launchpad-id: <USERNAME>
        launchpad-public-key: ssh-rsa AAAAA...
        launchpad-private-key: |
            -----BEGIN RSA PRIVATE KEY-----
            MII....
            ...
            -----END RSA PRIVATE KEY-----
        launchpad-credentials: |
            [1]
            consumer_key = pmr
            consumer_secret =
            access_token = 1232...
            access_secret = AAA...

Then you can deploy pmr with (assuming you're in `pmr-configs`):

    juju deploy --constraints "mem=6G arch=amd64" --repository charms local:xenial/cert-pmr --config pmr-config.yaml

passing the filename of the file you just created.

[1]: https://github.com/checkbox/pmr-configs
