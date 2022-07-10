<div align="center">

<img src="https://i.imgur.com/LPggi78.png">

</div>


# <b>Overpass</b>

Level - easy

<br/><br/>

## <b>Step 1 - Initial overview</b>
<br/>

<img src="./assets/nmap.jpg">

Go to web server coz no sense to brute SSH(no clue about passwords & private keys or any other hints)

<br/>

Here is simple site. Small number of any external links, directories, nothing in source code or console

<img src="./assets/init2.jpg">
<br/>
<img src="./assets/init3.jpg">

<br/><br/>

## <b>Step 2 - Dirbusting</b>
<br/>


Let's try to find directories

<img src="./assets/dirb.jpg">


For this time - only <b>/admin</b> is interesting. Let's check

<br/><br/>

## <b>Step 3 - Research</b>
<br/>
<img src="./assets/admin.jpg">

Let's discover the source code. Here we can notice <b>login.js</b> script which looks interesting because gives us informarion about auth logic.

<br/>
<img src="./assets/res1.jpg">
<br/>
Here we can see that the function save the cookie <b>SessionToken</b> if login was success. But hint said us about OWASP, so let's to exploit it via manual cookie change using dev console
<br/>
<img src="./assets/res2.jpg">

<br/>
We don't know the value,so use HelloWorld. Then,make a reload
</br>

<img src="./assets/auth.jpg">


## BOOOM we have someone's RSA encrypted private key for SSH

Name hints us that it's user <code>james</code>
<br/>

<img src="./assets/ssh.jpg">

<br/><br/>

## <b>Step 4 - What next?</b>

Honestly, I've stuck here for a while, because hint said us "not to brute", so I've no clue where to find the other hints. I've decided to run <code>John The Ripper</code> and continue to find something more.

After a few seconds I've received password...😅

<img src="./assets/brute1.jpg">
<img src="./assets/brute2.jpg">

<br/><br/>

## <b>Step 4 - On machine</b>

Firstly connect and grab <code>user.txt</code>

<img src="./assets/connect1.jpg">


<br/><br/>

## <b>Step 5 - PrivEsc</b>

Before we start, I've initially downloaded <code>overpass.go</code> to check the source code. Here is simply ROT47, so we can easily encrypt the ciphertext

<br/>

<img src="./assets/over0.jpg">
<img src="./assets/over1.jpg">
<img src="./assets/over2.jpg">

<br/>

The only interesting file here is ~/.overpass with ciphertext of our passwords

Come back to our terminal with SSH session and find this file locally

<img src="./assets/pass0.jpg"></br>
<img src="./assets/pass1.jpg">
<img src="./assets/pass2.jpg">

<br/>
Make sure it's james' password by test on <code>sudo</code>
<br/>

<img src="./assets/pass3.jpg">

<br/><br/>
I've notice that we have access to <code>nano</code>, so let's use <b>LinEnum</b> bash script to get quick enumeration

<img src="./assets/linenum.jpg">

Among tons of useless data, found interesting point for crontab. Some bash script taken from <b>overpass.thm</b> will be runned as root.


<img src="./assets/cron.jpg">


<b>overpass.thm</b> doesn't look like real domain, so let's try to modify <code>/etc/hosts</code> and add our VPN's interface for this domain. Run a python oneliner for test

<img src="./assets/test.jpg">

<br/><br/>

<div align="center">

## Yeah, we have a query, so let's put a reverse shell here

</div>
<br/>
<img src="./assets/revshell.jpg">

Run a listener

<img src="./assets/last.jpg">


And after a few seconds we have a shell

<img src="./assets/root.jpg">