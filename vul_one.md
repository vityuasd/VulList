## Description
In [Akaunting](https://github.com/akaunting/akaunting) versions 3.0.4 to 3.1.19, authenticated attackers can exploit a persistent XSS or redirection vulnerability by injecting \<a\> tag into the `name` field of reports at /common/reports .
## Environment
- **Operating System** : docker
-  **Mysql Version**  : 8.4
-  **Affected Version** : 3.0.4 to 3.1.19

## PoC
1. Log in
2. visit http://<host>/<id>/common/reports
3. Edit the target component's name field and input: `<a href="https://google.com">test</a>`

4. Save the changes.



Observe that clicking the hyperlinked text "test" triggers a redirect to google.com


## Screenshots
<img width="853" height="609" alt="image" src="https://github.com/user-attachments/assets/13ad03d3-a8d5-432e-9be3-d77ebd132a01" />
<img width="594" height="123" alt="image" src="https://github.com/user-attachments/assets/4b65b776-d800-460e-9122-4c710bda2469" />

## Vulnerable Code Location:  
`resources\views\common\reports\index.blade.php`,
specifically at: 
```php
<x-link.hover group-hover>
{!! $report->name !!}
</x-link.hover>

