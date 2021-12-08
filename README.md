# Phaser 기반으로 구현한 퍼즐 장르의 웹 게임 - Colorful World
<img width="640" height="360" src="https://user-images.githubusercontent.com/42332051/141237238-44b1340f-7085-40cb-b97d-275f6581c26f.gif">

## 개요
주어진 색상 선택지를 이용해서 색상을 합성하여 제시된 정답 색상을 맞추는 게임.

## 개발 환경 및 사용 API
1. Back-end
   - Python 3.9.5
   - Flask 2.0.2
2. Front-end
   - HTML5, CSS3, JavaScript(ECMAScript6)
   - jQuery 3.6.0
   - Bootstrap 5.1.3
3. API
   - Phaser 3.55.2

## 주요 기능
1. 메인 페이지
   - <img width="640" height="360" src="https://user-images.githubusercontent.com/42332051/141237250-07839e8c-751e-4489-a923-ce4976534f30.gif">
   - 게임 페이지로 이동할 수 있다.
   - 게임 방법을 모달 형태로 표시하여 알려준다.
2. 게임 화면
   - <img width="640" height="360" src="https://user-images.githubusercontent.com/42332051/141237259-e3f57e00-d081-454e-aa3e-a36105dbaba2.gif">
   - *위/아래 화살표 키*를 이용해서 **색칠할 바탕을 지정**할 수 있다.
   - *왼쪽/오른쪽 화살표 키*를 이용해서 **왼쪽/오른쪽 색상 팔레트를 회전**시킬 수 있다.
   - *스페이스 키*를 이용해서 **왼쪽/오른쪽 팔레트의 색상을 합성해서 지정된 바탕에 적용**한다.
   - 모든 바탕의 색상을 상단의 목표 이미지와 동일하게 색칠하면 게임 클리어 메시지가 모달 형태로 표시된다.

## 게임 동작 원리
1. **색상 데이터 생성**
   - **정답 색상 데이터 3개를 임의로 생성**한다. 각각의 색상 데이터는 [0, 255] 범위의 rgb 값으로 구성한다.
   - **선택지 색상 데이터 6개를 임의로 생성**한다. 지정된 두 색상의 rgb 값의 평균이 정답 데이터와 일치하도록 구성한다.
   - 생성된 정답 및 선택지 색상 데이터를 배열에 저장하고 순서를 임의로 섞는다.
2. **색상 설정**
   - 게임 화면을 로딩할 때, 색상 데이터가 저장된 배열을 읽어서 목표 이미지 및 왼쪽/오른쪽 팔레트 이미지들을 모두 초기화한다.
   - *위/아래 화살표 키*를 입력하면 *색칠할 바탕을 지정*할 수 있다. 기존에 지정된 바탕에 대한 커서를 비활성화하고 새로 지정된 바탕에 대한 **커서를 활성화**한다.
   - *왼쪽/오른쪽 화살표 키*를 입력하면 *왼쪽/오른쪽 팔레트를 회전*시킬 수 있다. 화면에 표시된 왼쪽/오른쪽 팔레트의 색상을 이용해서 **합성된 색상 값을 계산하고 커서에 적용**한다.
   - *스페이스 키*를 입력하면 커서에 적용된 색상을 **지정된 바탕에 적용**한다.
3. **클리어 판정**
   - 팔레트 회전이 발생할 때마다, 목표 색상과 바탕 색상이 일치하는지 하나씩 검사한다.
   - 검사를 모두 통과하면 모달 창을 통해 게임 클리어 메시지를 표시한다.

## 비고
- 실행 방법(Windows 운영체제 기준)
  - (Flask가 설치된 환경에서, 명령 프롬프트에서 앱이 위치하는 폴더를 지정한 후)
  - set FLASK_APP=colorful_world
  - flask run
