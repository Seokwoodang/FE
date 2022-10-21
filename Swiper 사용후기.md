페이지를 작성하며 마우스 스크롤에 따라 한 페이지씩 자연스럽게 auto focus 가 되는 기능을 구현해야 했다. 

직접 auto focus 를 구현해본 결과 자연스럽지도 않고 마우스 스크롤에 따라 정확하게 한번씩만 내려가는 기능도 구현하기가 어려웠다.

빠른 제작과 정확하고 효과적인 auto focus를 위해 Swiper 라이브러리를 사용하게 되었다.


```
import { Swiper, SwiperSlide } from 'swiper/react';

import { Keyboard, Mousewheel, Navigation, Pagination } from 'swiper';

  const pagination = {
    clickable: true,
    renderBullet: function (index, className) {
      if(index === 1 || index === 5){
        return '<A></A>'
      }
      else if( index === 0){
        return '<div class="' + className + '">홈</div>'
      }
      else if( index === 2){
        return '<div class="' + className + '">서비스</div>'
      }
      else if( index === 3){
        return '<div class="' + className + '">기술</div>'
      }
      else if( index === 4){
        return '<div class="' + className + '">이용방법</div>'
      }
      else if( index === 6){
        return '<div class="' + className + '">문의하기</d>'
      }
      else{
      return '<span class="' + className + '">' + (index + 1) + "</span>";
      }
    },
  };
  
  return (
  
    <Swiper    
      direction={"vertical"}
      slidesPerView={1} // 한번의 뷰에 몇개의 슬라이드를 보여줄건지
      spaceBetween={0} 
      mousewheel={true} // 마우스 휠 반응 사용할거야?
      navigation={false}
      modules={[Mousewheel, Pagination,Keyboard, Navigation]}
      speed={800} // 페이지 이동 속도
      simulateTouch={false} 
      keyboard={{ enabled: true }} // 키보드 반응 사용할거야?
      pagination={pagination} // 페이지네이션을 사용하기 위에 return 위의 함수를 작성하였다. 
      // breakpoints={{8000:{mousewheel:false}}} 가로 사이즈에 의해 브레이크 포인트 안의 요소 변경
    >
      <SwiperSlide><Home1 onClickModal={onClickModal} /></SwiperSlide>
      <SwiperSlide><Home2 /></SwiperSlide>
      <SwiperSlide><Home3 /></SwiperSlide>
      <SwiperSlide><Home4 /></SwiperSlide>
      <SwiperSlide><Home5 /></SwiperSlide>
      <SwiperSlide><Home6 /></SwiperSlide>
      <SwiperSlide><Home7 /></SwiperSlide>
      <StFooter src={footer} />
    </Swiper>
    )
  }
```

Swiper 태그로 컴포넌트를 감싸준 뒤 각각의 컴포넌트를 SwiperSlide로 감싸주었다.

스와이퍼 라이브러리 자체적으로 지원해주는 특성들이 많았고 그 안에 마우스 휠과 페이지네이션 네비게이션 키보드 기능을 

사용하게 되었다.

위의 태그에 대한 자세한 설명은 여기에 적는 것보다 공식문서를 직접 보는 것이 더 나으므로

https://swiperjs.com/react

이 안에 들어가서 보는 것이 더 낫다.

이틀정도 라이브러리를 수정하고 내부적으로 커스텀한 결과 디자이너님께서 기획하신 것과 거의 같은 페이지를 만들 수 있었다.

하지만 결국 이렇게 만든 기능은 사라지게 되는데 이는 

다른 페이지의 헤더에서 네비게이션바를 누를경우 다시 이전 페이지로 돌아와 그 부분을 보여주지 못하기 때문이었다. 

자세히 말하자면 1페이지에서 헤더의 네비게이션 버튼을 누를 경우 버튼에 해당하는 부분으로 스크롤이 자동으로 내려가 그 컴포넌트를 보여주었다.

하지만 라이브러리의 특성상 스와이퍼의 기능을 사용하기 위해서는 <Swiper>태그를 감싸주어야 하는데 다른 페이지는 태그로 감싸줄 수 가 없었기에
  
2페이지의 헤더에서 네비게이션 버튼을 누를 경우 ( 사실 애초에 다른페이지에서는 스와이퍼 autofocus 기능이 들어간 네비게이션 버튼을 만들 수도 없다. )

아무일도 일어나지 않게 되는 것이다. 
  
따라서 autofocus부분을 없던일로 처리하게 되었고 이번 프로젝트에서 내가 몇일간 공부해서 만든 Swiper파트는 사라지게 되었다...
  
하지만 다른 프로젝트에서 사용하게 된다면 훨씬 더 빠르게 만들 수 있겠지!  
  
뀨

