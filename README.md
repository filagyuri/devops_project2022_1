# devops_project2022_1
docker-swarm exercise based on https://www.youtube.com/watch?v=YuZ002YrvUA&t=1296s, and https://github.com/devopsjourney1/devops-project2021
Many thanks for Brad! 

cél:
- lesz 4 Virtualbox VM, egy control (C), a többi csak node (N) 3 db
- a C-re telepítjük, és onnan futtatjuk az ansible-t, és arról vezéreljük a node 1-3-at
- beállítjuk az ansible node group-ot a myhost file alapján, hogy tudjanak kommunikálni a node-ok
- legyen Python-simplejson a node 1-3-on - ezt Ansible nodes paranccsal tesszük fel mindegyikre, hogy több funkcionalitása legyen az ansible-nak
- legyen docker és docker-compose a node 1-3-on és a vagrant user legyen hozzáadva a docker csoporthoz - ezt az Ansible playbook.yml-el kell feltenni
- Dockerfile-al telepítünk egy flask-ben futó python app-ot, amit ha az 5000-es porton lekérdezünk, akkor visszaadja, hogy Hello World! I am .... (hostname, ami majd a futattó dockerkonténer ID-je lesz) és
- docker-swarm-mal orchestráljuk a node 1-3-ra, akár több példányban - tehát több konténer node-onként, hogy a load-balancing működjön.
---------------
Target:
- there will be 4 Virtualbox VMs, one control (C), the rest only node (N) 3 pcs
- install on C and run ansible from there and control node 1-3 from there
- configure the ansible node group based on the myhost file so that the nodes can communicate
- have Python-simplejson on node 1-3 - put this on each with the Ansible nodes command to make ansible more functional
- have docker and docker-compose on node 1-3 and vagrant user added to docker group - this should be done with Ansible playbook.yml
- With Dockerfile, we install a python app running in flask, which, if queried on port 5000, returns Hello World! I am .... (hostname, which will be the ID of the runner dock container) and
- orchestrate with docker-swarm to node 1-3, even in multiple instances - so multiple containers per node for load-balancing to work.
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
