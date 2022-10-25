네비게이션 바를 구현하는데 있어 ref 값을 사용한 scrollIntoView 를 사용하였다.

페이지 상단의 네비게이션 바를 클릭할 경우 원하는 위치의 컴포넌트까지 오게 되고 속성값에 따라 (시작,끝,중간) 에 따라 화면에 배치되는 컴포넌트의 위치를 정할 수 있다.

기획에 따르면 Landing Page의 헤더 뿐만 아니라 다른 페이지의 네비게이션 바를 이용해서도 Landing page로 이동 후 그 컴포넌트의 위치를 보여주어야 했기에 상당히 많은 고민을 했다.

또한 현재 페이지가 Landing Page 인지 아닌지에 따라 컴포넌트로 이동하는 방식도 smooth 인지 바로 보여주는 형식인지 또한 달랐기에 분기를 쳐주어야 했다.

우선 네비게이션 기능을 모든 페이지에서 구현하기 위해 헤더를 최상단 컴포넌트로 바꾸는 수 밖에 없었다.

App.js 의 Routes 밖으로 빼내어 모든 페이지에 적용 될 수 있도록 구현하였고 state 값을 선언해 주었다.

state 안에는 현재 페이지가 랜딩페이지인지를 따져주는 boolean 값과 보여줄 컴포넌트의 ref 값을 저장해주었다.

ref 값의 경우 컴포넌트에 바로 주는 것이 아니라 컴포넌트에 props로 내려준 뒤 그 안에서 ref 지정을 해주어야 오류가 나지 않는다.

이제 state값의 정보를 읽어 경우의 수를 따져주고 작동을 시키면 완성이다.

```
  useEffect(()=>{
    if(nav[0] === 1){
      if(nav[1] === true){
        top.current.scrollIntoView({block : 'end', behavior:'smooth'});
      }
      else{
        top.current.scrollIntoView({block : 'end'});
      }
    }
    else if(nav[0] === 3){
      if(nav[1] === true){
        service.current.scrollIntoView({block : 'end', behavior:'smooth'});
      }
      else{
        service.current.scrollIntoView({block : 'end'});
      }
    }
    else if(nav[0] === 4){
      if(nav[1] === true){
        technic.current.scrollIntoView({block : 'center', behavior:'smooth'});
      }
      else{
        technic.current.scrollIntoView({block : 'center'});
      }
    }
    else if(nav[0] === 5){
      if(nav[1] === true){
        how.current.scrollIntoView({block : 'center', behavior:'smooth'});
      }
      else{
        how.current.scrollIntoView({block : 'center'});
      }
    }
    else if(nav[0] === 7){
      if(nav[1] === true){
        qna.current.scrollIntoView({block : 'center', behavior:'smooth'});
      }
      else{
        qna.current.scrollIntoView({block : 'center'});
      }
    }
  },[nav,setNav])
```
