# App-Service-troubleshooting

# Log categories

1. AppServiceAuditLogs - Logs generated when publishing users successfully log on via one of the App Service publishing protocols. 
2. AppServiceConsoleLogs - Console logs generated from application or container.
3. AppServiceHTTPLogs - Incoming HTTP requests on App Service. Use these logs to monitor application health, performance and usage patterns.
4. AppServicePlatformLogs - Logs generated through AppService platform for your application.

# Instructions

1. Go to [Azure_Portal](https://azure.microsoft.com/en-us/get-started/azure-portal/) then search `app service` and select `app service`

<img width="964" alt="image" src="https://user-images.githubusercontent.com/46469458/190918854-eab6613c-8d30-4121-95d9-dabe4822564e.png">

2. Select your app service 

<img width="1019" alt="image" src="https://user-images.githubusercontent.com/46469458/190918935-43941919-facc-4791-a2d5-63aad9fbf000.png">

3. At Overview page click on URL to see your web can or cannot access (**this workshop it cannot access**)

<img width="1478" alt="image" src="https://user-images.githubusercontent.com/46469458/190919061-84f3538e-ebda-41c5-ac87-41aa970f39ae.png">

<img width="1080" alt="image" src="https://user-images.githubusercontent.com/46469458/190920460-9fc55511-d1dd-4ba8-b872-7e822241032c.png">

4. Scroll down to Monitoring session and click log stream to see live log

<img width="1471" alt="image" src="https://user-images.githubusercontent.com/46469458/190919233-57f36777-7f97-49c1-b1ca-4bdfa09fbcba.png">

5. Go to Monitoring session and click Logs and close Queries pop up

<img width="1451" alt="image" src="https://user-images.githubusercontent.com/46469458/190919375-9324c61a-4835-4c6f-8a7a-6bfd5a0d8640.png">

6. At query tool paste this query command `AppServicePlatformLogs | where Level == "Error"` and click run 

<img width="808" alt="image" src="https://user-images.githubusercontent.com/46469458/190919512-8ed3189f-40b4-4a4f-96cf-946ed4fec11e.png">

7. Click Display time (UTC+00:00) and change to Local time

<img width="908" alt="image" src="https://user-images.githubusercontent.com/46469458/190919609-23dcbbc8-4276-48f9-8325-88543abb2f5d.png">

8. Then go to last log and click expand ( > ) and go to messege line, you will see error root cause 

<img width="862" alt="image" src="https://user-images.githubusercontent.com/46469458/190919723-30d837c9-4147-4ba9-bb38-291439c2d621.png">

* From error in this workshop root cause is expose wrong port 

9. In this step we will check Dockerfile configuration. In this Dockerfile you will see `EXPOSE 8000` but result from step 8. expose is 8888

<img width="530" alt="image" src="https://user-images.githubusercontent.com/46469458/190920061-c061505f-2fdb-4024-80e8-2f26d1c25d3b.png">

10. At left menu go to Settings --> Configuration, when pop up show click Ok

<img width="1026" alt="image" src="https://user-images.githubusercontent.com/46469458/190920319-a6a20dbb-2e3e-47c8-b686-54bd5fad2247.png">

11. At Configuration page, search form fill `WEBSITES_PORT`, Value column click on `Hidden value. Click to show value` you will see expose port

<img width="933" alt="image" src="https://user-images.githubusercontent.com/46469458/190920546-31d862e1-6232-4a78-b344-23f9b407d5fc.png">

12. Click on `WEBSITES_PORT` and change Value from 8888 to 8000 then click Ok

<img width="364" alt="image" src="https://user-images.githubusercontent.com/46469458/190920764-524f78bd-3b6c-4490-a500-9c3798a3b144.png">

13. Click save

<img width="463" alt="image" src="https://user-images.githubusercontent.com/46469458/190920816-eee421fd-bd2e-46ac-bac4-53ff1cbda2ed.png">

14. When click save you will see confirmation pop up, Click Continue

<img width="837" alt="image" src="https://user-images.githubusercontent.com/46469458/190920864-f0dea9cd-2350-43ce-b35a-3e9bc18b6db1.png">

15. After that wait 2 - 3 minutes for web restart. then try to refresh web page

<img width="1380" alt="image" src="https://user-images.githubusercontent.com/46469458/190921029-7a9ad34d-ebf7-4158-90dd-436212da06b5.png">

16. Back to Log stream you will see log line like this `"GET / HTTP/1.1" 200 7947` that mean your web page is Ok 

<img width="1048" alt="image" src="https://user-images.githubusercontent.com/46469458/190921144-92cac13f-d17e-450c-849f-bd1b3bde39cb.png">

# Metrics

1. Go to Monitoring --> Metrics. At select metric select `Avarage memory working set`

<img width="1362" alt="image" src="https://user-images.githubusercontent.com/46469458/190921400-8eadd576-2241-4d39-806b-c5fb275e6e38.png">

2. Click on + New Chart and add `CPU time`

<img width="1108" alt="image" src="https://user-images.githubusercontent.com/46469458/190921770-18090977-4f9c-45f5-854e-aaacef5cee88.png">

3. Click on + New Chart and add `Htto Server Errors`

<img width="1109" alt="image" src="https://user-images.githubusercontent.com/46469458/190921831-6453b49d-911e-4f7f-9114-a20269cfbbdf.png">

4. When finished you will see 3 charts on Metrics page then go to `Avarage memory working set` to set alert rule

<img width="1051" alt="image" src="https://user-images.githubusercontent.com/46469458/190922031-bfdf74c5-6ec0-458e-899a-739661f40340.png">

5. At Create an alert rule page 

  Operator = Greater than or equal to 
  
  Unit = MB
  
  Threshold value = 60
  
then Click Next: Actions > 

<img width="1472" alt="image" src="https://user-images.githubusercontent.com/46469458/190922124-b8a52d93-956a-48c9-930a-4874e531f2ba.png">

6. At Actions tab select Create action group

<img width="656" alt="image" src="https://user-images.githubusercontent.com/46469458/190922229-04cd3937-d5ad-453d-a109-abdeaf6ce306.png">

7. At Create an action group, specific your action group name then click Next: Notifications

<img width="951" alt="image" src="https://user-images.githubusercontent.com/46469458/190922331-e910b118-e23f-4b79-92a6-df0184edf6ea.png">

8. At Notifications 

  Notification types = Email/SMS Messege/Push/Voice
  Email = Check and fill Recipient 
then click Ok, and create name of notification, Click Next: Actions >

<img width="1380" alt="image" src="https://user-images.githubusercontent.com/46469458/190922490-9e6d71f4-bcdf-4a93-8b5c-093a86cf82b4.png">

9. At Actions tab click Review + create

<img width="524" alt="image" src="https://user-images.githubusercontent.com/46469458/190922693-158a1ca1-0024-40d3-85de-37e2e62faefa.png">

10. Click Create

<img width="947" alt="image" src="https://user-images.githubusercontent.com/46469458/190922759-69d9aa4d-14f4-4a46-9d7d-5a0745197993.png">

11. When back to Create an alert rule click Next Details >

<img width="753" alt="image" src="https://user-images.githubusercontent.com/46469458/190922800-88ba5e27-ab5a-4f89-9caa-e66ea467d742.png">

12. At Details tab select Severity of this alert (default is 3 - Informational) and specific alert rule name then click Review + create

<img width="996" alt="image" src="https://user-images.githubusercontent.com/46469458/190922836-f4548aad-2545-401c-a968-efe3b82b1cf1.png">

13. Review your alert rule and click create

<img width="790" alt="image" src="https://user-images.githubusercontent.com/46469458/190922964-ee2d4e1b-bd0d-4afc-bcc6-8a754cd93ad5.png">

14. Recipient will receive email to confirm 

<img width="966" alt="image" src="https://user-images.githubusercontent.com/46469458/190923048-527c6233-7bc8-4895-ae1b-fa40d09806ba.png">

15. This is alert email

<img width="1140" alt="image" src="https://user-images.githubusercontent.com/46469458/190923235-6d3b29e4-2b16-43d4-a7a9-20111f4cf173.png">
<img width="1162" alt="image" src="https://user-images.githubusercontent.com/46469458/190923279-9eef58a5-c29c-430a-85f2-369591d634c1.png">
<img width="1172" alt="image" src="https://user-images.githubusercontent.com/46469458/190923312-9f500c71-b900-474a-8f3c-bd6a191b71aa.png">

16. This is clear email

![image](https://user-images.githubusercontent.com/46469458/190924204-e523281d-13e7-4082-8cae-494a7025f2da.png)
<img width="1161" alt="image" src="https://user-images.githubusercontent.com/46469458/190924180-c5132dc9-2820-48ef-9444-3bcdd33dd5bc.png">
<img width="1160" alt="image" src="https://user-images.githubusercontent.com/46469458/190924235-dde6b65f-81d5-4112-bf9e-b3bc9d9e92ea.png">

17. At Alert page you will see alert dashboard

<img width="1474" alt="image" src="https://user-images.githubusercontent.com/46469458/190923378-ab8ab7f0-d243-4216-a829-a60885fb3691.png">

18. Go to Health check and click enable and fill which path you want to check health

<img width="1071" alt="image" src="https://user-images.githubusercontent.com/46469458/190924055-0f1d21c6-86e9-45be-a73d-ef6bef96b0b0.png">
