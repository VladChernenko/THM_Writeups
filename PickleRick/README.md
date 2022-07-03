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
After this "micro-fail" let's try to find interesting locations via <b>dirsearch</b>...and we have the following results

<br/>

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

```shell

git diff /dev/null 'FILE-TO-READ'

```

<img src="./assets/git_file_read.jpg">

<br/>

## And we have the first flag

<img src="./assets/flag1.jpg">



<br/>

## <b>Step 4 - Flag2</b>

Let's get some hint from <code>clue.txt</code>

<img src="./assets/hint.jpg">

Ok,let's do this. But not to spend your time, I'll give you a tip: Go to the <b>/home/rick</b>. Here we'll see the following

<img src="./assets/rick_ls.jpg">

## And grab the second file

<img src="./assets/flag2.jpg">



<br/>

## <b>Step 5 - Flag3</b>

You can also use flag <b>-a</b> to get the hidden dirs. For example

<img src="./assets/ubuntu.jpg">

I've tried to read SSH keys, find secrets in .bash* files but nothing. We don't have rights. BTW,later I've noticed that we have so high privilleges(via <code>sudo -l</code>)

<img src="./assets/sudo.jpg">

## <b>Let's use reverse shell</b>

Go to https://www.revshells.com/ and copy a shell for Python3

<img src="./assets/shell.jpg">

Run a listener locally and force connection. Then run <code>sudo bash</code> and you're <b>root</b> !!!. Now find the third flag in home directory
