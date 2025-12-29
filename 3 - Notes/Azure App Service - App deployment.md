Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[__Web_Development]]

# Deploying using App Service
- Tutorial about that: [https://www.youtube.com/watch?v=FOTTt-qTv9o&list=PLLasX02E8BPADO_R-D6ctSoV4EeE8ow9B&index=7](https://www.youtube.com/watch?v=FOTTt-qTv9o&list=PLLasX02E8BPADO_R-D6ctSoV4EeE8ow9B&index=7) 
- If deployment fails it might be worth to try again in some time or try lower version of Azure Resources extension in VS code (version v0.8.0)
- I can check web app files in VS code:
  ![[2 - Images/Azure app service deployment/Screenshot 1.png]]

- I can view files and use server consol in Kudu. I can access it in the Development Tools > Advanced Tools section:
  ![[2 - Images/Azure app service deployment/Screenshot 2.png]]
  
  ![[2 - Images/Azure app service deployment/Screenshot 3.png]]
  
  In order to use SSH console I need to set up the ‘Always on’ setting to ‘On’:
  
  ![[2 - Images/Azure app service deployment/Screenshot 4.png]]
- I can check logs in the ‘Diagnose and solve problems’ section of App Service:
  ![[2 - Images/Azure app service deployment/Screenshot 5.png]]
  
  in the Monitoring > Logs section (there is a tab called ‘Queries’ with different useful queries for checking logs):
  ![[2 - Images/Azure app service deployment/Screenshot 6.png]]
  
  And in the Log Stream section:
  ![[2 - Images/Azure app service deployment/Screenshot 7.png]]
