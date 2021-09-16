# MXroute

* [Email Hosting](https://mxroute.com/)

## Add DNS records in your domain provider

Domain		Priority	TTL	Value \
domain.com	MX1	10		600	echo.mxrouting.net \
domain.com	MX2	20		600	echo-relay.mxrouting.net

2 TXT records from mx routing direct admin > [DKIM Keys](https://echo.mxrouting.net:2222/user/dns)

## FAQ

* [Resolve the "CharacterStringTooLong (Value is too long) encountered with {Value}" Error When Creating a DNS TXT Record](https://aws.amazon.com/premiumsupport/knowledge-center/route53-resolve-dkim-text-record-error/)
