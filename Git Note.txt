* Structure
git master
	develop
		AHT1
		AHT2

[Merge/Rebase]
git checkout -b AHT1 (create 'AHT1', change from 'master' -> 'AHT1')
/* add some modified code here */
git checkout branch_higher_level 
git merge AHT1 ( this is branch_2)
git push origin branch_wanna_push

[AHT1]
Code 
-> git status 
-> git add . 
-> git commit - m '' 
-> git pull origin develop (avoid conflict)
-> git push origin AHT1
