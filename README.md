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
![command_line_options_main](https://user-images.githubusercontent.com/83429267/194098502-a222c83c-61ae-4855-af19-0e4d22c28760.png)

### SIEM API Options
![command_line_options_siem](https://user-images.githubusercontent.com/83429267/194098953-51c5fcde-6c23-4d58-b4ca-49ab0ab52ea8.png)


### Forensics API Options
![command_line_options_forensics](https://user-images.githubusercontent.com/83429267/194099110-7add88c8-33ad-4efb-a2da-fc8944a0964b.png)

### Campaign API Options
![command_line_options_campaign](https://user-images.githubusercontent.com/83429267/194099393-8bc589d7-d234-499a-b2fa-60365b34a95c.png)

### People API Options
![command_line_options_people](https://user-images.githubusercontent.com/83429267/194099469-122688b7-823e-49c2-b649-d6a59a2e5acf.png)

### Threat API Options
![command_line_options_threat](https://user-images.githubusercontent.com/83429267/194099590-de88a301-4b21-4709-8a11-214cfbae3227.png)

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
