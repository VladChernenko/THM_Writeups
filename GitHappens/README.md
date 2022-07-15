# TryHackMe - GitHappens

<div align="center">

<img src="https://assets.tryhackme.com/img/banners/default_tryhackme.png">

</div>

<p><b>Level</b>:EASY</p>

<p><b>Link</b>:<a href="https://tryhackme.com/room/githappens">https://tryhackme.com/room/githappens</a></p>

<br/><br/><br/>

## Part 1 - Clone repository

Do it recursively via <code>wget</code>

```shell

wget -r http://10.10.97.46/.git/

```

<img src="./0.jpg">

<br/><br/>

## Part 2 - Go to right commit

This one looks interesting

<img src="./1.jpg">

<p>Go to <code>index.html</code></p>

<img src="./2.jpg">
<img src="./3.jpg">

<p>Check the source code</p>

<img src="./flag.jpg">