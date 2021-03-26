# baby bonechewercon
We are given an archive with a docker image for the challenge. It is a Twig application that is vulnerable to Server-Side Template Injection. It allows us to execute any code on the server and get the flag. 

![](pictures/2021-03-26-22-12-48.png)
 
After submitting `{{['cat /flag']|filter('system')}} ` as the name we get the flag.
 
![](pictures/2021-03-26-22-12-55.png)