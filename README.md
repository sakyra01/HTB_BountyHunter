# HTB_BountyHunter
Hello everyone, here we will consider the solution of the BountyHunter machine, which can be found on the special platform Hack The Box.
Well, below is a description of the machine itself and its specific parameters, including the ip-address. 
![изображение](https://user-images.githubusercontent.com/57565730/138012255-c305ebdc-bb0d-4ccf-ad18-0710aa668851.png)
# Machine solution
1. First you need to go to the site itself and study it carefully. We have a rather primitive service that can provide information about vulnerabilities. 
But the trouble is, the service does not work correctly, or rather, the functionality of providing data on vulnerabilities does not work.
![Screenshot from 2021-10-19 18-29-33](https://user-images.githubusercontent.com/57565730/138013017-aed1f55c-fe01-42d7-a7f0-4c5265a934fc.png)
AND BUG Service 
![Screenshot from 2021-10-19 18-30-23](https://user-images.githubusercontent.com/57565730/138013063-98d6236f-b6f4-48c9-bcd4-716d8e61c86c.png)
2. Well, now you need to do some exploration and see what this site is fraught with. 
  > - To begin with, you can use the nmap tool, you need to find out which ports are open (look outside) and analyze the overall picture of the service structure
   ```console
   ~$ nmap -Pn -A 10.10.11.100
   ``` 
  ![Screenshot from 2021-10-19 18-41-06](https://user-images.githubusercontent.com/57565730/138013851-0f1808e4-d197-45e5-8241-60f550b624db.png)
