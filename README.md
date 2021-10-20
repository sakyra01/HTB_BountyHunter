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
   > To begin with, you can use the nmap tool, you need to find out which ports are open (look outside) and analyze the overall picture of the service structure
   ```console
   ~$ nmap -Pn -A 10.10.11.100
   ``` 
  ![Screenshot from 2021-10-19 18-41-06](https://user-images.githubusercontent.com/57565730/138013851-0f1808e4-d197-45e5-8241-60f550b624db.png)
  
The fact that ports 22 and 80 are open is good news, as an option for the future it is possible to brute force port 22 of ssh, but this is a bad idea. 
I think it's better to find ssh credentials information somewhere...
  > Now I want to look diffrent possible paths which include this service
  > And I'm going to use dirsearch tool, which you can easily find on github
   ```console
   ~$ ./dirsearch.py -u 10.10.11.100
   ``` 
   
   That's what i get btw:
   
  ![Screenshot from 2021-10-19 18-52-09](https://user-images.githubusercontent.com/57565730/138014769-d9fa18cb-aa45-4897-9e61-f7975debe988.png)

  > There are a couple of interesting local files here, db.php is empty, but we find something interesting in the README ...
  
  ![Screenshot from 2021-10-19 18-56-46](https://user-images.githubusercontent.com/57565730/138015184-f8a02acf-628d-4360-ac09-730e76ea0189.png)
  
3. We have collected some information for a more successful injection on the server. Well, what interested me the most was the submit.php path. 
   I decided to use Burp Suite to intercept and modify server requests. How example i tried look on this page:
 
 > I gues we can find here xml
 
 ![Screenshot from 2021-10-21 00-19-01](https://user-images.githubusercontent.com/57565730/138175483-1fe3628b-e6eb-4443-a7eb-e966396e0a46.png)

  Next step is to research Bounty Report System:
  
  > I push POST request on the server and get this Responce

![Screenshot from 2021-10-21 00-25-42](https://user-images.githubusercontent.com/57565730/138175861-25cf5382-2e4b-4139-bbc7-91eab34a4518.png)

  Data is base64 encoded xml, the next step I am convinced of this

![изображение](https://user-images.githubusercontent.com/57565730/138176625-394fd5cc-ad94-45ed-974d-51ce5be4ec94.png)

4. Now we need to figure out how to exploit the xxe vulnerability associated with the injection of additional parameters into the xml, which the server will then return to us.

   For more information about XXE look here:
    
    1. https://cisoclub.ru/rukovodstvo-po-xxe-injection/ - XXE Injection Guide
    2. https://gist.github.com/staaldraad/01415b990939494879b4) - XXE_payloads


 
 
