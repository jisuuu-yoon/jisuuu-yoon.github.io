---
title: summary_git 
date: "2019-11-09T21:57:57.121Z"
template: "post"
draft: false
slug: "/posts/eventBubbling/"
category: "Development"
tags:
  - "onClick"
  - "event bubbling"
description: " "
---
# event Bubbling 정리하기

**event bubbling이란?** : 이벤트가 발생하는 가장 안쪽부터 바깥쪽, 하위 노드에서 상위 노드로 이벤트 전파되는 과정이다.
하위 DOM Element부터 전파되는 이벤트는 최종적으로 document 객체까지 전달되며, 상위 Element에서 이벤트 핸들러를 재정의해서 전파를 제어할 수 있다.

- 하위 DOM Element부터 전파되는 이벤트는 최종적으로 document 객체까지 전달되며, 상위 Element에서 이벤트 핸들러를 재정의해서 전파를 제어할 수 있다.

    

**event capturing이란?** : 이벤트 캡쳐링은 이벤트 버블링의 반대방향으로 이벤트가 전달된다.

- Parent노드부터 이벤트가 전달되는 것으로, 즉 상위노드부터 하위노드로 이벤트가 전달되는 형태.


- 내가 겪었던 문제를 설명하자면,
세개의 li태그로 이뤄진 tab이 있고 그안에는 각각의 tab이름과 <span>으로 감싸진 숫자가 있을때,
각각의 탭을 눌렀을 때 onClick으로 해당 tab부분만 css를 변경해주고 싶었다. 
그래서, 아래와 같이 id값으로 받아오게 했는데, tab의 이름부분을 눌렀을때는 이벤트가 실행되는데, 다른부분 즉 <span>태그부분을 누르면 
해당이벤트가 실행되지 않았다. 내 상식으로는 당연히 tab의 li태그안에 span태그가 있기때문에 span부분을 눌러도 그 부모인
li태그의 이벤트가 실행될것이라고 생각했기 때문이다. 
~~~
<div className='menuContainer'>
                    <div className='menuTab'>
                        <ul className='menuTab__ul'>
                            <li 
                            idname="menuTab"
                            className={"menuTab__ul__li "+ (this.props.menuTabs.menuTab? "buttonColorRed" : "")} 
                            onClick={this.props.passEvent(e)}
                            > 메뉴 </li>
                            <li 
                            idname="reviewTab"
                            className={"menuTab__ul__li "+ (this.props.menuTabs.reviewTab? "buttonColorRed" : "")} 
                            onClick={()=>{this.props.passEvent(e)}
                            >클린리뷰<span>{this.props.reviewNum}</span></li>
                            <li 
                            idname="infoTab"
                            className={"menuTab__ul__li "+ (this.props.menuTabs.infoTab? "buttonColorRed" : "")} 
                            onClick={()=>{this.props.passEvent(e)}
                            >정보</li>
                        </ul>
                    </div>
</div>                    
~~~

~~~
handleClick=(e)=>{
        console.log(this.state)
        if(e.target.id==="ownerMsg"){
            //console.log("clicked")
            let updatedMenuTabs = {...this.state.infoTab} //copy &paste
            updatedMenuTabs["menuTab"] = false
            updatedMenuTabs["reviewTab"] = false
            updatedMenuTabs["infoTab"] = true
            this.setState({menuTabs : updatedMenuTabs});
            
        }
        if(e.target.id==="menuTab"){
            let updatedMenuTabs = {...this.state.menuTabs}
            updatedMenuTabs["menuTab"] = true
            updatedMenuTabs["reviewTab"] = false
            updatedMenuTabs["infoTab"] = false
            
            this.setState({menuTabs : updatedMenuTabs});
        
        }
        if(e.target.id==="reviewTab"){
            let updatedMenuTabs = {...this.state.reviewTab}
            updatedMenuTabs["menuTab"] = false
            updatedMenuTabs["reviewTab"] = true
            updatedMenuTabs["infoTab"] = false

            this.setState({menuTabs : updatedMenuTabs});
            
        }
        if(e.target.id==="infoTab"){
            let updatedMenuTabs = {...this.state.infoTab}
            updatedMenuTabs["menuTab"] = false
            updatedMenuTabs["reviewTab"] = false
            updatedMenuTabs["infoTab"] = true

            this.setState({menuTabs : updatedMenuTabs});
            
        }
    }
    
~~~



- 위의 코드를 보면 각각의 tab에 id를 주고 event를 전달시킨다. 그리고 그 이벤트를 받아서 e.target.id로 어떤부분이 클릭이 됐는지 파악하려했었다.
- 하지만 이렇게되면 event bubbling 으로 인해 해당 id값을 가지고 있는 li태그만 클릭되는게 당연했다. 
- 그래서 코드를 아래와 같이 변경시켰다.


 >해당 ResetModal 컴포넌트의 코드는
 
 ~~~
 <div className='menuContainer'>
                     <div className='menuTab'>
                         <ul className='menuTab__ul'>
                             <li 
                             className={"menuTab__ul__li "+ (this.props.menuTabs.menuTab? "buttonColorRed" : "")} 
                             onClick={()=>{this.props.passEvent("menuTab")}}
                             > 메뉴 </li>
                             <li 
                             className={"menuTab__ul__li "+ (this.props.menuTabs.reviewTab? "buttonColorRed" : "")} 
                             onClick={()=>{this.props.passEvent("reviewTab")}}
                             >클린리뷰<span>{this.props.reviewNum}</span></li>
                             <li 
                             className={"menuTab__ul__li "+ (this.props.menuTabs.infoTab? "buttonColorRed" : "")} 
                             onClick={()=>{this.props.passEvent("infoTab")}}
                             >정보</li>
                         </ul>
                     </div>
 </div>                   
 ~~~
 
 ~~~
 handleClick=(tab)=>{
         console.log(this.state)
         if(tab==="ownerMsg"){
             //console.log("clicked")
             let updatedMenuTabs = {...this.state.infoTab} //copy &paste
             updatedMenuTabs["menuTab"] = false
             updatedMenuTabs["reviewTab"] = false
             updatedMenuTabs["infoTab"] = true
             this.setState({menuTabs : updatedMenuTabs});
             
         }
         if(tab==="menuTab"){
             let updatedMenuTabs = {...this.state.menuTabs}
             updatedMenuTabs["menuTab"] = true
             updatedMenuTabs["reviewTab"] = false
             updatedMenuTabs["infoTab"] = false
             
             this.setState({menuTabs : updatedMenuTabs});
         
         }
         if(tab==="reviewTab"){
             let updatedMenuTabs = {...this.state.reviewTab}
             updatedMenuTabs["menuTab"] = false
             updatedMenuTabs["reviewTab"] = true
             updatedMenuTabs["infoTab"] = false
 
             this.setState({menuTabs : updatedMenuTabs});
             
         }
         if(tab==="infoTab"){
             let updatedMenuTabs = {...this.state.infoTab}
             updatedMenuTabs["menuTab"] = false
             updatedMenuTabs["reviewTab"] = false
             updatedMenuTabs["infoTab"] = true
 
             this.setState({menuTabs : updatedMenuTabs});
         }
     }
 ~~~
 
 - 해당 탭에서 onclick으로 보낼때, arrow function을 이용해 해당 tab의 이름만을 보내주고
 그 탭의 이름만들 받아서 비교했더니 그 해당 탭전체 어느곳을 눌러도 css가 바뀌게끔 할 수있었다.
 ------------------------------------------------------