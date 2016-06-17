# Toquen Python Library

This library is a small wrapper around some [boto3](https://github.com/boto/boto3) functions that allows users of the [Toquen](https://github.com/bmuller/toquen) project to fetch server information in Python projects.

## Installation

```
pip install toquen
```

## Usage
*This assumes you have a working familiarity with [Toquen](https://github.com/bmuller/toquen).*

Assuming you want to be able to set up roles in your [Fabric](http://docs.fabfile.org/) with the host locations of your servers in AWS, use this form:

```python
from fabric.api import env, roles, run
from toquen.client import FabricFriendlyClient

aws = FabricFriendlyClient()
env.roledefs = {
    'staging': aws.ips_with_roles(['web'])
}

def dosomething():
    run('ls /home')
```

Then, on the command line, you can run the `dosomething` task over all servers with the `staging` role like this:

```shell
fab -R staging dosomething
```

Easy peasy.