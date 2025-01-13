# Deploy a Production Ready Kubernetes Cluster + ceph + prometheus + calico

![Kubernetes Logo](https://raw.githubusercontent.com/kubernetes-sigs/kubespray/master/docs/img/kubernetes-logo.png)

#instruction

0. # get credentials for ceph and get access to ssh of your nodes using certificates
   # example
" key = AQA8T1dnaWSvIxAAVWmmg+16v+LtXp0IKBZy8Q== "
" caps mon = "allow r" "
" caps osd = "allow rwx pool=ceph-volume" "

1. # install need app
   sudo apt update && sudo apt install -y python3-pip git ansible
pip install --upgrade pip
2. # Clone this repository
    git clone  https://github.com/DanilenkA/k8spython3 -m venv ~/kubespray-venv-pub.git && cd k8s-pub
3. # install environment
   python3 -m venv ./kubespray-venv
   source /kubespray-venv/bin/activate
   pip install -U pip
   pip install ansible
   pip install -r requirements.txt
4. # Change the configuration to suit your infrastructure
   inventory/sample inventory/mycluster
   inventory/mycluster/group_vars/all.yml
   inventory/mycluster/group_vars/k8s_cluster/k8s-cluster.yml
   roles/kubernetes-apps/csi_driver/ceph/ceph_secret.yaml
6. # deploy your cluster (here is the user k8s, change it to yours)
   ansible-playbook -i inventory/mycluster/inventory.ini cluster.yml -b -v
7. # check
   kubectl get nodes
   helm version
   kubectl get pods -n monitoring | grep prometheus
   kubectl describe sc
   

   
