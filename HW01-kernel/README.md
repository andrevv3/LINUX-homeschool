### Сборка собственного ядра

обновляем программное обеспечение и устанавлимаем инструменты для разработки, необходимые для компиляции ядра...
```
yum update
yum install -y ncurses-devel make gcc bc bison flex elfutils-libelf-devel openssl-devel grub2
```

просмотр текущей версии ядра
`rpm -qa kernel` vs `uname -r`

скачиваем и извлекаем нужную версию ядра
```
cd /usr/src/
wget https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.20.tar.xz
tar -xvf linux-4.20.tar.xz
rm -f linux-4.20.tar.xz
```

копируем текущую конфигурацию ядра
`cp -v /boot/config-3.10.0-1062.12.1.el7.x86_64 /usr/src/linux-4.20/.config`

выполняем конфигурирование ядра (make oldconfig использовать конф. старого ядра, make oldconfig создать конф по умолчанию)
`cd /usr/src/linux-4.20/ && make menuconfig`

запускаем сборку (-j 4 кол-во потоков)
`make -j 4`

выполняем установку (файл будет помещён  каталог в /boot, и внесены изменения в /boot/grub/grub.conf)
`make install && make modules_install`
