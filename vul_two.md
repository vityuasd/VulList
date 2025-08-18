## Description
In [Akaunting](https://github.com/akaunting/akaunting) versions 3.1.19 and earlier, authenticated attackers can send POST request sent to settings/localisation, when modifying the timezone to a non-existent or incorrect value, it causes a denial of service and returns a 500 Internal Server Error.
## Environment
- **Operating System** : docker
-  **Mysql Version**  : 8.4
-  **Affected Version** : 3.1.19 and earlier

## PoC
1. Log in
2. visit `http://<host>/<id>/settings/localisation` and click save

modify the request
```
<non-existent or incorrect value>
------WebKitFormBoundaryRWG4Ala2wgozDmly
Content-Disposition: form-data; name="timezone"
```
Noticed that after refreshing, it returned a 500 error page.

## Screenshots
<img width="687" height="512" alt="image" src="https://github.com/user-attachments/assets/a285cf39-b6b4-4449-b0b0-ad79ec2dca12" />

## Vulnerable Code Location:  
The code in `\app\Utilities\Overrider.php` uses `date_default_timezone_set(config('app.timezone'))` without first validating the app.timezone value.
