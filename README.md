Ansible issue certification
=========

透過 ansible 的 `acme_certificate` 以及相關的 `DNS module` 來完成自動申請 HTTPS 證書。

Requirements
------------

- python >= 2.6
- either openssl or cryptography >= 1.5


Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml):

Account key 相關設定
```
## ACME account-key 存放的位置
acme_account_key_path: '/data/ansible-acme'
## 是否強制重新生成 account-key，如果需要重新生成的話，請改成 yes
acme_account_key_regen: no
```

AMCE 相關設定
```
## ACME 存放 HTTPS certs 跟 key 的位置。
acme_certs_path: '/data/ansible-acme/certs'
## ACME 第三方，可以使用 letsencrypt 或是 buypass
acme_third_party: letsencrypt
## 生成環境 production 或是 staging
acme_enviroment: production
## ACME 版本，可以是 1 or 2 ，預設為 2
acme_version: 2
## ACME challenge mode，目前只有開發 dns-01
acme_challenge: dns-01
## 證書有效期限小於 60 天時會重新生成
acme_remaining_days: 60
## 是否開啟 debug log
debug_log: False
```

DNS 廠商設定
```
## 設定使用哪一家DNS進行驗證。
dns_third_party: cloudflare
## 要申請證書的域名
acme_dns_data:
  - { "zone": "ly-uat.com", "subjectAltName": ["ly-uat.com","*.ly-uat.com"] }
```

Cloudflare 設定，如使用 cloudflare，必填
```
cloudflare_email:
cloudflare_api_token:
```

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

This role was created in 2020 by Renato Li.
