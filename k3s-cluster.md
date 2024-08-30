## Installing k3s on centos 

### Install Script[​](https://docs.k3s.io/quick-start#install-script "Direct link to Install Script")

K3s provides an installation script that is a convenient way to install it as a service on systemd or openrc based systems. This script is available at  [https://get.k3s.io](https://get.k3s.io/). To install K3s using this method, just run:

```
curl -sfL https://get.k3s.io | sh -
```

After running this installation:

-   The K3s service will be configured to automatically restart after node reboots or if the process crashes or is killed
-   Additional utilities will be installed, including  `kubectl`,  `crictl`,  `ctr`,  `k3s-killall.sh`, and  `k3s-uninstall.sh`
-   A  [kubeconfig](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/)  file will be written to  `/etc/rancher/k3s/k3s.yaml`  and the kubectl installed by K3s will automatically use it

### Manual Configuration after installation
- Add **/usr/local/bin** to your PATH if it is missing:
	```
	export PATH=$PATH:/usr/local/bin
	```
- Make this change permanent by adding it to your .bashrc or .bash_profile:
	```
	echo 'export PATH=$PATH:/usr/local/bin' >> ~/.bashrc
	source ~/.bashrc
	```
- Set the **KUBECONFIG** environment variable:
	```
	echo 'export KUBECONFIG=/etc/rancher/k3s/k3s.yaml' >> ~/.bashrc
	source ~/.bashrc
	```
### Join the worker nodes to master for the multi node cluster
Spin 2 more vms ( 1 master & 2 worker nodes ) and change the hostname of the worker nodes. The names must be exclusive otherwise they won't get added to the cluster. 
```
curl -sfL https://get.k3s.io | K3S_URL=https://myserver:6443enter code here K3S_TOKEN=mynodetoken sh -
```
Setting the `K3S_URL` parameter causes the installer to configure K3s as an agent, instead of a server. The K3s agent will register with the K3s server listening at the supplied URL. The value to use for `K3S_TOKEN` is stored at `/var/lib/rancher/k3s/server/node-token` on your server node.

#### Good to know
- IP of master node:  `kubectl get nodes -o wide` on master
- No need to install anything on the worker nodes as k3s script takes care of the installations. 
- It can take up to 25 minutes for the worker node to join the master. 
