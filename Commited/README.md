# TryHackMe - Committed

<div align="center">

<img src="https://assets.tryhackme.com/img/banners/default_tryhackme.png">

</div>

<p><b>Level</b>:EASY</p>

<p><b>Link</b>:<a href="https://tryhackme.com/room/committed">https://tryhackme.com/room/committed</a></p>

<br/><br/><br/>


## Part 1 - My inattention

Start machine and press "Split Terminal" to avoid my mistakes and time spend 

<img src="./split.jpg">

## Part 2 - Overview

Unzip repository

<img src="./unzip.jpg"></br>

Let's check available branches & commits

<img src="./overview0.jpg"></br>
<img src="./branch.jpg"></br>


<div align="center">

### So the task is to go through the history and check the content to find the flag 

</div></br>

## Part 3 - Recon

Go through the commits and check <code>main.py</code> file to get the flag

<img src="./walk.jpg"></br>
<img src="./still_master.jpg"></br>

## Part 4 - New branch

Then I've moved to <code>dbint</code> branch

<img src="./newbranch.jpg"></br>

Here on commit <code>3a8cc16</code> you'll find a version with hardcoded flag

<img src="./true.jpg"></br>

Finally,get the flag

<img src="./flag.jpg"></br>