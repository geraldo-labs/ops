# Site Ops

The following ansible scripts setup up any server for static website.


# How to run?

Before running it is mandatory to provide the `./config/vars.yaml` configuration and the `hosts.ini` file.

A valid configuration for `./config/vars.yaml` would be:

    domain:
        username: geraldo
        comments: geraldo's website
        name: yourdomain.com
        email: email@email.com

    static:
        enabled: true
        repository: 
            name: https://github.com/geraldo-labs/site.git
            version: 0.0.5

    proxy_pass:
        enabled: false
        repository: 
            name: https://github.com/geraldo-labs/site.git
            version: 0.0.5
        port: 9999
        path: /v1/test
        rewrite: /


A valid configuration for `hosts.ini` would be:

    [all]
    yourwebsite.com ansible_connection=ssh ansible_user=root


This script count on you using the ssh key instead of username and password. You can generate the ssh key running the command:

    ssh-keygen -t rsa -b 4096  # follow the screen instructions


You can export your ssh key by running:

    ssh-copy-id -i $HOME/.ssh/id_rsa.pub yourdomain.com


Then run the command:

    ansible-playbook setup.yaml

# Standards

In order to simplify the deployment some standards must be obeyed.

1. The static content must be at `/static` folder in the root of the repository