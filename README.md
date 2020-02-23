# OverTheWire - WriteUps

1) [Bandit](Bandit) : https://overthewire.org/wargames/bandit/
  - The Bandit wargame is aimed at absolute beginners. It will teach the basics needed to be able to play other wargames. 
  This game, like most other games, is organised in levels. You start at Level 0 and try to “beat” or “finish” it. Finishing a level results in information on how to start the next level. The pages on this website for “Level <X>” contain information on how to start level X from the previous level. E.g. The page for Level 1 has information on how to gain access from Level 0 to Level 1. All levels in this game have a page on this website, and they are all linked to from the sidemenu on the left of this page.

2) [Natas](Natas) : https://overthewire.org/wargames/natas/  
  - Natas teaches the basics of serverside web-security.
    Each level of natas consists of its own website located at http://natasX.natas.labs.overthewire.org, where X is the level       number. There is no SSH login. To access a level, enter the username for that level (e.g. natas0 for level 0) and its   password. Each level has access to the password of the next level. Your job is to somehow obtain that next password and level up. All passwords are also stored in /etc/natas_webpass/. E.g. the password for natas5 is stored in the file /etc/natas_webpass/natas5 and only readable by natas4 and natas5.
