# SPOT
대학생연합IT동아리 잇타(IT'sTIME) 4기 잇플 프로젝트<br/>
위치정보 기반 동네 정보 공유 플랫폼

## 주요 페이지 및 기능 설명
- 로그인&회원정보입력<br/>
  <h4>로그인</h4>
  1. 애플로그인&카카오로그인 지원
     spring security를 이용하여 jwt 인증/인가 구현
     <img width="1433" alt="image" src="https://github.com/iTpple-S-POT/.github/assets/49396352/4b9864d3-c54f-441a-af20-c2127d6516f9">
  <h4>유저정보 입력</h4>
  1. 유저 정보 관련 입력 및 수정 api(post: 유저 정보 입력, put: 유저 정보 수정)
     자유롭게 데이터 입력/수정 가능
     <img width="1435" alt="image" src="https://github.com/iTpple-S-POT/.github/assets/49396352/aeb35cce-70ef-4fe8-a541-edeb2b4d3a2d">
     
     ```json
     
     {
      "_comment": "유저 조회할 경우 데이터",
      "id": 1,
      "loginType": "KAKAO",
      "profileImageUrl": "test.jpg",
      "name": "test",
      "nickname": "test",
      "phoneNumber": "010-0000-0000",
      "birthDay": "2024-01-25",
      "gender": "FEMALE",
      "mbti": "ENFP",
      "interests": [
        "영화"
      ],
      "status": "PROGRESS"
     }
     ```
- 팟 생성&조회(카테고리)<br/>
  <h4>팟 생성</h4>
  1. 팟 생성 시 위도경도 기반 좌표계를 통해 위치를 특정지음
  2. 이때 이미지는 aws s3 presigned url를 사용하여 image upload 시 보안&속도 향상
  3. 해시태그는 따로 입력을 받아 db에 역인덱스 구조 테이블을 생성하여 조회 시 성능이 떨어지지 않게 관리함
     <img width="1438" alt="image" src="https://github.com/iTpple-S-POT/.github/assets/49396352/21285f90-d13d-4bd0-a06e-cabb6877c9a8">
  <h4>팟 조회</h4>
  
  1. 팟 조회 시 현재 지점에서 반경 3km까지 조회할 수 있음. 또한 카테고리 및 해시태그로 필터 가능
     ```json
     {
       "_comment": "팟 조회할 경우 데이터",
       [
          {
            "id": 0,
            "userId": 0,
            "categoryId": [
              0
            ],
            "potType": "TEXT",
            "content": "string",
            "location": {
              "lat": 0,
              "lon": 0
            },
            "imageKey": "string",
            "expiredAt": "2024-01-25T11:06:00.618Z",
            "hashtagList": [
              {
                "hashtagId": 0,
                "hashtag": "string"
              }
            ],
            "viewCount": 0
          }
        ]
     } 
     ```
  <h4>좋아요 및 대댓글 기능</h4>
  1. 팟 개별로 좋아요를 달 수 있음.
    <img width="1440" alt="image" src="https://github.com/iTpple-S-POT/.github/assets/49396352/e0ebcb00-c2d0-405a-8bb4-c48379c50215">

  2. 대댓글 작성 시 특정 댓글에 연속적으로 댓글 작성 가능.
    <img width="1441" alt="image" src="https://github.com/iTpple-S-POT/.github/assets/49396352/d287e48f-05de-490f-8056-6d78faf4711e">

    ```json
    [
      "_comment": "댓글 조회할 경우 데이터",
      {
        "commentId": 1,
        "content": "test",
        "commentUpdatedAt": "2024-01-25T11:11:30.912Z",
        "writer": {
          "userId": 1,
          "profileImageUrl": "test.jpg",
          "name": "username"
        }
      }
    ]
    ```


- 마이페이지<br/>
- 그 외 주요 기능(해시태그 검색 등)<br/>
