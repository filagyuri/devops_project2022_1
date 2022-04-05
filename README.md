# devops_project2022_1
devops exercise

cél:
- lesz 4 VM, egy control (C), a többi csak node (N) 3 db
- a C-re telepítjük, és onnan futtatjuk az ansible-t, és arról vezéreljük a többi node-ot
- beállítjuk az ansible node group-ot s myhost - file alapján, hogy tudjanak kommunikálni a node-ok.
- minden VM-en legyen Python-simplejson - ezt Ansible nodes paranccsal tesszük fel mindegyikre, hogy több funkcionalitása legyen az ansiblenak.
- minden VM-en legyen docker és docker-compose és minden VM-en a vagrant user legyen hozzáadva a docker csoporthoz - ezt az Ansible playbook1.yml-el kell feltenni az összes VM-re.
- Dockerfile-al telepítünk egy VM-re egy flask-ben futó python app-ot, amit ha az 5000-es porton lekérdezünk, akkor visszaadja, hogy Hello World! I am .... (hostname, ami majd a futattó dockerkonténer ID-je lesz).
- docker-swarm-mal orchestráljuk a többi VM-re, akár több példányban.

the goal: 
- there will be 4 VMs, one control (C), the others will be nodes only (N) 3 pcs
- we will install the ansible on C and from there we will control the other nodes
- we will configure the ansible node group based on myhost - file so that the nodes can communicate.
- all VMs will have Python-simplejson - we put this on each with the Ansible nodes command to give the ansiple more functionality.
- have a docker and docker-compose on each VM and add vagrant user to the docker group on each VM - this must be applied to all VMs with Ansible playbook1.yml.
- Using Dockerfile, we install a python app running on flask on a VM, which, if queried on port 5000, returns Hello World! I am .... (hostname, which will be the ID of the runner dock container).
- orchestrate with docker-swarm to other VMs, even in multiple instances.
-
