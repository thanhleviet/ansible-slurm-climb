This repo contains ansible playbooks extracted from [elasticluster](http://elasticluster.readthedocs.io/en/latest/playbooks.html)'s playbooks for installing a slurm based cluster on CLIMB, with few modification.

As CLIMB is built on top of OpenStack, ideally, we can use elasticluster to install slurm conveniently. However, the OpenStack API on CLIMB is likely not available, I eventually ended up with this workaround.

## Prerequisites
- Install ansible: `pip install ansible`
- Login to Horizon [url not shown here] and create a your own private key pair. Download the key to you local computer
- Initiate manually instances using **Launch a custom server** from https://bryn.climb.ac.uk/. The cluster should have 1 head and at least 1 node.

## Installn slurm using Ansible playbook
- Clone this repo:
`git clone https://github.com/thanhleviet/ansible-slurm-climb`
- Copy the key pair into the folder `ansible-slurm-climb`
- Create an inventory file, define server name and ip for the head and the nodes. See the `hosts.cardiff` for example.
- Replace location to the key pair and inventory in `ansible.cfg`
- To install the cluster, run this command from a terminal: `ansible-playbook climb.yml`

The playbook `climb.yml` will install slurm for a e cluster of 1 head and a numbers of nodes defined in `hosts.cardiff` . As I used the cluster temporarily for analyses, I removed some setup which may take the installation longer (i.e. `nis`) and destroy all the instances after I finished. This playbook also install [conda](https://conda.io/miniconda.html), [nextflow](nextflow.io), [singularity](singularity.lbl.gov), [docker](docker.io) for running my own bioinformatics pipelines.

Tested with Ubuntu 16.04 distro but the playbook should work with Debian/Centos/REHL and even on physical computers

Thanks MRC for this valuable computing resource.
