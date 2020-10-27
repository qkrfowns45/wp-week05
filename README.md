# 5주차 실습 TRASITION, TRANSFORM, ANIMATION

1.과제 설명
 1)기존에 있던 4주차 과제에서 상단 메뉴바를 버튼식으로 사이드로 배치하고 메인 게시판 모습에 애니메이션을 넣어 움직임을 넣었다.
    [1]transition과 css폴더를 사용하여 사이드바 생성
        ->기존에 있던 menu 8개를 바에 숨겨서 클릭하면 나타나게 했다.
        header와 button을 사용하여 상단에 메뉴바를 생성했고 bar를 버튼으로 사용하여 사이드에 hidden으로 숨겨져있던 메뉴들을 불러냈다.
        또한 box-shader를 사용하여 메뉴에 마우스를 가져갔을때 외곽선을 나타나게 했다.(수업때 들은 내용을 적용)

        ->직접 실습하기 위해 메뉴바에 있는 my home page란 글귀에 transition을 응용함
        homepage란 id를 사용하여 글귀를 버튼화 하였다. 글자에 마우스를 가져갔을때 border를 사용하여 외각선을 만들었고 마우스가 클릭하였을때 위치한다는 것을 시각적으로 표시했다.
        또한 transition-duration을 사용하여 3초 동안 글자의 크기가 p의 기본 사이즈에서 font-size를 사용해 large의 크기만큼 커지는 것을 이용해 homepage의 모습을 역동적으로 표현했다.
        (결과적으로 마우스를 가져갔을때 글씨가 커지며 클릭하면 외곽선이 시각적으로 보임)

        ->transform을 살짝 적용하여 바에 마우스를 가져갔을때 90를 돌려 사이드 메뉴를 누를 준비가 된 것을 시각적으로 표현했다.
        Rotate를 사용했고 90도 정도 3초간 돌렸다.

    [2]메인 화면에 보이는 8개의 메뉴들에 입체감을 입혔다.
        ->special이라는 박스를 선언하여 레이아웃하였고 기존 상단에 존재했던 메뉴 8개를 시각으로 볼 수 있게 했었다. 이에 입체감을 더하기 위해 hover를 사용해 역동성을 더했고 transition-duration을 통해 시간을 지정해 자연스러운 느낌을 표현했다.

    [3]소개글 애니메이션 넣기
        ->기존에 있던 welcome to my homepage의 글귀에 애니메이션을 넣고자 css 함수에 ball을 생성함
        
        ->기존 사각틀 안에 모서리를 border-radius로 깍았고 크기도 늘려 정확히 흰색 배경안에 들어갈 크기로 할당하였다. 또한 글귀의 위치도 가운데로 위치하였고 색은 빨강과 파랑을 넣어 배경을 입혔다.
        
        ->시작점은 오른쪽 끝에서 시작하여 화면의 중간까지 왔다가 다시 자리로 회전하면서 돌아가게 구현하였다.
        (keyframe을 사용하였고 transformlotate를 사용해 회전을 넣어 역동적으로 보이게 하였다.)

2.주요 코드 설명

[1] 메뉴 버튼 만들기 코드
  #menu-button {  ->메뉴 버튼을 생성했다.
    width: 40px;
    border: none;
    background-color: transparent;
    padding: 10px;
    cursor: pointer;
    margin-right: 2em;
  }
  
  #menu-button:focus { ->외곽선은 없는 것으로 설정했다.
    outline: none;
  }
  
  #menu-button > .bar { ->바를 만드는데 위, 가운데, 아래를 포함해서 3개의 바를 만들었다.
    width: 100%;
    height: 3px;
    background-color: #333;
    border-radius: 1.5px; ->외곽선은 유해보이게 꼭지점을 깍았다.
    margin: 3px auto;
  }
  #menu-button:hover > .bar{ ->마우스를 가져갔을때 역동적으로 보이기 위해 애니메이션느낌을 추가하여 90도 정도 회전하게 구성했다.
    transform : rotate(90deg);
    transition-duration: 2s; ->2초동안 돌아가게 구성했다.
  }

[2] 사이드 메뉴 만들기 코드
  #side-menu {->사이드 메뉴를 만들어서 메뉴 바에 마우스를 이동시켰을때 나올 사이드 메뉴를 구성하였다.
    position: fixed;
    top: 60px;
    left: 0;
    bottom: 0;
    border-right: 1px solid #ddd;
    background-color: #eee;
    width: 200px;
    padding: 10px 20px;
    box-shadow: 1px 0 2px rgba(0, 0, 0, 0.4);
    transition-duration: 500ms;
}

#side-menu.hidden { ->숨기기 위해 왼쪽에서 100%만큼 뒤로 이동하였다.
  left: -100%;
}

#side-menu > ul > li > a:hover { ->마우스를 가져갔을때 두껍게 표기하기 위해 bold를 사용했다.
    font-weight: bold;
    color: #222;
}

->html 본문에서 스크립트 내부에 선언한 코드이다.(자바 스크립트 코드라서 6주차부터 확실하게 다를 예정이다.)
    let hidden = true; 숨기는 것을 활성화 시킨다.
    const menuButton = document.getElementById('menu-button');
    const sideMenu = document.getElementById('side-menu');
    
    menuButton.addEventListener('click', () => {
        if (hidden) {
        sideMenu.classList.remove('hidden');
        hidden = false;
        } else {
        sideMenu.classList.add('hidden');
        hidden = false;
        }
    });

[3]배너 안에 메뉴 생성하기
->special이라는 박스를 생성해서 배너 안에 들어갈 메뉴 8개에 움직임을 더해 길이가 늘어나게 구성하였다.
.special {
      border: 1px solid #333;
      width: 9%; height: 80%;
      margin: 30px 10px;
      background-color: skyblue;
      transition-duration: 1.5s; ->1.5초동안 동작하게 구성했다.
    }
    .special:hover{ -> 이처럼 생성하여 길이를 90%까지 확장시켰다.
      width: 90%;
    }

[4] 메인 환영글 움직이기
->수업 때 배운 볼을 활용하여 환영을 표하기 위한 움직이는 객체를 생성하였다.
.ball {
  position: absolute;
  width: 610px; height: 500px;
  border-radius: 10%; ->외곽선은 원이 아닌 기존 사각틀에서 10%를 깍았다.
  text-align: center;
  background: linear-gradient(red 0%, blue 100%);

  animation-name: ball; ->애니메이션 이름을 ball로 하였고 3초동안 linear하게 움직이게 구현했다.
  animation-duration: 3s;
  animation-timing-function: linear;
}

.ball > h1 {
  line-height: 500px;
}

@keyframes ball { ->시작은 왼쪽 끝에서 시작하여 50%위치까지 굴러오다가 다시 제자리인 70%까지 움직이게 구현하였다.
  from {
    left: 100%;
    transform: rotate(0deg);
  }
  50% {
    left: 50%;
  }
  to {
    left: 70%;
    transform: rotate(360deg);
  }
}


3.비고 및 고찰
->이번 시간에는 애니메이션을 통해 4주차 과제에 움직임을 추가하는 것을 연습했다. 다수의 실용방법이 있었기에 여러가지를 도전해 볼 수 있었고 특히 x,y,z방향으로 움직이는 것을 통해 3D느낌을
 홈페이지에 주는 것을 알게 되었다. 또한 레이아웃 과정에서 고려해야 하는 순서나 css문법들을 고려하며 학습할 수 있었고 여러가지 애니메이션을 추가 및 합성할 수 있게 되었다.
 아쉬운 점은 이미지를 활용하여 배경으로 넣고 싶어 도전했지만 background-image('../image/01.jpg');를 활용해도 도저히 배경으로 이미지가 넘어가지 않았다. 이는 더 노력해서 무엇이 문제인지
 파악 후에 실행할 예정이다. 이를 통해 웹 프로그래밍 하는 것에 자신감이 생겼고 레이아웃하고 틀을 만드는데 능숙하게 사용할 수 있게 되었다.





