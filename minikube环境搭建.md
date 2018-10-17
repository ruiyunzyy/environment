1. 查看你的CPU是否支持虚拟化

```bash
intel: grep -E 'vmx' /proc/cpuinfo
amd: grep -E 'svm' /proc/cpuinfo
```

如果出现如下的字样说明你的cpu是支持虚拟化的

vmx

vmx intel


2. 安装KVM

```bash
yum install qemu-kvm qemu-img virt-manager libvirt libvirt-python libvirt-client virt-install virt-viewer bridge-utils
```

3. 启动libvirtd

```bash
systemctl start libvirtd
systemctl enable libvirtd
```

4. 检查kvm module 是否加载成功

```bash
lsmod | grep kvm
kvm_intel             162153  0
kvm                   525409  1 kvm_intel
```

5. 安装kubectl

> 参考文献 https://kubernetes.io/docs/tasks/tools/install-kubectl/

配置代理

```bash
export https_proxy=http://<your_proxy>
export http_proxy=http://<your_proxy>
```

配置google源

```bash
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
> [kubernetes]
> name=Kubernetes
> baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
> enabled=1
> gpgcheck=1
> repo_gpgcheck=1
> gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
> EOF
```

安装

```bash
yum install -y kubectl
```

6. 安装minikube

```bash
# 官方下载
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/

# 阿里云下载
curl -Lo minikube http://kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/releases/v0.28.0/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```

7. 安装驱动

> 参考: https://github.com/kubernetes/minikube/blob/master/docs/drivers.md#kvm-driver
> https://github.com/kubernetes/minikube/blob/master/docs/drivers.md#kvm2-driver
> 

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/docker-machine-driver-kvm2 && chmod +x docker-machine-driver-kvm2 && sudo mv docker-machine-driver-kvm2 /usr/local/bin/
```

8. 启动minikube

```bash
minikube start --registry-mirror=https://registry.docker-cn.com --docker-env HTTP_PROXY=http://<your_proxy> --docker-env HTTPS_PROXY=http://<your_proxy>
```