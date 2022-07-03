<div align="center">

<img src="https://i.imgur.com/BkKtAkO.png">

</div>

# <b>Pickle Rick</b>

Simple room. In general - use directory traversal + reverse shell for the third flag

<br/><br/>

## <b>Step 1 - Initial overview</b>
<br/>

<img src="./assets/Overview0.jpg">

<br/>

Since nothing interesting(fields and so on) - check the source code, console , scripts | styles comments and other sources we have on this stage. Lucky for you, we can find something interesting immidiately in index sources

<br/>

<img src="./assets/Source0.jpg">

Store it - it might be an SSH / FTP username or this site's login


<br/>

## <b>Step 2 - Port scan + Dirbusting</b>


<br/>
Then I've tried to scan the machine with <b>nmap</b> but in general - nothing interesting excluding potential SMB or some differences with content on 80 port

<br/>

<img src="./assets/nmap.jpg">

<br/>
After this "micro-fail" let's try to find interesting locations via <b>dirsearch</b>

<br/>

...and we have the following results

<img src="./assets/dirsearch.jpg">

<br/>

## <b>Step 3 - Find creds & places to use them</b>

Go to <b>/robots.txt</b> and see

<img src="./assets/robots.jpg">

That's can be the "second part" for some credentials pair. We already have username, now something which looks like password. Now go to /login.php and try to use this pair.

<img src="./assets/control.jpg">

<h1 align="center"><b>Awesome,move on</b></h1>

Try default shell commands to get the role, location and so on.After some attempts you'll notice some commands are blacklisted(you'll have an empty output). Ok,let's list the current directory

<img src="./assets/ls.jpg">

To get the content of files I've used bypass via GTFOBINS(popular bins which are usually on each machine by default). Follow link and choose <b>File read</b> option

<img src="./assets/gtfobins.jpg">

<br/>

After some attempts I've found that we can read files via <b>git</b>. Use this pattern


<b></b>