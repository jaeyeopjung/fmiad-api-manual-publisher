FMI-AD API 연동가이드
---

### 목차
##### I. Reward(보상형) 연동
##### II. nReward(비보상형) 연동
##### III. CPC (클릭형) 연동
##### IV. 연동 공통
##### V. 기타

<br/>
<br/>

I. Reward(보상형) 연동
----

1. **광고 요청 (설치형-CPI / 실행형-CPE / 액션형-CPA / … )**

    ```
    광고 요청을 통해 광고 목록 또는 단일 광고를 요청하는 방식으로 제공되는 API 입니다.
    단일 광고 연동의 경우 사전 협의하여 URL 직접 전달하여 처리하는 방식으로도 제공됩니다.
    단일 광고 연동의 경우 포커스엠 비즈니스팀과 협의하여 진행하시길 바랍니다.
    URL 전달형 연동의 경우 광고 요청 API 연동은 생략 가능합니다.
    ```
   
    1. **Request**
    
        1. **연동방식**
            
            > Redirect 연동형 : 매체에서 판단없이 FMI을 통해 광고 참여 처리 시 사용<br/>
            JSON 연동형 : 매체에서 광고 상태를 확인하여 매체에서 광고 참여 등을 직접 처리
            
            **광고 요청 시 리턴되는 JSON DATA에 각 연동 타입에 맞는 정보가 제공됩니다.**
            
            URL : <br/>
                http://ad.focusm.kr/service/freeList.php (Redirect 연동형) - 3. 광고 참여 (REDIRECT TYPE) 참고<br/>              
                http://ad.focusm.kr/service/freeListL.php (JSON 연동형) - 4. 광고 참여 (JSON TYPE) 참고
            
            Method : GET 방식으로 요청
            
        2. **Parameters**
            
            | Parameter Name | Essential | Desc.  |
            | :------------: | :-------: | :----------------------- |
            | mid            | O         | **매체 코드** <br/> - 포커스엠에서 발급한 매체 코드 |
            | adimg          | -         | 추가 이미지 타입<br/> - ddhl (정사각형)<br/> - floating3 (띠배너)<br/> - fullimg (풀이미지)<br/> - ptscs (직사각형)<br/> ex) adimg=ddhl,floating3<br/><br/> * icon 이외 배너 이미지 등을 요청 시에만 사용됩니다.  |
        
    2. **Response**
    
        1. **Result infos**
        
            | Parameter Name  | Essential | Desc.  |
            | :-------------: | :-------: | :----------------------- |
            | Result          | O         | 결과 여부 <br/> - true : 정상, false : 오류 |
            | ResultCode      | O         | 결과 코드                                   |
            | ResultMsg       | O         | 결과 메시지                                 |
            | Campaigns []    | -                                                      ||
            | AdId            | -         | 광고코드            |
            | AdTitle         | -         | 광고명칭            |
            | AdType          | -         | 광고 타입<br/> - install : 설치형<br/> - click : 클릭형<br/> - imapressions : 노출형<br/> - run : 실행형<br/> - action : 액션형 |
            | AppPackage      | -         | 패키지명            |
            | AppName         | -         | 앱 이름            |
            | AppDownloadURL  | -         | 광고 참여시 호출 URL            |
            | AppShowURL      | -         | 광고 노출시 호출 URL            |
            | AppIcon         | -         | 앱아이콘 URL            |
            | ViewTitle       | -         | 광고 타이틀            |
            | ViewDesc        | -         | 광고 설명            |
            | AdADType        | -         | 매체 구분 코드            |
            | DeviceVer       | -         | 단말 버전            |
            | addImage        | -         | 추가 이미지 URL            |
            | addWidth        | -         | 광고 소재 가로 사이즈            |
            | addHeight       | -         | 광고 소재 세로 사이즈            |
            | DayCut          | -         | 일 노출 제한 값            |
            | DayClickCut     | -         | 일 클릭 제한 값            |
            | DayGoalCut      | -         | 일 실행 제한 값            |
            | Price           | -         | 매체 단가            |
            | UserPoint       | -         | 매체 사용자 단가            |
            | Country         | -         |  국가 코드           |
        
        2. **Result example**
            
            (성공)
            ```json
            {
                "Result": "true" ,
                "ResultCode": 1 ,
                "ResultMsg": "참여가능",
                "Campaigns": [
                    {
                        "AdId": "SAD1712014",
                        "AdTitle": "뮤직메이트",
                        "AdType": "run",
                        "AppPackage": "skplanet.musicmate",
                        "AppName": "뮤직메이트",
                        "AppDownloadUrl": "http://ad.focusm.kr/service/freeLanding.php?ad_type=1&mid=AD1404003366&aid=SAD1712014&uid=",
                        "AppShowUrl": "http://ad.focusm.kr/service/freeShow.php?ad_type=1&mid=AD1404003366&aid=SAD1712014&uid=",
                        "AppIcon": "http://img.focusm.co.kr/data/ad/SP1407002_05160733a200.png",
                        "ViewTitle": "뮤직메이트 ",
                        "ViewDesc": "국내 정상급 음원 보유량의 모바일 스트리밍 서비스",
                        "AdADType": "1",
                        "DeviceVer": "9",
                        "addImage": "",
                        "DayCut": 0,
                        "DayClickCut": 0,
                        "UserPoint": 0,
                        "Country": "KR"
                    },
                    {
                        "AdId": "SAD1606058",
                        "AdTitle": "앱리프트_킹덤스토리 (사이트 NCPI 노출)",
                        "AdType": "run",
                        "AppPackage": "com.nhnent.SK10392",
                        "AppName": "킹덤스토리",
                        "AppDownloadUrl": "http://ad.focusm.kr/service/freeLanding.php?ad_type=1&mid=AD1404003366&aid=SAD1606058&uid=",
                        "AppShowUrl": "http://ad.focusm.kr/service/freeShow.php?ad_type=1&mid=AD1404003366&aid=SAD1606058&uid=",
                        "AppIcon": "http://img.focusm.co.kr/data/ad/SP1405010_08114840a77.png",
                        "ViewTitle": "킹덤스토리",
                        "ViewDesc": "매일 펼쳐지는 천하제일장수대회! PVP 최강자들이 누리는 원보 파티!",
                        "AdADType": "1",
                        "DeviceVer": "9",
                        "addImage": "",
                        "DayCut": 0,
                        "DayClickCut": 0,
                        "UserPoint": 0,
                        "Country": "KR"
                    }
                ]
            }
            ```
            
            (실패)
            ```json
            {"Result":"false", "ResultCode": "89", "ResultMsg" : "광고없음", "Campaigns": []}
            ```        

2. **노출 신호 (OPTIONAL)**

    ```
    광고 요청 API 사용하지 않고 단일 광고에 대해 FMI으로부터 직접 전달받아 사용하는 경우 사용됩니다.
    FMI에서 노출 빈도를 집계하기 위한 API 입니다.
    매체 사정에 의해 생략 가능합니다.
    ```

    1. **Request**
        
        1. **연동방식**
            
            URL : http://ad.focusm.kr/service/freeShow.php <br/>
            Method : GET 방식으로 요청
            
        2. **Parameters**
            
            | Parameter Name | Essential | Desc.                                                               |
            | :------------: | :-------: | :------------------------------------------------------------------ |
            | mid            | O         | **매체 코드** <br/> - 포커스엠에서 발급한 매체 코드                |
            | aid            | O         | **광고 코드** <br/> - 포커스엠에서 생성한 연동 광고 코드           |
            | uid            | -         | 매체에서 식별할 수 있는 유일키 정보 <br/> ex) 사용자 고유 키 등     |
            | puid2          | -         | 기기 고유 값 <br/> - IMEI 정보 (없을 경우 mac address 로 대체 가능) |
            | adid           | -         | 구글 광고 ID                                                        |
        
    2. **Response**
    
        1. **Result infos**
        
            | Parameter Name  | Essential | Desc.                    |
            | :-------------: | :-------: | :----------------------- |
            | ResultCode      | O         | 결과 코드                |
            | ResultMsg       | O         | 결과 메시지              |
        
        2. **Result example**
            
            (성공)
            ```json
            {"ResultCode": "10", "ResultMsg" : "정상처리"}
            ```
            
            (실패)
            ```json
            {"ResultCode": "100", "ResultMsg" : "참여 중 오류 발생"}
            ```        

3. **광고 참여 (REDIRECT TYPE)**

    ```
    광고 참여 요청으로 광고 설치 마켓이나 트래커 또는 광고 상태에 따른 페이지로 redirect 처리
    광고 요청 연동 시에는 response 를 통해 제공되는 URL 사용 가능
    ```

    1. **Request**
        
        1. **연동방식**
            
            URL : http://ad.focusm.kr/service/freeGoto.php <br/>
            Method : GET 방식으로 요청
            
        2. **Parameters**
            
            | Parameter Name | Essential | Desc.                                                               |
            | :------------: | :-------: | :------------------------------------------------------------------ |
            | mid            | O         | **매체 코드** <br/> - 포커스엠에서 발급한 매체 코드                |
            | aid            | O         | **광고 코드** <br/> - 포커스엠에서 생성한 연동 광고 코드           |
            | uid            | O         | 매체에서 식별할 수 있는 유일키 정보 <br/> ex) 사용자 고유 키 등 <br/> * Reward 광고 연동 시 필수 |
            | puid2          | O         | 기기 고유 값 <br/> - IMEI 정보 (없을 경우 mac address 로 대체 가능) <br/> * Reward 광고 연동 시 필수 |
            | adid           | O         | 구글 광고 ID <br/> * Reward 광고 연동 시 필수 |
            | ad_type        | O         | 광고 구분 코드 <br/> - 광고 요청시 광고의 매체 구분 코드            |
        
    2. **Response**

        result 정보 없이 요청 페이지로 redirect

4. **광고 참여 (JSON TYPE)**

    ```
    광고 참여 요청으로 광고 상태와 광고 참여 URL 정보를 리턴
    광고 요청 연동 시에는 response 를 통해 제공되는 URL 사용 가능
    ```

    1. **Request**
        
        1. **연동방식**
            
            URL : http://ad.focusm.kr/service/freeLanding.php <br/>
            Method : GET 방식으로 요청
            
        2. **Parameters**
            
            | Parameter Name | Essential | Desc.                                                               |
            | :------------: | :-------: | :------------------------------------------------------------------ |
            | mid            | O         | **매체 코드** <br/> - 포커스엠에서 발급한 매체 코드                |
            | aid            | O         | **광고 코드** <br/> - 포커스엠에서 생성한 연동 광고 코드           |
            | uid            | O         | 매체에서 식별할 수 있는 유일키 정보 <br/> ex) 사용자 고유 키 등 <br/> * 광고참여완료 POSTBACK 연동시 필수 |
            | puid2          | O         | 기기 고유 값 <br/> - IMEI 정보 (없을 경우 mac address 로 대체 가능) <br/> * Reward 광고 연동 시 필수 |
            | adid           | O         | 구글 광고 ID <br/> * Reward 광고 연동 시 필수 |
            | ad_type        | O         | 광고 구분 코드 <br/> - 광고 요청시 광고의 매체 구분 코드            |
        
    2. **Response**

        1. **Result infos**
        
            | Parameter Name  | Essential | Desc.                     |
            | :-------------: | :-------: | :-----------------------  |
            | Result          | O         | 결과 여부 (true or false) |
            | ResultCode      | O         | 결과 코드                 |
            | ResultMsg       | O         | 결과 메시지               |
            | LandingURL      | O         | 광고 참여 URL             |

        2. **Result example**
            
            (성공)
            ```json
            {
              "Result": true,
              "ResultCode": "10",
              "ResultMsg": "참여가능",
              "LandingURL": "[광고 참여 URL]"
            }
            ```
            
            (실패)
            ```json
            {
              "Result": false,
              "ResultCode": "2000",
              "ResultMsg": "이미광고에 참여",
              "LandingURL": ""
            }
            ```           

5. **광고 참여 완료 (설치형-CPI)**

    ```
    설치형 광고에만 해당하는 경우이며, 설치 완료 후 설치 완료에 대한 신호를 전송 해야합니다.
    ```

    1. **Request**
        
        1. **연동방식**
            
            URL : http://ad.focusm.kr/service/freeInstall.php <br/>
            Method : GET 방식으로 요청
            
        2. **Parameters**
            
            | Parameter Name | Essential | Desc.                                                               |
            | :------------: | :-------: | :------------------------------------------------------------------ |
            | mid            | O         | **매체 코드** <br/> - 포커스엠에서 발급한 매체 코드                |
            | aid            | O         | **광고 코드** <br/> - 포커스엠에서 생성한 연동 광고 코드           |
            | uid            | O         | 매체에서 식별할 수 있는 유일키 정보 <br/> ex) 사용자 고유 키 등 <br/> * 광고 참여완료 POSTBACK 연동시 필수 |
            | puid2          | O         | 기기 고유 값 <br/> - IMEI 정보 (없을 경우 mac address 로 대체 가능) <br/> * Reward 광고 연동 시 필수 |
            | adid           | O         | 구글 광고 ID <br/> * Reward 광고 연동 시 필수 |
            | puid           | O         | 광고 구분 코드 <br/> - 광고 요청시 광고의 매체 구분 코드            |
        
    2. **Response**

        1. **Result infos**
        
            | Parameter Name  | Essential | Desc.                     |
            | :-------------: | :-------: | :-----------------------  |
            | ResultCode      | O         | 결과 코드                 |
            | ResultMsg       | O         | 결과 메시지               |

        2. **Result example**
            
            (성공)
            ```json
            {
                "ResultCode": "10",
                "ResultMsg": "참여완료"
            }

            ```
            
            (실패)
            ```json
            {
                "ResultCode": "2000",
                "ResultMsg": "이미광고에 참여"
            }
            ```
            
            ```json
            {
            "ResultCode": "99",
            "ResultMsg": "참여불가"
            }
            ```   

II. nReward(비보상형) 연동
----

1. **광고 요청 (설치형-CPI / 실행형-CPE / 액션형-CPA / … )**

    ```
    광고 요청을 통해 광고 목록 또는 단일 광고를 요청하는 방식으로 제공되는 API 입니다.
    단일 광고 연동의 경우 사전 협의하여 URL 직접 전달하여 처리하는 방식으로도 제공됩니다.
    단일 광고 연동의 경우 포커스엠 비즈니스팀과 협의하여 진행하시길 바랍니다.
    URL 전달형 연동의 경우 광고 요청 API 연동은 생략 가능합니다.
    ```
   
    1. **Request**
    
        1. **연동방식**
            
            > Redirect 연동형 : 매체에서 판단없이 FMI을 통해 광고 참여 처리 시 사용<br/>
            JSON 연동형 : 매체에서 광고 상태를 확인하여 매체에서 광고 참여 등을 직접 처리
            
            **광고 요청 시 리턴되는 JSON DATA에 각 연동 타입에 맞는 정보가 제공됩니다.**
            
            URL : <br/>
                http://ad.focusm.kr/service/freeList.php (Redirect 연동형) - 3. 광고 참여 (REDIRECT TYPE) 참고<br/>              
                http://ad.focusm.kr/service/freeListL.php (JSON 연동형) - 4. 광고 참여 (JSON TYPE) 참고
            
            Method : GET 방식으로 요청
            
        2. **Parameters**
            
            | Parameter Name | Essential | Desc.  |
            | :------------: | :-------: | :----------------------- |
            | mid            | O         | **매체 코드** <br/> - 포커스엠에서 발급한 매체 코드 |
            | adimg          | -         | 추가 이미지 타입<br/> - ddhl (정사각형)<br/> - floating3 (띠배너)<br/> - fullimg (풀이미지)<br/> - ptscs (직사각형)<br/> ex) adimg=ddhl,floating3<br/><br/> * icon 이외 배너 이미지 등을 요청 시에만 사용됩니다.  |
        
    2. **Response**
    
        1. **Result infos**
        
            | Parameter Name  | Essential | Desc.  |
            | :-------------: | :-------: | :----------------------- |
            | Result          | O         | 결과 여부 <br/> - true : 정상, false : 오류 |
            | ResultCode      | O         | 결과 코드                                   |
            | ResultMsg       | O         | 결과 메시지                                 |
            | Campaigns  []   | -                                                      ||
            | AdId            | -         | 광고코드            |
            | AdTitle         | -         | 광고명칭            |
            | AdType          | -         | 광고 타입<br/> - install : 설치형<br/> - click : 클릭형<br/> - imapressions : 노출형<br/> - run : 실행형<br/> - action : 액션형 |
            | AppPackage      | -         | 패키지명            |
            | AppName         | -         | 앱 이름            |
            | AppDownloadURL  | -         | 광고 참여시 호출 URL            |
            | AppShowURL      | -         | 광고 노출시 호출 URL            |
            | AppIcon         | -         | 앱아이콘 URL            |
            | ViewTitle       | -         | 광고 타이틀            |
            | ViewDesc        | -         | 광고 설명            |
            | AdADType        | -         | 매체 구분 코드            |
            | DeviceVer       | -         | 단말 버전            |
            | addImage        | -         | 추가 이미지 URL            |
            | addWidth        | -         | 광고 소재 가로 사이즈            |
            | addHeight       | -         | 광고 소재 세로 사이즈            |
            | DayCut          | -         | 일 노출 제한 값            |
            | DayClickCut     | -         | 일 클릭 제한 값            |
            | DayGoalCut      | -         | 일 실행 제한 값            |
            | Price           | -         | 매체 단가            |
            | UserPoint       | -         | 매체 사용자 단가            |
            | Country         | -         |  국가 코드           |
        
        2. **Result example**
            
            (성공)
            ```json
            {
                "Result": "true" ,
                "ResultCode": 1 ,
                "ResultMsg": "참여가능",
                "Campaigns": [
                {
                    "AdId": "SAD1406012",
                    "AdTitle": "TOP10 보상형 실행광고",
                    "AdType": "run",
                    "AppDownloadUrl": "http://ad.focusm.kr/service/freeGoto.php?mid=AD140100374&ad_type=1&aid=SAD1406012&uid=",
                    "AppIcon": "http://ad.focusm.kr/data/ad/SP1406004_20164052a0.png",
                    "AppPackage": "kr.co.ytop10",
                    "AppShowUrl": "http://ad.focusm.kr/service/freeShow.php?mid=AD140100374&ad_type=1&aid=SAD1406012&uid=",
                    "ViewDesc": "TOP10 설명",
                    "ViewTitle": "TOP10",
                    "addImage": "http://ad.focusm.kr/data/ad/SP1406004_20164052a11.png"
                },
                {
                    "AppShowUrl": "http://ad.focusm.kr/service/freeShow.php?mid=AD140100374&ad_type=2&aid=SAD1406013&uid=",
                    "AdId": "SAD1406013",
                    "AdTitle": "어디갈까 보상형 설치광고",
                    "AdType": "install",
                    "AppDownloadUrl": "http://ad.focusm.kr/service/freeGoto.php?mid=AD140100374&ad_type=2&aid=SAD1406013&uid=",
                    "AppIcon": "http://ad.focusm.kr/data/ad/SP1406004_20164052a1.png",
                    "AppPackage": "kr.co.thisweek",
                    "ViewDesc": "어디갈까설명",
                    "ViewTitle": "어디갈까",
                    "AdADType": "2",
                    "addImage": "http://ad.focusm.kr/data/ad/SP1406004_20164052a11.png"
                }
            ] 
            }
            ```
            
            (실패)
            ```json
            {"Result":"false", "ResultCode": "89", "ResultMsg" : "광고없음", "Campaigns": []}
            ```        

2. **노출 신호 (OPTIONAL)**

    ```
    광고 요청 API 사용하지 않고 단일 광고에 대해 FMI으로부터 직접 전달받아 사용하는 경우 사용됩니다.
    FMI에서 노출 빈도를 집계하기 위한 API 입니다.
    매체 사정에 의해 생략 가능합니다.
    ```

    1. **Request**
        
        1. **연동방식**
            
            URL : http://ad.focusm.kr/service/freeShow.php <br/>
            Method : GET 방식으로 요청
            
        2. **Parameters**
            
            | Parameter Name | Essential | Desc.                                                               |
            | :------------: | :-------: | :------------------------------------------------------------------ |
            | mid            | O         | **매체 코드** <br/> - 포커스엠에서 발급한 매체 코드                |
            | aid            | O         | **광고 코드** <br/> - 포커스엠에서 생성한 연동 광고 코드           |
            | uid            | -         | 매체에서 식별할 수 있는 유일키 정보 <br/> ex) 사용자 고유 키 등     |
            | puid2          | -         | 기기 고유 값 <br/> - IMEI 정보 (없을 경우 mac address 로 대체 가능) |
            | adid           | -         | 구글 광고 ID                                                        |
        
    2. **Response**
    
        1. **Result infos**
        
            | Parameter Name  | Essential | Desc.                    |
            | :-------------: | :-------: | :----------------------- |
            | ResultCode      | O         | 결과 코드                |
            | ResultMsg       | O         | 결과 메시지              |
        
        2. **Result example**
            
            (성공)
            ```json
            {"ResultCode": "10", "ResultMsg" : "정상처리"}
            ```
            
            (실패)
            ```json
            {"ResultCode": "100", "ResultMsg" : "참여 중 오류 발생"}
            ```        

3. **광고 참여 (REDIRECT TYPE)**

    ```
    광고 참여 요청으로 광고 설치 마켓이나 트래커 또는 광고 상태에 따른 페이지로 redirect 처리
    광고 요청 연동 시에는 response 를 통해 제공되는 URL 사용 가능
    ```

    1. **Request**
        
        1. **연동방식**
            
            URL : http://ad.focusm.kr/service/freeGoto.php <br/>
            Method : GET 방식으로 요청
            
        2. **Parameters**
            
            | Parameter Name | Essential | Desc.                                                               |
            | :------------: | :-------: | :------------------------------------------------------------------ |
            | mid            | O         | **매체 코드** <br/> - 포커스엠에서 발급한 매체 코드                |
            | aid            | O         | **광고 코드** <br/> - 포커스엠에서 생성한 연동 광고 코드           |
            | uid            | O         | 매체에서 식별할 수 있는 유일키 정보 <br/> ex) 사용자 고유 키 등 <br/> * 광고참여완료 POSTBACK 연동 시 필수 항목 |
            | puid2          | -         | 기기 고유 값 <br/> - IMEI 정보 (없을 경우 mac address 로 대체 가능) |
            | adid           | -         | 구글 광고 ID  |
            | ad_type        | O         | 광고 구분 코드 <br/> - 광고 요청시 광고의 매체 구분 코드            |
        
    2. **Response**

        result 정보 없이 요청 페이지로 redirect

4. **광고 참여 (JSON TYPE)**

    ```
    광고 참여 요청으로 광고 상태와 광고 참여 URL 정보를 리턴
    광고 요청 연동 시에는 response 를 통해 제공되는 URL 사용 가능
    ```

    1. **Request**
        
        1. **연동방식**
            
            URL : http://ad.focusm.kr/service/freeLanding.php <br/>
            Method : GET 방식으로 요청
            
        2. **Parameters**
            
            | Parameter Name | Essential | Desc.                                                               |
            | :------------: | :-------: | :------------------------------------------------------------------ |
            | mid            | O         | **매체 코드** <br/> - 포커스엠에서 발급한 매체 코드                |
            | aid            | O         | **광고 코드** <br/> - 포커스엠에서 생성한 연동 광고 코드           |
            | uid            | O         | 매체에서 식별할 수 있는 유일키 정보 <br/> ex) 사용자 고유 키 등 <br/> * 광고참여완료 POSTBACK 연동시 필수 |
            | puid2          | O         | 기기 고유 값 <br/> - IMEI 정보 (없을 경우 mac address 로 대체 가능) |
            | adid           | O         | 구글 광고 ID <br/> * Reward 광고 연동 시 필수 |
            | ad_type        | O         | 광고 구분 코드 <br/> - 광고 요청시 광고의 매체 구분 코드            |
        
    2. **Response**

        1. **Result infos**
        
            | Parameter Name  | Essential | Desc.                     |
            | :-------------: | :-------: | :-----------------------  |
            | Result          | O         | 결과 여부 (true or false) |
            | ResultCode      | O         | 결과 코드                 |
            | ResultMsg       | O         | 결과 메시지               |
            | LandingURL      | O         | 광고 참여 URL             |

        2. **Result example**
            
            (성공)
            ```json
            {
              "Result" : true,
              "ResultCode" : "10",
              "ResultMsg" : "참여가능",
              "LandingURL" : "[광고 참여 URL]"
            }
            ```
            
            (실패)
            ```json
            {
              "Result": false,
              "ResultCode": "99",
              "ResultMsg": "참여불가",
              "LandingURL": ""
            }
            ```
                
            ```json
            {
              "Result": false,
              "ResultCode": "9999",
              "ResultMsg": "올바른 처리가 아님",
              "LandingURL": ""
            }
            ```           

5. **광고 참여 완료 (설치형-CPI)**

    ```
    설치형 광고에만 해당하는 경우이며, 설치 완료 후 설치 완료에 대한 신호를 전송 해야합니다.
    ```

    1. **Request**
        
        1. **연동방식**
            
            URL : http://ad.focusm.kr/service/freeInstall.php <br/>
            Method : GET 방식으로 요청
            
        2. **Parameters**
            
            | Parameter Name | Essential | Desc.                                                               |
            | :------------: | :-------: | :------------------------------------------------------------------ |
            | mid            | O         | **매체 코드** <br/> - 포커스엠에서 발급한 매체 코드                |
            | aid            | O         | **광고 코드** <br/> - 포커스엠에서 생성한 연동 광고 코드           |
            | uid            | O         | 매체에서 식별할 수 있는 유일키 정보 <br/> ex) 사용자 고유 키 등 <br/> * 광고참여완료 POSTBACK 연동시 필수 |
            | puid2          | O         | 기기 고유 값 <br/> - IMEI 정보 (없을 경우 mac address 로 대체 가능)  |
            | adid           | O         | 구글 광고 ID |
            | puid           | O         | 광고 구분 코드 <br/> - 광고 요청시 광고의 매체 구분 코드 <br/> * puid2 파라미터를 보내지 못하는 경우 사용 |
        
    2. **Response**

        1. **Result infos**
        
            | Parameter Name  | Essential | Desc.                     |
            | :-------------: | :-------: | :-----------------------  |
            | ResultCode      | O         | 결과 코드                 |
            | ResultMsg       | O         | 결과 메시지               |

        2. **Result example**
            
            (성공)
            ```json
            {
                "ResultCode": "10",
                "ResultMsg": "참여완료"
            }

            ```
            
            (실패)
            ```json
            {
                "ResultCode": "9999",
                "ResultMsg": "올바른 처리가 아님"
            }
            ```
            
            ```json
            {
            "ResultCode": "99",
            "ResultMsg": "참여불가"
            }
            ``` 

III. CPC (클릭형) 연동
----

1. **광고 요청 (클릭형)**

    클릭형(CPC) 광고에 대한 요청을 보내고 JSON 형태의 광고 정보를 회신 받는다.<br/>
    정상으로 요청된 광고는 HTML로 제공한다.<br/> 
    
    1. **request**
    
        1. **연동방식**
            
            URL : http://ad.focusm.kr/api2/ncpc_imp
            Method : GET, POST 방식으로 연동
            
        2. **Parameter**
        
            | Parameter Name | Essential | Desc.                                                               |
            | :------------: | :-------: | :------------------------------------------------------------------ |
            | mid            | O         | **매체 코드** <br/> - 포커스엠에서 발급한 매체 코드                |
            | os             | O         | **OS 종류** <br/> - ex) android, ios           |
            | adid           | O         | **유일키** <br/> - s_type : 1 (application) 인 경우 <br/>  android google ads id, ios IDFA  |
            | adtype         | O         | 기기 고유 값 <br/> - IMEI 정보 (없을 경우 mac address 로 대체 가능)  |
            | s_type         | O         | **서비스 타입** <br/> - 1 : application <br/> - 2 : mobile web site |
            | agent          | -         | 광고 구분 코드 <br/> - 광고 요청시 광고의 매체 구분 코드 <br/> * puid2 파라미터를 보내지 못하는 경우 사용 |
            | osv            | -         | 광고 구분 코드 <br/> - 광고 요청시 광고의 매체 구분 코드 <br/> * puid2 파라미터를 보내지 못하는 경우 사용 |
            | model          | -         | 광고 구분 코드 <br/> - 광고 요청시 광고의 매체 구분 코드 <br/> * puid2 파라미터를 보내지 못하는 경우 사용 |
            | pkg            | O         | 패키지 명 또는 사이트 도메인 <br/> - 광고 요청시 광고의 매체 구분 코드 <br/> * puid2 파라미터를 보내지 못하는 경우 사용 |
        
    2. **response**
    
        1. **Result infos**

            | Parameter Name  | Essential | Desc.                     |
            | :-------------: | :-------: | :-----------------------  |
            | code            | O         | **결과 코드** <br/> - 10 : 광고 있음, 99 : 광고 없음 |
            | adcode          | O         | **광고 코드**               |        
            | html            | O         | **광고** <br/> - webview 또는 browser 에서 바로 사용 |        
            | time            | O         | **회신시간**               |        
        
        2. **Result example**
        
            (성공)
            ```json
            {
            "adcode": "SAD0000000",
            "code": 10,
            "html": "<div><a href=\"http://ad.focusm.kr/service/freeGoto.php?ad_type=1&aid=SAD1606001&mid=AD16060041496\"><img src=\"http://img.shoppingcast.kr/data/files/ai20160629132312_16.jpg\" style=\"width: 100%; height: 100%;\"></a></div>",
            "time": 1467264462
            }
            ```
            
            (실패)
            ```json
            {
               "code": 99,
               "adcode": "",
               "html": "",
               "time": 1467264462
             }
            ```
            
IV. 연동 공통
----

1. **광고 참여 완료 POSTBACK (OPTION)**

    광고 참여 완료 신호를 포커스엠에서 매체로 전달해 주기 위한 연동입니다.<br/>
    매체사는 전달 받을 POSTBACK URL 을 포커스엠 비지니스팀에 전달하여 등록해야 합니다.<br/> 
    Reward 광고의 경우 필수 연동.<br/>
    
    **postback URL 과 연동 method 를 등록 후 연동 가능**
    
    1. **request**
    
        1. **연동방식**
            
            URL : 매체사에서 구현한 URL 정보
            Method : GET, POST 방식으로 연동
            
        2. **Parameter (POST)**
        
            | Parameter Name  | Essential | Desc. |
            | :------: | :---: | :----------------------- |
            | puid     | -    | **Transaction ID** <br/> - FocusM 에서 처리된 Transaction ID |
            | uid      | -    | 매체에서 전달한 식별할 수 있는 유일키 정보<br/>ex) 사용자 고유 키, transaction key 등.  |
            | adtitle  | -    | 광고 제목 |
            | price    | -    | 사용자 단가 |
            | userip   | -    | 광고 참여시 IP 정보 |
            | adcode   | -    | **광고 코드**<br/> - 포커스엠에서 생성한 연동 광고 코드  |
        
        3. **Parameter (GET)**
            ```
            Macro 값들이 치환되어 지정된 Parameter Name 으로 정보가 전달됩니다. 
            GET 방식을 원하시는 경우 매크로가 포함된 Full URL로 전달 바랍니다.
            ex) [매체사URL]?[매체사 지정 파라미터명1]={puid}&[매체사지정파라미터명2]={uid}&[매체사지정파라미터명3]={adtitle}&(생략...)
            ```      
                
### V. 기타

1. **공통 결과 코드**
    
    | 코드 | 메시지 |
    | :---: | :----------------------- |
    | 1     | 참여가능 |
    | 10    | 광고 참여 완료 or 광고 참여 가능 |
    | 20    | 리포팅 완료 |
    | 29    | 리포팅데이터 없음 |
    | 13    | 필수항목이 비었습니다. |
    | 89    | 광고 없음 |    
    | 99    | 오류발생 or 참여불가 |    
    | 100   | 참여중 오류 발생 or 광고 참여 불가 |    
    | 1000  | 유효하지 않은 광고 |    
    | 1100  | 유효하지 않은 매체 |    
    | 2000  | 이미광고에 참여 |    
    | 2300  | 일일 할당량을 넘었습니다. |    
    | 2400  | 광고 정보를 불러 오는 데 실패하였습니다. |    
    | 9999  | 올바른 처리가 아님 |
