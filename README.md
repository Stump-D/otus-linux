# **Домашнее задание №1**
**Цель:** Получить навыки работы с Git, Vagrant, Packer и публикацией готовых образов в Vagrant Cloud.

## **Задание**
Обновить ядро в базовой системе.

## **Выполнено**

1. Подготовлен и развернут стенд на платформе Centos 7.
2. На стенде установлено необходимое ПО:
- Git
- Vagrant 
```Bash
wget https://releases.hashicorp.com/vagrant/2.2.6/vagrant_2.2.6_x86_64.rpm
yum install vagrant_2.2.6_x86_64.rpm
```
- VirtualBox Guest Additions install
```Bash
vagrant plugin install vagrant-vbguest
```
- VirtualBox: <https://www.tecmint.com/install-virtualbox-on-redhat-centos-fedora>

- Packer

```Bash
curl https://releases.hashicorp.com/packer/1.4.4/packer_1.4.4_linux_amd64.zip | \
sudo gzip -d > /usr/local/bin/packer && \
sudo chmod +x /usr/local/bin/packer
```

3. Сконфигурирован и запущен с помощью Vagrant экземпляр виртуальной машины.
4. Обновлено ядро и произведены настройки загрузчика в запущенной виртуальной машине:
```Bash
sudo yum install -y http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
sudo yum --enablerepo elrepo-kernel install kernel-ml -y
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
sudo grub2-set-default 0
```

5. С помощью установленной утилиты packer создан свой образ системы, с уже установленым ядром 5й версии.
```Bash
packer build centos.json
```

6. Импорт созданного образа в Vagrant:
```Bash
vagrant box add --name centos-7-5 centos-7.7.1908-kernel-5-x86_64-Minimal.box
```
