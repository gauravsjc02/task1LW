<h2>OBJECTIVE:</h2>
Setup up an infrastructure such as there are three teams/environemnts :

1. Production
2. Testing
3. Quality Assurance
Production Team will deploy the code first, now there is some work going on in the developement team which is to be deployed on testing environment which will be sent to the production only when the QA team approves it.

<h2>REQUIREMENTS:</h2>
<ol>
<li>Knowledge of docker</li>
<li>Concepts of creating jobs on Jenkins</li>
<li>Networking</li>
</ol>

<h2>MY PROJECT:</h2>
First the developer sends its code, Quality Assurance teams checks it.
![Before](https://raw.githubusercontent.com/yashbajpai98/task1LW/master/task1-images/master-before.PNG)
I had a combination of 4 jobs as described:
<h3>JOB 1</h3>
As soon as a master developer put his code on github. A job1 is called which downloads all his codes from "master branch" and deploy on a apache web server already built in httpd image.
![alt img="job1"](https://raw.githubusercontent.com/yashbajpai98/task1LW/master/task1-images/job1.PNG)
<ul>
  <li> -p 8081:80 This exposes the port no. 8081 of particular image as to access through outside world. </li>
  <li> -v /root/taskmaster: This shows that an outside volume is attached to destination folder of particular container.
</ul>
Whenever any new commit occurs in master branch, it downloads the code and deploy in this container image.

<h3>JOB 2</h3>
As soon as a developer put his code on github. A job2 is called, which downloads all his codes from "dev1 branch" and deploy on a apache web server already built in httpd image.
![alt img="job2"](https://raw.githubusercontent.com/yashbajpai98/task1LW/master/task1-images/job1.PNG)
<ul>
  <li> -p 8082:80 This exposes the port no. 8082 of particular image as to access through outside world. </li>
  <li> -v /root/taskdev: This shows that an outside volume is attached to destination folder of particular container.
</ul>
Whenever any new commit occurs in dev1 branch, it downloads the code and deploy in this container image. And testing is done on this server only. Only if this code is properly working then only it will be deployed on master server.

<h3>JOB 3</h3>
This job checks that wheather the code deployed by dev1 is working or not. It only checks the "STATUS" of the server.
![alt img="job1"](https://raw.githubusercontent.com/yashbajpai98/task1LW/master/task1-images/job1.PNG)
<ul>
  <li> STATUS returns code 200 if it is working fine. </li>
  <li> STATUS returns code other than 200 if it is not working fine. </li>
 </ul>
Only when the status code is 200 then only it calls JOB 4.

<h3>JOB 4</h3>
This is a downstream job called by Job 3. This job merges the dev1 branch to master developer. And further calls Job 1.
![alt img="job1"](https://raw.githubusercontent.com/yashbajpai98/task1LW/master/task1-images/job1.PNG)
<ul>
  <li> Merges the dev1 branch to master.</li>
  <li> Calls Job 1 after it is build.</li>
 </ul>
 
 


