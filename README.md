# omb-infra-lab
Vagrantfile and salt config files to play with a potential omb infra

Requirements (I suppose like any other not-so-small infra):
Some points may be more or less redundant.

1. Near zero down time => multi-providers + HA setup
2. Easy to deploy/scale => Saltstack
3. Easy to test and deploy software on it => Jenkins
4. Easy to monitor => ElasticSearch
