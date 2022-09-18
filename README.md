# App-Service-troubleshooting
1. Go to [Azure_Portal](https://azure.microsoft.com/en-us/get-started/azure-portal/) then search `app service` and select `app service`

<img width="964" alt="image" src="https://user-images.githubusercontent.com/46469458/190918854-eab6613c-8d30-4121-95d9-dabe4822564e.png">

2. Select your app service 

<img width="1019" alt="image" src="https://user-images.githubusercontent.com/46469458/190918935-43941919-facc-4791-a2d5-63aad9fbf000.png">

3. At Overview page click on URL to see your web can or cannot access (**this workshop it cannot access**)

<img width="1478" alt="image" src="https://user-images.githubusercontent.com/46469458/190919061-84f3538e-ebda-41c5-ac87-41aa970f39ae.png">

4. Scroll down to Monitoring session and click log stream to see live log

<img width="1471" alt="image" src="https://user-images.githubusercontent.com/46469458/190919233-57f36777-7f97-49c1-b1ca-4bdfa09fbcba.png">

5. Go to Monitoring session and click Logs and close Queries pop up

<img width="1451" alt="image" src="https://user-images.githubusercontent.com/46469458/190919375-9324c61a-4835-4c6f-8a7a-6bfd5a0d8640.png">

6. At query tool paste this query command `AppServicePlatformLogs | where Level == "Error"` and click run 

<img width="808" alt="image" src="https://user-images.githubusercontent.com/46469458/190919512-8ed3189f-40b4-4a4f-96cf-946ed4fec11e.png">

7. Click Display time (UTC+00:00) and change to Local time

<img width="908" alt="image" src="https://user-images.githubusercontent.com/46469458/190919609-23dcbbc8-4276-48f9-8325-88543abb2f5d.png">

8. 
