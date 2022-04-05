# devops_project2022_1
devops exercise

cél:
- lesz 4 VM, egy control (C), a többi csak node (N) 3 db
- a C-re telepítjük, és onnan futtatjuk az ansible-t, és arról vezéreljük a többi node-ot
- beállítjuk az ansible node group-ot a myhost file alapján, hogy tudjanak kommunikálni a node-ok
- minden VM-en legyen Python-simplejson - ezt Ansible nodes paranccsal tesszük fel mindegyikre, hogy több funkcionalitása legyen az ansible-nak
- minden VM-en legyen docker és docker-compose és minden VM-en a vagrant user legyen hozzáadva a docker csoporthoz - ezt az Ansible playbook.yml-el kell feltenni az összes VM-re
- Dockerfile-al telepítünk egy VM-re egy flask-ben futó python app-ot, amit ha az 5000-es porton lekérdezünk, akkor visszaadja, hogy Hello World! I am .... (hostname, ami majd a futattó dockerkonténer ID-je lesz)
- docker-swarm-mal orchestráljuk mind a három node-ra/VM-re, akár több példányban - tehát több konténer VM-enként/node-onként, hogy a load-balancing működjön.
---------------
Target:
- there will be 4 VMs, one control (C), the other only node (N) 3 pcs
- install on C and run ansible from there and control the other nodes from there
- set the ansible node group based on myhost file so that the nodes can communicate
- Python-simplejson on all VMs - do this with the Ansible nodes command to make it more functional
- docker and docker-compose must be added to each VM and the vagrant user must be added to the docker group on each VM - this must be applied to all VMs with Ansible playbook1.yml
- Using Dockerfile, we install a python app running on a VM, which if queried on port 5000, returns Hello World! I am .... (hostname, which will be the ID of the runner dock container). - this is only needed to test the app. Can be deleted after verification.
- orchestrate with docker-swarm to all three nodes / VMs, even in multiple instances - so multiple containers per VM / node

Target:
- there will be 4 VMs, one control (C), the other only node (N): 3 pcs
- install on C and run ansible from there and control the other nodes from there
- configure the ansible node group based on the myhost file so that the nodes can communicate
- all VMs must have Python-simplejson - we put this on each of them with the Ansible nodes command to have more functionality for ansible
- have docker and docker-compose on all VMs and add vagrant user to docker group on all VMs - this must be added to all VMs with Ansible playbook.yml
- Using Dockerfile, we install a python app running on a VM, which if queried on port 5000, returns Hello World! I am .... (hostname, which will be the ID of the runner dock container)
- orchestrate with docker-swarm to all three nodes / VMs, even in multiple instances - so multiple containers per VM / node for load-balancing to work.
