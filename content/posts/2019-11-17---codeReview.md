---
    title: code review
date: "2019-11-17T12:17:27.121Z"
template: "post"
draft: false
slug: "/posts/codeReview/"
category: "Development"
tags:
    - "coding"
    - "code review"
description: " "
---
    # code review 정리하기 
 1. 폴더를 만들때 통일하기- 예) 대문자/소문자 폴더규칙
 파일이름 -> 클래스로 만드는 component만 capital로 시작
 2. style폴더를 만들어서 reset.scss (공통으로 넣어야하는 코드)
 normalize.scss (정확히 구분하기 어렵지만 모든 브라우저에서 똑같이보여지게 맞춰주는것) common.scss(button이나 글씨체, 폰트컬러 등 자주 공통으로 쓰이는것) 각각 하나씩 
 3.프로젝트 진행할 수록 관리해야할 키들이 많아진다.
 -> 매번 쓸때마다 각각 넣어주기 보다는
 config.js 에
 
 키나 토큰 등 한파일에서 관리하고 import만 해줄것
 고정값은 항상 상수처리하는 습관을 들이기 (const)
 
 4.약속한대로 절대경로를 쓰기로
 상대경로가 없는 경우에는 가장먼저찾는게 node_modules 먼저 찾는데, 
 거기를 매번 바라보기때문에 config.js는 항상 .js를 붙여줄것
 
 5.메인 라우트 하나만 만들고 
 그 컴포넌트가 constructor 만들어서 로그인을 했는지 안했는지 관리해서
 렌더에서 삼항연산자를 사용해서 ->로그인 전후 컴포넌트 리턴해주기
 
 
 6. components 는 어떤 페이지든 상관없이 두번 이상 쓰일만한것을 모아둬야함
 
 7. state관리시 굳이  constructor()안에 관리하지 않아도 된다.
 constructor 안에 쓰는경우는 -> props를 받아와서 state를 관리할경우 
 constructor(props) 사용
 
 state={
 	a: ture
 	}
 이외에는 위와같은 방식으로---
 
 
 
 8. 윈도우에 등록한 이벤트-> component가 끝날때 반드시 clear or remove하는 unmount 함수를 이용해 지워야함
 
 const {data.data}= this.state
 const {data:{data}}=this.state => this.state.data.data
 
 
