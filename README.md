# **Домашнее задание №1**
**Цель:** Получить навыки работы с Git, Vagrant, Packer и публикацией готовых образов в Vagrant Cloud.

## **Задание**
Обновить ядро в базовой системе.

## **Выполнено**

1. Подготовлен и развернут стенд на платформе Centos 7.
2. На стенде установлено необходимое ПО:
- Git
- Vagrant
    - VirtualBox Guest Additions install:
```
    vagrant plugin install vagrant-vbguest
```
- Packer
3. Сконфигурирован и запущен с помощью Vagrant экземпляр виртуальной машины.
4. Обновлено ядро и произведены настройки загрузчика в запущенной виртуальной машине:

sudo yum install -y http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
sudo yum --enablerepo elrepo-kernel install kernel-ml -y
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
sudo grub2-set-default 0

5. С помощью установленной утилиты packer создан свой образ системы, с уже установленым ядром 5й версии.
```
packer build centos.json
```