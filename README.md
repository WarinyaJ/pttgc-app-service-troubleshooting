# App-Service-troubleshooting
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

17. 
