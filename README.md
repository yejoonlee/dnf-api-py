<h1 align="center">던전 앤 파이터 API</h1>
<p align="center">
 <a href="https://github.com/yejoonlee/dnf-api-py/blob/main/LICENSE">
    <img alt="code style: prettier" src="https://img.shields.io/github/license/mashape/apistatus.svg?style=for-the-badge">
  </a>
</p>
<p align="center">
Python으로 사용할 수 있는 던전앤파이터 API입니다.<br>
API 키는 <a href="https://developers.neople.co.kr/main" target="_blank">developers.neople.co.kr</a>에서 발급 받으 실 수 있습니다.<br>
</p>

---

### 설치

```bash
pip install dnfapipy
```

### 사용법

dnfApiPy를 import하여 apiModule 클래스를 생성하여 사용하실 수 있습니다.

```python
from dnfApiPy import apiModule

dnfApi = apiModule({apiKey})

# 아래에 소스코드를 작성합니다.
```

---


# 서버정보

던전앤 파이터 서버 정보를 불러옵니다.  
  
호출되는 데이터의 상세 정보는 [이곳](https://developers.neople.co.kr/contents/guide/pages/all#%EC%84%9C%EB%B2%84)을 참고해주세요.
  
  
```Python
serverInfo = dnfApi.serverInfo()
```
  
  
데이터 형태는 다음과 같이 dict 타입으로 리턴됩니다.
![image](https://user-images.githubusercontent.com/35551019/167790408-18f93340-e905-4341-b508-685bc28bb781.png)

---

# 캐릭터

던전 앤 파이터 게임내 캐릭터에 관련된 API 입니다.

## 캐릭터 검색

캐릭터를 '서버 아이디'와 '캐릭터 이름(닉네임)'으로 검색하여 받아옵니다.  
optionalInput을 입력하면 더 상세한 조건으로 검색이 가능합니다.
  
  
```Python
# optionalInput =
# {
#   jobId:str
#   jobGrowId:str
#   limit:int
#   wordType:str
# }

characterSearch = dnfApi.characterSearch(serverId = {서버 아이디}
                                         , characterName = {캐릭터 이름}
                                         , optionalInput = optionalInput)
```
  
  
데이터 호출 예시
![image](https://user-images.githubusercontent.com/35551019/167795933-c03f0349-030a-496e-8f69-a2664feae44b.png)



## 캐릭터 기본 정보

'서버 아이디'와 '캐릭터 아이디'로 검색하여 캐릭터에 대한 기본적인 정보를 받아옵니다.  
'캐릭터 아이디'는 '캐릭터 이름(닉네임)'이 아닌 [캐릭터 검색](#캐릭터-검색) 결과에서 얻을 수 있는 정보입니다.
  
  
```Python
characterInfo = dnfApi.characterInfo(serverId={서버 아이디}
                                    , characterId={캐릭터 아이디})
```
  
  
데이터 호출 예시
![image](https://user-images.githubusercontent.com/35551019/167796270-7a03aa2e-58e8-4696-b84e-e73894f9e782.png)


## 타임라인 정보

'서버 아이디'와 '서버 아이디'로 타임라인 정보를 받아옵니다.  
'캐릭터 아이디'는 '캐릭터 이름(닉네임)'이 아닌 [캐릭터 검색](#캐릭터-검색) 결과에서 얻을 수 있는 정보입니다.  
optionalInput을 입력하면 더 상세한 조건으로 검색이 가능합니다.  
기간은 최대 90일입니다.
  
타임라인 코드에 대한 정보는 [이곳](https://developers.neople.co.kr/contents/guide/pages/all#%ED%83%80%EC%9E%84%EB%9D%BC%EC%9D%B8-%EC%BD%94%EB%93%9C)에서 확인하실 수 있습니다.
  
  
```Python
# optionalInput
# {
#   startDate:str
#   endDate:str
#   code:str
#   next:str
# }

characterTimelineInfo = dnfApi.characterTimelineInfo(serverId={서버 아이디}
                                                     , characterId={캐릭터 아이디}
                                                     , optionalInput=optionalInput)
```
  
  
데이터 호출 예시
![image](https://user-images.githubusercontent.com/35551019/167797313-e5691054-a076-4aa2-89db-9adcd921a760.png)
  
  
## 능력치 정보

'캐릭터 아이디'와 '서버 아이디'로 캐릭터의 능력치 정보를 받아옵니다.  
'캐릭터 아이디'는 '캐릭터 이름(닉네임)'이 아닌 [캐릭터 검색](#캐릭터-검색) 결과에서 얻을 수 있는 정보입니다. 
  
  
```Python
characterStatusInfo = dnfApi.characterStatusInfo(serverId={서버 아이디}
                                                 , characterId={캐릭터 아이디})
```

---

# 캐릭터 장비

## 캐릭터 '장착 장비', '장착 아바타', '장착 크리쳐', '장착 휘장', '장착 탈리스만' 조회
  
'서버 아이디'와 '캐릭터 아이디', 'keyword'로 캐릭터의 장비 정보를 받아옵니다.  
'캐릭터 아이디'는 '캐릭터 이름(닉네임)'이 아닌 [캐릭터 검색](#캐릭터-검색) 결과에서 얻을 수 있는 정보입니다. 
  
  
```Python
# '장착 장비' 조회 시 keyword_index = 0
# '장착 아바타' 조회 시 keyword_index = 1
# '장착 크리쳐' 조회 시 keyword_index = 2
# '장착 휘장' 조회 시 keyword_index = 3
# '장착 탈리스만' 조회 시 keyword_index = 4

equip_keywords = ['equipment', 'avatar', 'creature', 'flag', 'talisman']

characterEquip_equipment = dnfApi.characterEquip(serverId={서버 아이디}
                                               , characterId={캐릭터 아이디}
                                               , keyword=equip_keywords[{keyword_index}])
```
  
---

# 스킬 스타일 및 강화 장비

## 캐릭터 '스킬 스타일', '버프 스킬 강화 장착 장비', '버프 스킬 강화 장착 아바타', '버프 스킬 강화 장착 크리쳐' 조회
  
'서버 아이디'와 '캐릭터 아이디', 'keyword'로 캐릭터의  정보를 받아옵니다.  
'캐릭터 아이디'는 '캐릭터 이름(닉네임)'이 아닌 [캐릭터 검색](#캐릭터-검색) 결과에서 얻을 수 있는 정보입니다. 
  
  
```Python
# '스킬 스타일' 조회 시 keyword = None

characterSkillStyle = dnfApi.characterSkill(serverId={서버 아이디}
                                            , characterId={캐릭터 아이디})

# '버프 스킬 강화 장착 장비' 조회 시 keyword_index = 0
# '버프 스킬 강화 장착 아바타' 조회 시 keyword_index = 1
# '버프 스킬 강화 장착 크리쳐' 조회 시 keyword_index = 2

skill_keywords = ['equipment', 'avatar', 'creature']

characterSkillStyle = dnfApi.characterSkill(serverId={서버 아이디}
                                            , characterId={캐릭터 아이디}
                                            , keyword=skill_keywords[0])
```

---
