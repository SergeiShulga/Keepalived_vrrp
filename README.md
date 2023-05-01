# Keepalived_vrrp
#### 10.1 «Keepalived/vrrp» - Сергей Шульга

Задание 1
Разверните топологию из лекции и выполните установку и настройку сервиса Keepalived.
В качестве решения предоставьте:
- рабочую конфигурацию обеих нод, оформленную как блок кода в вашем md-файле;
- скриншоты статуса сервисов, на которых видно, что одна нода перешла в MASTER, а вторая в BACKUP state.
                                                                                       
  vrrp_instance test {
  state MASTER
  interface enp0s8
  virtual_router_id 10
  priority 110
  advert_int 4
  authentication {
  auth_type AH
  auth_pass 1234
  }
  unicast_peer {
  192.168.56.103
  }
  virtual_ipaddress {
  192.168.56.200 dev enp0s8 label vip
  }
  }


< >                                                                                         
vrrp_instance test {
state BACKUP
interface enp0s8
virtual_router_id 10
priority 110
advert_int 4
authentication {
auth_type AH
auth_pass 1234
}
unicast_peer {
192.168.56.102
}
virtual_ipaddress {
192.168.56.200 dev enp0s8 label vip
}
}
>
![alt text](https://github.com/SergeiShulga/Keepalived_vrrp/blob/main/img/VirtualBox_host%202.png)
![alt text](https://github.com/SergeiShulga/Keepalived_vrrp/blob/main/img/VirtualBox_host%203.png)

Дополнительные задания со звёздочкой*
Эти задания дополнительные. Их можно не выполнять. На зачёт это не повлияет. Вы можете их выполнить, если хотите глубже разобраться в материале.

Задание 2*
Проведите тестирование работы ноды, когда один из интерфейсов выключен. Для этого:

добавьте ещё одну виртуальную машину и включите её в сеть;
на машине установите Wireshark и запустите процесс прослеживания интерфейса;
запустите процесс ping на виртуальный хост;
выключите интерфейс на одной ноде (мастер), остановите Wireshark;
найдите пакеты ICMP, в которых будет отображён процесс изменения MAC-адреса одной ноды на другой.
В качестве решения пришлите скриншот до и после выключения интерфейса из Wireshark.
