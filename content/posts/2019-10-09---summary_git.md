---
title: summary_git 
date: "2019-10-09T21:46:37.121Z"
template: "post"
draft: false
slug: "/posts/summary_git/"
category: "Development"
tags:
  - "git"
  - "git push"
description: " "
---
# git 정리하기

**git** : 소스코드 넣는 저장소

- git remote add origin  url주소 
	 > github에 올릴 레파지토리 주소 등록(origin은 무조건 써야하므로 외울것)
	

- git remote -v 
 	 >원격저장소 주소보기

- git status  
	 >현재 저장소의 상태를 확인

- git add filename or directory name
	>원하는 file 또는 directory add
		(해당 프로젝트의 모든 file을 커밋하기 위 해 'add .' 입력)
		(git add를 하기 이전의 파일들은 git이 추적하지 않지만 git add 이후에 git status로 확인시 git이 추적하는 파일과 그렇지 않은 파일을 명확하게 구분 가능)

- git commit -m '제목'
	>add된 file or directory commit

- git log
	>commit이 대한 아이디와 작성자, 날짜. 그 밑에는 commit메세지를 확인 가능

- git push origin master
	 >github에 올릴 file or directory push
	 (master는 default branch임, 사용X)
	 
 -	git branch develop 
      >develop이라는 branch 생성 

- git branch 
	>확인 

- git checkout develop 
	>현재 branch에서 나와서 develop branch로 이동

- yarn deploy 

	or
- npm run deploy -> for release
	>배포하기





