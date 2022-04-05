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
- there will be 4 VMs, one control (C), the other only node (N): 3 pcs
- install on C and run ansible from there and control the other nodes from there
- configure the ansible node group based on the myhost file so that the nodes can communicate
- all VMs must have Python-simplejson - we put this on each of them with the Ansible nodes command to have more functionality for ansible
- have docker and docker-compose on all VMs and add vagrant user to docker group on all VMs - this must be added to all VMs with Ansible playbook.yml
- Using Dockerfile, we install a python app running on a VM, which if queried on port 5000, returns Hello World! I am .... (hostname, which will be the ID of the runner dock container)
- orchestrate with docker-swarm to all three nodes / VMs, even in multiple instances - so multiple containers per VM / node for load-balancing to work.
---------------
vagrant up

vagrant ssh control

cd /vagrant
sudo cp /vagrant/hosts /etc/hosts
ssh-keygen
ssh-copy-id node1 && ssh-copy-id node2 && ssh-copy-id node3
sudo apt-get update -y && sudo apt-get install ansible -y
ansible nodes -i myhosts1 -m command -a hostname
ansible nodes -i myhosts1 -m command -a 'sudo apt-get -y install python-simplejson'
ansible-playbook -i myhosts1 -K playbook.yml
ansible-playbook -i myhosts2 -K swarm.yml
ssh node1
cd /vagrant
docker stack deploy --compose-file docker-compose.yml myapp
docker service scale myapp_web=6
ssh control
curl node1:5000
