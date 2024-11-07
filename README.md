# Asuswrt-Merlin DDNS for CloudFlare

This is a custom shell script for Asuswrt-Merlin router firmware to update DDNS via CloudFlare for IPv4

## Notice

This script is run in version 3.0.0.6.102, in other version is not be checked. I can't Run `ddns-start` success in crontab, Because the `curl` command can't be run success.


## Setup

1. Add an `A record` in [CloudFlare](https://www.cloudflare.com/) for your domain. IP for the record can be anything since the script will overwrite it later anyway.

1. Download [ddns-start](ddns-start) script and modify the following variables with your own settings:

   | Variable      | Description                                                                                                                                                                                                                                                                                     |
   | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
   | `API_TOKEN`   | Your API Token generated from the [User Profile 'API Tokens' page](https://dash.cloudflare.com/profile/api-tokens). I recommend creating a token with minimal access to limit exposure:<br />**Permission**: Zone > DNS > EDIT<br />**Zone Resources**: Include > Specific Zone > \<your zone\> |
   | `ZONE_ID`     | Your Zone ID, hex16 string                                                                                                                                                                                                                                                                      |
   | `RECORD_NAME` | Your DNS record name, e.g. host.example.com                                                                                                                                                                                                                                                     |
   | `RECORD_TTL`  | TTL for the record in seconds, defaults to 1 (auto)                                                                                                                                                                                                                                             |


1. SSH to your router and place `ddns-start` under `/jffs/scripts/`

1. Make sure it's executable `chmod +x /jffs/scripts/ddns-start`

1. Add crontab 

   1. edit file `init-start` under `/jffs/scripts/`
      ```shell
      #!/bin/sh
      cru a ScheduleDDNS "*/15 * * * * /jffs/scripts/ddns-start"
      ```
   1. Make sure it's executable `chmod +x /jffs/scripts/init-start`
   1. Run the script /jffs/scripts/init-start manually.


## References

- <https://github.com/alphabt/asuswrt-merlin-ddns-cloudflare>
- <https://github.com/RMerl/asuswrt-merlin.ng/wiki/Custom-DDNS>
- <https://github.com/RMerl/asuswrt-merlin.ng/wiki/User-scripts>
