Kroki wykonane w realizacji zadania:
- po imporcie vmki zalogowałem się na usera zdt i sprawdziłem połaczenie z siecią, działajace procesy i uprawnienia usera
- zastanawiałem się czy to, że już działa docker to jakiś podstep, sprawdziłem czy nie ma już działajacych kontenerów/cronów/skryptów robiacych coś podejrzanego
- zrestartowałem maszyne i zresetowałem hasło do konta root
- nie działało resolvowanie adresów, dodałem dns do skryptu dla NATowego interfejsu sieciowego w /etc/sysconfig/network-scripts, zrestartowałem network manager
- wyrzuciłem immutable z /etc/resolv.conf, zrestartowałem network managera jeszcze raz
- puściłem dnf install httpd -> installing package httpd-filesystem-2.4.37-21.module_el8.2.0+382+15b0afa8.noarch needs 2 inodes on the /var/www filesystem
- początkowo wydawalo mi się, że 2.6MB w /var/www to moze być za mało miejsca ale przy okazji odkryłem, ze /var/www jest zamonotowane jako RO
- zremountowałem /var/www na rw i wywaliłem ro z /etc/fstab dla /var/www
- instalacja pakietu httpd przeszła, wystartowałem i enablowałem usługe httpd
- przez firewall-cmd dodałem service http i https
- potwierdziłem, że defaultowa strona apacha jest dostepna przez http://192.168.56.10/ w przegladarce
- pobrałem i rozpakowałem (unzipem) http://kotewa.com.pl/files/www.tar.gz
- jednak 2.6MB to za mało miejsca, zastapiłem /var/www/html linkiem do innej lokalizacji
- skopiowałem zawartość www.tar.gz do /var/www/html
- zakomentowałem welcome.conf i zezwoliłem na dostep do /var/www/html w /etc/httpd/conf/httpd.conf
- potwierdziłem, ze stronka działa w przegladarce
- zrestartowałem maszyne, żeby sprawdzić czy dalej bedzie działać
![](itsalive.png)