# فیلترشکن چندگانه

در این مقاله به شما آموزش میدهیم چگونه یک فیلترشکن اختصاصی مالتی پروتوکل در پورت 443 ایجاد کنید. موارد پشتیبانی شده:

<details>

<summary>Telegram MTProxy Proxy</summary>

پروکسی ایجاد شده یک پروکسی faketls هست که در صورتی که کلاینت غیر تلگرام به آن متصل شود سایت گوگل را نشان می‌دهد.

`(faketls domain=mail.google.com)`

</details>

<details>

<summary>Shadowsocks+obfs</summary>

پروکسی شدوساکس مشابه پروکسی تلگرام فوق، از faketls استفاده میکند تا ترافیک شدوساکس را پنهان کند.

`faketls domain=www.google.com`

</details>

<details>

<summary>Shadowsocks+v2ray (cdn support)</summary>

این پروکسی، از v2ray استفاده میکند و یک زیرمسیر از سایت که با tls و http2 فعال است استفاده میکند

</details>

<details>

<summary>vmess (cdn support)</summary>

Same as v2ray

</details>

<details>

<summary>DNS over HTTPS (cdn support)</summary>

برای استفاده از DNS over HTTPS کافی است در مرورگر از dns زیر استفاده کنید:

`https://yourdomain.com/yoursecret/dns/dns-query{?dns}`

</details>

<details>

<summary>Redirector (cdn support)</summary>

نکته این امر آن است که برای مثال وقتی میخواهید پروکسی تلگرام یا پروکسی شدوساکس را از طریق برنامه های دیگر به اشتراک بگذارید امکان آن فراهم می شود. برای مثال اگر کانفیگ شدوساکس را به جای `fullURL` آن قرار دهید باعث میشود با کلیک بر روی این لینک، نرم افزار شدوساکس باز شده و پروکسی بر روی آن فعال شود.

`https://yourdomain.com/yoursecret/redirect/fullURL`

به عنوان مثال:

`https://yourdomain.com/yoursecret/redirect/ss://secret/`

</details>

<details>

<summary>پروکسی هوشمند برای سایت های غیر ایرانی و فیلترشده</summary>

با استفاده از کلاینت کلش و کانفیگی که درست کردیم میتوانید در 3 مود به اینترنت وصل بشید.

* روش اول فقط سایت فیلترشده را از فیلترشکن عبور دهد.
  * مشکلات:
    * در شرایط فیلترینگ شدید الان که تقریبا همه سایت ها فیلتر شده یک مقدار خوب نیست
    * سایت هایی که ایران را تحریم کرده اند کار نمیکنند
* فقط سایت های ایرانی بدون فیلترشکن باز شود (پیشنهادی)
* تمام سایت ها از فیلترشکن عبور کنند
  * مشکلات:
    * سرعت بازدید از صفحات ایرانی کمتر شود
    * باعث شود سرور شما سریعتر شناسایی شود

کانفیگ اول یا دوم کمک به دیرتر شناسایی شدن پروکسی میکند و کانفیگ سوم ممکن است

</details>

<details>

<summary>مقاوم در برابر کشف توسط فیلترچی</summary>

سعی شده جلوی حملات معمول به سرور گرفته شود و امکان شناسایی حداقل باشد با این وجود فراموش نکنید که سایر پورت ها به جز 22، 80 و 443 را غیر فعال کنید

</details>

<details>

<summary>صفحات راهنمای کاربران</summary>



</details>

<details>

<summary>Open Source</summary>

کلیه سورس کدها در [گیت هاب](https://github.com/hiddify/hiddify-config)

</details>

## پیش نیازها:

* یک vps آماده با ubuntu 20.04 و آی پی مثلا `1.1.1.1`
* یک دامنه یا زیردامنه (برای مثال: `myservice.hiddify.com`) که رکورد A ی آن به آی پی شما وصل باشد. اگر زیر دامنه ندارید از این لینک یک زیر دامنه برای خود بسازید

#### مرحله 1: پارامترها

ابتدا دامنه خود را در بخش زیر قرار دهید.

domainsecret

#### مرحله 2: چک کردن آنکه این زیر دامنه به آی پی متصل است

با کلیک بر روی دکمه [check](https://mxtoolbox.com/SuperTool.aspx?action=a%3amyservice.hiddify.com\&run=toolpage) چک کنید که زیر دامنه درست به IP اشاره میکند. اگر تازه انجام داده اید و در بالا IP سرور خود را نمی بینید 5 دقیقه صبر کنید و مجدد تست کنید

#### مرحله 3: اجرای اسکریپت

به سرور خود با ssh متصل شوید و دستور زیر را اجرا کنید

```
bash <(curl -sL https://raw.githubusercontent.com/hiddify/config/main/install.sh) 0ba19c4c14b8699ff6070e75379cdcfd myservice.hiddify.com all myservice.hiddify.com
```

پس از اجرای موفقیت آمیز، سرور ری استارت میشود و با کلیک بر روی لینک زیر میتوانید جزییات کانفیگ سمت کلاینت سرور را ببینید: [تنظیمات اختصاصی برای کلاینت ها](https://myservice.hiddify.com/751F2F753854422EA4C5FDDB8314F068/)

توجه داشته باشید که لینک را حتما کپی کنید. این لینک به صورت تصادفی ایجاد شده و با ریفرش شدن صفحه تغییر میکند پس آن را در جای امنی ذخیره کنید

## تنظیمات پیشرفته

<details>

<summary>نصب مجدد</summary>

ابتدا دستور زیر را اجرا کنید و سپس دستورات بالا را مجدد اجرا کنید.

```
rm -rf /opt/hiddify-config/ 
```

</details>

<details>

<summary>نصب فقط بخشی از پروکسی ها</summary>

کافی است که به جای عبارت all در دستور بالا، یکی از عبارت های `telegram-shadowsocks-vmess` را قرار دهید یا دوتا را با - کنار هم قرار دهید. مثل `telegram-vmess`

</details>

<details>

<summary>CDN Support</summary>

برای سرعت بالاتر و گذر از اینترانت کافی است که یک دامنه خریداری کنید (برای مثال از [اینجا به قیمت 1 دلار](https://www.namecheap.com/promos/99-cent-domain-names/) یا [اینجا رایگان](https://www.freenom.com/)

* قبل از خرید دامنه ابتدا دامنه را چک کنید که در ابرآروان مورد پذیرش قرار دهد
* سپس یک اکانت در ابرآروان ایجاد کنید میتوانید با یک شماره خارجی اینکار را انجام دهید
* سپس nameserver بر روی دامنه ای که خریداری کرده اید را مطابق اعلامی ابرآروان پر کنید
* سپس روی زیر دامنه دلخواه، آی پی سرور را تنظیم کنید و تیک کلود سرویس را تنظیم کنید و سپس به جای `myservice.hiddify.com` زیردامنه جدید خود را تنظیم کنید. لازم است این زیر دامنه با دامنه ای که در بالا انتخاب کرده اید متفاوت باشد.
* سپس لینک زیر را با تغییر در نامه دامنه در مرورگر جهت مشاهده تنظیمات باز کنید.

```
       https://myservice.hiddify.com/751F2F753854422EA4C5FDDB8314F068/
```

در زیر توضیحات با تصویر نشان داده شده است.

#### 2. Arvancloud setup

1. Log in to the Arvancloud account and add your domain.

```
Domain List > Add new domains
```

<img src="https://raw.githubusercontent.com/WeAreMahsaAmini/FreeInternet/main/protocols/media/arvanclound_adddomain.jpg" alt="Arvancloud dashboard > Add new domain" data-size="original">

Then:

* Enter your domain name
* Select Free plan
* Skip DNS Records
* Note the nameservers presented on the last step

<img src="https://raw.githubusercontent.com/WeAreMahsaAmini/FreeInternet/main/protocols/media/arvanclound_nameservers.jpg" alt="Add new domain > Nameservers" data-size="original">

* Go to your domain registrar (the website where you bought your domain, e.g. Godaddy, Namecheap, ...)
* Update the nameservers to the one you got in Arvancloud (after adding the domain).

After your domain nameservers changed successfully (depending on the registrar, it can take a few hours, but it's usually quite fast), your domain is now using Arvancloud DNS.

1. Connect your domain to your server's IP address using `A` records. Make sure the `Cloud Service` option is enabled for each record. ![Add new domain > Nameservers](https://raw.githubusercontent.com/WeAreMahsaAmini/FreeInternet/main/protocols/media/arvanclound\_add\_dns.jpg)
2. Go to `HTTPS settings` on the navbar, select `Issue certificate`. It will take around 30 minutes for the certificate to be ready.
3. After the certificate is issued, enable the `Activate HTTPS` option. ![HTTPS Settings > Activate HTTPS](https://raw.githubusercontent.com/WeAreMahsaAmini/FreeInternet/main/protocols/media/arvanclound\_https.jpg)

(توضیحات بخش CDN برگرفته از دوستان FreeInternet)\[https://github.com/WeAreMahsaAmini/FreeInternet/tree/main/protocols/shadowsocks-v2ray-tls]

## اگر از ابرآروان استفاده میکنید

به جای زیر پارامتر چهارم در اسکریپت فوق عبارت arvancloud.com را قرار دهید.

const genRanHex = size => \[...Array(size)] .map(() => Math.floor(Math.random() \* 16).toString(16)).join(''); document.getElementById("usersecret").value=genRanHex(32); codes=document.getElementsByTagName('code'); as=document.getElementsByTagName('a'); default\_contents={'code':{},'a':{\}} function replace\_info(str){ var host = document.getElementById("userdomain").value; var secret = document.getElementById("usersecret").value; str=str.replaceAll('myservice.hiddify.com',host); str=str.replaceAll('751F2F753854422EA4C5FDDB8314F068',secret); return str; } for (i=0; i\<codes.length;i++){ default\_contents\['code']\[i]=codes\[i].innerHTML; } for (i=0; i\<as.length;i++){ default\_contents\['a']\[i]={'href':as\[i].href,'inner':as\[i].innerHTML} } function handleValueChange(){ for (i=0; i\<codes.length;i++){ codes\[i].innerHTML=replace\_info(default\_contents\['code']\[i]); } for (i=0; i\<as.length;i++){ as\[i].href=replace\_info(default\_contents\['a']\[i]\['href']); as\[i].innerHTML=replace\_info(default\_contents\['a']\[i]\['inner']); } } handleValueChange();

</details>
