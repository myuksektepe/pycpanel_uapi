# pycpanel_uapi
Bununla cPanel UAPI'ı basit ve hızlı şekilde kullanabilirsiniz.


Örnek

```
cp = pycpanel_uapi.connect(
    hostname='SERVER_HOST_NAME',
    username='muratyuksektepe',
    password='ÇOKGİZLİŞİFRE',
)
params = {
    'email': 'deneme',
    'password': 'P4SSw0rd',
    # 'quota': 0,
    # 'domain': 'muratyuksektepe.com',
    # 'skip_update_db': 1,
}
add_pop = cp.doit(module='Email', function='add_pop', parameters=params)
```


add_pop ve diğer bütün işlemler için cPanel'in kendi dokümanlarını inceleyiniz; https://docs.cpanel.net/display/DD/UAPI+Functions+-+Email%3A%3Aadd_pop
