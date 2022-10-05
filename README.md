# Proofpoint TAP API Command Line Query Tool

This tool implements all of the functions of the TAP 2.0 API and provides access to these functions via a BASH script. 

### Requirements:
* bash
* curl
* hexdump (for stdout ouput)
* xxd (for stdout ouput)

### Configuration
Edit the tap_query script and modify the following values at the top of the script:
```
declare -r PRINCIPAL="<enter_principal_here>"
declare -r SECRET="<enter_secret_here>"
```

### Top Level API Options
![command_line_options_main](https://user-images.githubusercontent.com/83429267/194107940-244e0315-c6b6-4c5e-bcbe-252253d4ede2.png)


### SIEM API Options
![command_line_options_siem](https://user-images.githubusercontent.com/83429267/194108181-5f5d6a2e-a300-47ac-a4f3-3c96a0b7b244.png)

### Forensics API Options
![command_line_options_forensics](https://user-images.githubusercontent.com/83429267/194108442-aa537093-4c34-4e8e-81db-ff349161cf71.png)

### Campaign API Options
![command_line_options_campaign](https://user-images.githubusercontent.com/83429267/194108854-0603891e-9a4d-4ce0-8eef-d84019ed1695.png)

### People API Options
![command_line_options_people](https://user-images.githubusercontent.com/83429267/194108890-d3a01db9-91be-48c5-9dbc-c40b9728f030.png)

### Threat API Options
![command_line_options_threat](https://user-images.githubusercontent.com/83429267/194108922-4ff42caf-8eea-404d-bdb0-f52d64c0a517.png)

# Typical SIEM API Usage Examples

Although the tool is self explanatory, this section provides some common use usage.

```
# Hourly Query for Cron Jobs for All Alerts (SYSLOG,JSON)
pfpt_api --siem-api --all  --range-start "now - 1 hour" --range-end "now"  --format-syslog --output /tapquery/outputfolder/$(date +%Y%m%d%H%M%S).syslog

pfpt_api --siem-api --all  --range-start "now - 1 hour" --range-end "now"  --format-json --output /tapquery/outputfolder/$(date +%Y%m%d%H%M%S).json
```

The 12 hour limit is not a limit on the script but rather a limit on the API.

```
# Past 12 Hours (SYSLOG,JSON)
pfpt_api ---siem-api --all  --range-start "now - 12 hour" --range-end "now"  --format-syslog --output /tapquery/outputfolder/PAST_TWELVE_HOURS_$(date +%Y%m%d%H%M%S).syslog

pfpt_api ---siem-api --all  --range-start "now - 12 hour" --range-end "now"  --format-json --output /tapquery/outputfolder/PAST_TWELVE_HOURS_$(date +%Y%m%d%H%M%S).json
```

Using --range-start --range-end
```
# Past Hour to STDOUT (SYSLOG,JSON)
pfpt_api --siem-api --all  --range-start "now - 1 hour" --range-end "now"  --format-syslog 

pfpt_api --siem-api --all  --range-start "now - 1 hour" --range-end "now"  --format-json
```

Using --since-seconds
```
# Past 3600 seconds to STDOUT (SYSLOG,JSON)
pfpt_api --siem-api --all  --since-seconds 3600 --format-syslog 

pfpt_api --siem-api --all  --since-seconds 3600 --format-json
```

# Typical Forensics API Usage Examples

Using --threat-id
```
pfpt_api --forensics-api --threat-id <threat_id>   
```
Using --threat-id + campaign forensics
```
pfpt_api --forensics-api --threat-id <threat_id>   --campaign-forensics
```
Using --campaign-id
```
pfpt_api --forensics-api --campaign-id <campaign_id>
```
Typical Campaign API Usage Examples
Using --campaign-id
```
pfpt_api --campaign-api --campaign-id   
```
# Typical People API Usage Examples
Using --people-api (14 day, 30 day, 90 day)
```
pfpt_api --people-api --vap --window-14

pfpt_api --people-api --vap --window-30

pfpt_api --people-api --vap --window-90
```

Using --people-api --clickers (14 day, 30 day, 90 day)
```
pfpt_api --people-api --clickers --window-14

pfpt_api --people-api -clickers --window-30

pfpt_api --people-api -clickers --window-90
```

# Revisions
10/18/2016 - Initial Release  
11/19/2016 - Added API selector  
11/20/2016 - Added Forensics API  
11/20/2016 - Added Campaign API  
11/23/2016 - Added rest_call function for generic API calls  
04/03/2017 - Fixed --output switch bug  
05/31/2019 - Fixed --interval format validation  
05/31/2019 - Fixed issues with UTC dates using --data-urlencode for curl  
02/04/2020 - Added People API VAPs  
06/06/2020 - Fixed CURL rvalue issue  
05/19/2021 - Added People API Clickers  
08/30/2021 - Fixed bug help output for People API  
05/03/2022 - Added Threat API Support  
07/25/2022 - Fixed bug in range based searching temp files failing  
07/27/2022 - Improved the range based search and using PID for unique log
