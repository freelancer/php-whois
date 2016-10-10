# php-whois2

Fork of php-whois, a PHP class to retrieve WHOIS information. You can view the original codebase here: https://github.com/regru/php-whois

## Differences with php-whois

**TL;DR this allows lookups with `=domain` syntax.**

WHOIS allows lookups in the form of `=domain` to single out domains registered with different registrars (e.g. `gmail.com`) and return its full lookup info.

Otherwise, simply looking up with `domain` (without the `=`) for certain domains will yield a notice from WHOIS to specify the search. For example, in looking up `gmail.com`, we get the following response:

```
Whois Server Version 2.0

Domain names in the .com and .net domains can now be registered
with many different competing registrars. Go to http://www.internic.net
for detailed information.

GMAIL.COM.BR
GMAIL.COM.DEADKNIFERECORDS.COM
GMAIL.COM.MY
GMAIL.COM.TEJAARH.COM
GMAIL.COM

To single out one record, look it up with &quot;xxx&quot;, where xxx is one of the
records displayed above. If the records are the same, look them up
with &quot;=xxx&quot; to receive a full display for each record.

...
```

Specifying with `=` yields the info we need:

```
string(3620) "Domain Name: gmail.com
Registry Domain ID: 4667231_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.markmonitor.com
...
```

Due to the very immediate need for this, I have decided to create a fork and update from there. This should no longer be a problem once the PR for this is accepted and merged. You can view the PR here: https://github.com/regru/php-whois/pull/64


## Example of usage

```php

<?php

$domain = new Phois\Whois\Whois('=gmail.com');
$domainInfo = $domain->info();
echo domainInfo;
```
