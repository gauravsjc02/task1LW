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
I had a combination of 4 jobs as described:
<h3>JOB 1</h3>
As soon as a developer put his code on github. A job1 is called which downloads all his codes from "master branch" and deploy on a apache web server already built in httpd image.

<ul>
  <li> -p 8081:80 This exposes the port no. 8081 of particular image as to access through outside world. </li>
  <li> -v /root/taskmaster: This shows that an outside volume is attached to destination folder of particular container.
</ul>
