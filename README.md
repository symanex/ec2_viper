# ec2_viper

**ec2_viper** is a small tool to _find and terminate EC2 instances without a
certain tag_ that are running longer than a defined grace time. It can be used
to clean up EC2 instances that are missing mandatory tags on a regular basis.

The default behaviour for `ec2_viper` is to search for all EC2 instances in
the default region (`AWS_DEFAULT_REGION` if set, otherwise `us-east-1`) that are
running for longer than 30 minutes and have no `Name` tag set.

`ec2_viper` will not terminate any instances until the `--armed` option was
explicitly set.

## Examples

Search for EC2 instances that are missing a 'Name' tag and are running for at
least 15 minutes (dry run):

``ec2_viper``

Terminate all EC2 instances that are missing a 'Name' tag and are running for at
least 30 minutes:

``ec2_viper --armed``

Terminate all EC2 instances that are missing an 'Environment' tag an are runnung
for at least 15 minutes:

``ec2_viper --qualifier Environment --gracetime 15 --armed``

Terminate all EC2 instances in the `eu-west-1` region that are running for at
least 5 minutes and have no `Status` tag set:

``ec2_viper --qualifier Status --gracetime 5 --region eu-west-1 --armed``

# ec2_janitor

**ec2_janitor** is a small tool to _find and terminate EC2 instances that are
flagged by a specific tag=value_. This is especially useful to flag instances
for deletion and delete them asynchronously.

The default behaviour of `ec2_janitor` is to search for all EC2 instances in
the default region (`AWS_DEFAULT_REGION` if set, otherwise `us-east-1`) that
have a tag `DeleteMe` set to `now`.

`ec2_janitor` will not terminate any instances until the `--armed` option was
explicitly set.

## Examples

Search for EC2 instances that have a tag 'DeleteMe' set to 'now':

``ec2_janitor``

Terminate all EC2 instances that have a tag 'DeleteMe' set to 'now':

``ec2_janitor --armed``

Terminate all EC2 instances that a tag 'terminate-me' set to 'true':

``ec2_janitor --tag terminate-me --value true --armed``

Terminate all EC2 instances in the `eu-west-1` region that have a tag
'DeleteMe' set to 'now':

``ec2_janitor --region eu-west-1 --armed``
