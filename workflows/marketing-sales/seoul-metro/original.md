



# Seoul Metro Skill

Query real-time Seoul Metro information.

## Features

| Feature | Description | Trigger Example (KO) | Trigger Example (EN) |
|---------|-------------|----------------------|----------------------|
| Real-time Arrival | Train arrival times by station | "강남역 도착정보" | "Gangnam station arrivals" |
| Station Search | Line and station code lookup | "강남역 몇호선?" | "What line is Gangnam?" |
| Route Search | Shortest path with time/fare | "신도림에서 서울역" | "Sindorim to Seoul Station" |
| Service Alerts | Delays, incidents, non-stops | "지하철 지연 있어?" | "Any subway delays?" |

## Environment Variables

| Variable | Usage | Provider |
|----------|-------|----------|
| `SEOUL_OPENAPI_KEY` | Arrival info, station search | data.seoul.go.kr |
| `DATA_GO_KR_KEY` | Route search, alerts | data.go.kr |

**How to get API keys:**
1. **SEOUL_OPENAPI_KEY**: Sign up at [data.seoul.go.kr](https://data.seoul.go.kr), go to "My Page" > "API Key Management"
2. **DATA_GO_KR_KEY**: Sign up at [data.go.kr](https://www.data.go.kr), search for the API service, and request access

---

## API Reference

### 1. Real-time Arrival Info

**Endpoint**
```
http://swopenAPI.seoul.go.kr/api/subway/{KEY}/json/realtimeStationArrival/{start}/{end}/{station}
```

**Response Fields**

| Field | Description |
|-------|-------------|
| `subwayId` | Line ID (1002=Line 2, 1077=Sinbundang) |
| `trainLineNm` | Direction (e.g., "성수행 - 역삼방면") |
| `arvlMsg2` | Arrival time (e.g., "4분 20초 후") |
| `arvlMsg3` | Current location |
| `btrainSttus` | Train type (일반/급행) |
| `lstcarAt` | Last train (0=No, 1=Yes) |

---

### 2. Station Search

**Endpoint**
```
http://openapi.seoul.go.kr:8088/{KEY}/json/SearchInfoBySubwayNameService/{start}/{end}/{station}
```

**Response Fields**

| Field | Description |
|-------|-------------|
| `STATION_CD` | Station code |
| `STATION_NM` | Station name |
| `LINE_NUM` | Line name (e.g., "02호선") |
| `FR_CODE` | External station code |

---

### 3. Route Search

**Endpoint**
```
https://apis.data.go.kr/B553766/path/getShtrmPath
```

**Parameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `serviceKey` | Yes | DATA_GO_KR_KEY |
| `dptreStnNm` | Yes | Departure station |
| `arvlStnNm` | Yes | Arrival station |
| `searchDt` | Yes | Datetime (yyyy-MM-dd HH:mm:ss) |
| `dataType` | Yes | JSON |
| `searchType` | No | duration / distance / transfer |

**Response Fields**

| Field | Description |
|-------|-------------|
| `totalDstc` | Total distance (m) |
| `totalreqHr` | Total time (seconds) |
| `totalCardCrg` | Fare (KRW) |
| `paths[].trainno` | Train number |
| `paths[].trainDptreTm` | Departure time |
| `paths[].trainArvlTm` | Arrival time |
| `paths[].trsitYn` | Transfer flag |

---

### 4. Service Alerts

**Endpoint**
```
https://apis.data.go.kr/B553766/ntce/getNtceList
```

**Parameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `serviceKey` | Yes | DATA_GO_KR_KEY |
| `dataType` | Yes | JSON |
| `pageNo` | No | Page number |
| `numOfRows` | No | Results per page |
| `lineNm` | No | Filter by line |

**Response Fields**

| Field | Description |
|-------|-------------|
| `noftTtl` | Alert title |
| `noftCn` | Alert content |
| `noftOcrnDt` | Timestamp |
| `lineNmLst` | Affected line(s) |
| `nonstopYn` | Non-stop flag |
| `xcseSitnBgngDt` | Incident start |
| `xcseSitnEndDt` | Incident end |

---

## Line ID Mapping

| Line | ID | Line | ID |
|------|----|------|----|
| Line 1 | 1001 | Line 6 | 1006 |
| Line 2 | 1002 | Line 7 | 1007 |
| Line 3 | 1003 | Line 8 | 1008 |
| Line 4 | 1004 | Line 9 | 1009 |
| Line 5 | 1005 | Sinbundang | 1077 |
| Gyeongui-Jungang | 1063 | Gyeongchun | 1067 |
| Airport Railroad | 1065 | Suin-Bundang | 1075 |

---

## Station Name Mapping (English → Korean)

주요 역 이름의 영어-한글 매핑 테이블입니다. API 호출 시 영어 입력을 한글로 변환해야 합니다.

### Line 1 (1호선)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Seoul Station | 서울역 | City Hall | 시청 |
| Jonggak | 종각 | Jongno 3-ga | 종로3가 |
| Jongno 5-ga | 종로5가 | Dongdaemun | 동대문 |
| Cheongnyangni | 청량리 | Yongsan | 용산 |
| Noryangjin | 노량진 | Yeongdeungpo | 영등포 |
| Guro | 구로 | Incheon | 인천 |
| Bupyeong | 부평 | Suwon | 수원 |

### Line 2 (2호선)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Gangnam | 강남 | Yeoksam | 역삼 |
| Samseong | 삼성 | Jamsil | 잠실 |
| Sindorim | 신도림 | Hongdae (Hongik Univ.) | 홍대입구 |
| Hapjeong | 합정 | Dangsan | 당산 |
| Yeouido | 여의도 | Konkuk Univ. | 건대입구 |
| Seolleung | 선릉 | Samsung | 삼성 |
| Sports Complex | 종합운동장 | Gangbyeon | 강변 |
| Ttukseom | 뚝섬 | Seongsu | 성수 |
| Wangsimni | 왕십리 | Euljiro 3-ga | 을지로3가 |
| Euljiro 1-ga | 을지로입구 | City Hall | 시청 |
| Chungjeongno | 충정로 | Ewha Womans Univ. | 이대 |
| Sinchon | 신촌 | Sadang | 사당 |
| Nakseongdae | 낙성대 | Seoul Nat'l Univ. | 서울대입구 |
| Guro Digital Complex | 구로디지털단지 | Mullae | 문래 |

### Line 3 (3호선)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Gyeongbokgung | 경복궁 | Anguk | 안국 |
| Jongno 3-ga | 종로3가 | Chungmuro | 충무로 |
| Dongguk Univ. | 동대입구 | Yaksu | 약수 |
| Apgujeong | 압구정 | Sinsa | 신사 |
| Express Bus Terminal | 고속터미널 | Gyodae | 교대 |
| Nambu Bus Terminal | 남부터미널 | Yangjae | 양재 |
| Daehwa | 대화 | Juyeop | 주엽 |

### Line 4 (4호선)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Myeongdong | 명동 | Hoehyeon | 회현 |
| Seoul Station | 서울역 | Sookmyung Women's Univ. | 숙대입구 |
| Dongdaemun History & Culture Park | 동대문역사문화공원 | Hyehwa | 혜화 |
| Hansung Univ. | 한성대입구 | Mia | 미아 |
| Mia Sageori | 미아사거리 | Gireum | 길음 |
| Chongshin Univ. | 총신대입구 | Sadang | 사당 |

### Line 5 (5호선)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Gwanghwamun | 광화문 | Jongno 3-ga | 종로3가 |
| Dongdaemun History & Culture Park | 동대문역사문화공원 | Cheonggu | 청구 |
| Wangsimni | 왕십리 | Haengdang | 행당 |
| Yeouido | 여의도 | Yeouinaru | 여의나루 |
| Mapo | 마포 | Gongdeok | 공덕 |
| Gimpo Airport | 김포공항 | Banghwa | 방화 |

### Line 6 (6호선)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Itaewon | 이태원 | Samgakji | 삼각지 |
| Noksapyeong | 녹사평 | Hangang | 한강진 |
| Sangsu | 상수 | Hapjeong | 합정 |
| World Cup Stadium | 월드컵경기장 | Digital Media City | 디지털미디어시티 |

### Line 7 (7호선)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Gangnam-gu Office | 강남구청 | Cheongdam | 청담 |
| Konkuk Univ. | 건대입구 | Children's Grand Park | 어린이대공원 |
| Junggok | 중곡 | Ttukseom Resort | 뚝섬유원지 |
| Express Bus Terminal | 고속터미널 | Nonhyeon | 논현 |
| Hakdong | 학동 | Bogwang | 보광 |
| Jangam | 장암 | Dobongsan | 도봉산 |

### Line 8 (8호선)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Jamsil | 잠실 | Mongchontoseong | 몽촌토성 |
| Gangdong-gu Office | 강동구청 | Cheonho | 천호 |
| Bokjeong | 복정 | Sanseong | 산성 |
| Moran | 모란 | Amsa | 암사 |

### Line 9 (9호선)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Sinnonhyeon | 신논현 | Express Bus Terminal | 고속터미널 |
| Dongjak | 동작 | Noryangjin | 노량진 |
| Yeouido | 여의도 | National Assembly | 국회의사당 |
| Dangsan | 당산 | Yeomchang | 염창 |
| Gimpo Airport | 김포공항 | Gaehwa | 개화 |
| Olympic Park | 올림픽공원 | Sports Complex | 종합운동장 |

### Sinbundang Line (신분당선)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Gangnam | 강남 | Sinsa | 신사 |
| Yangjae | 양재 | Yangjae Citizen's Forest | 양재시민의숲 |
| Pangyo | 판교 | Jeongja | 정자 |
| Dongcheon | 동천 | Suji District Office | 수지구청 |
| Gwanggyo | 광교 | Gwanggyo Jungang | 광교중앙 |

### Gyeongui-Jungang Line (경의중앙선)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Seoul Station | 서울역 | Hongdae (Hongik Univ.) | 홍대입구 |
| Gongdeok | 공덕 | Hyochang Park | 효창공원앞 |
| Yongsan | 용산 | Oksu | 옥수 |
| Wangsimni | 왕십리 | Cheongnyangni | 청량리 |
| DMC | 디지털미디어시티 | Susaek | 수색 |
| Ilsan | 일산 | Paju | 파주 |

### Airport Railroad (공항철도)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Seoul Station | 서울역 | Gongdeok | 공덕 |
| Hongdae (Hongik Univ.) | 홍대입구 | Digital Media City | 디지털미디어시티 |
| Gimpo Airport | 김포공항 | Incheon Airport T1 | 인천공항1터미널 |
| Incheon Airport T2 | 인천공항2터미널 | Cheongna Int'l City | 청라국제도시 |

### Suin-Bundang Line (수인분당선)
| English | Korean | English | Korean |
|---------|--------|---------|--------|
| Wangsimni | 왕십리 | Seolleung | 선릉 |
| Gangnam-gu Office | 강남구청 | Seonjeongneung | 선정릉 |
| Jeongja | 정자 | Migeum | 미금 |
| Ori | 오리 | Jukjeon | 죽전 |
| Suwon | 수원 | Incheon | 인천 |

---

## Usage Examples

**Real-time Arrival**
```bash
curl "http://swopenAPI.seoul.go.kr/api/subway/${SEOUL_OPENAPI_KEY}/json/realtimeStationArrival/0/10/강남"
```

**Station Search**
```bash
curl "http://openapi.seoul.go.kr:8088/${SEOUL_OPENAPI_KEY}/json/SearchInfoBySubwayNameService/1/10/강남"
```

**Route Search**
```bash
curl -G "https://apis.data.go.kr/B553766/path/getShtrmPath?serviceKey=${DATA_GO_KR_KEY}&dataType=JSON" \
  --data-urlencode "dptreStnNm=신도림" \
  --data-urlencode "arvlStnNm=서울역" \
  --data-urlencode "searchDt=$(date '+%Y-%m-%d %H:%M:%S')"
```

**Service Alerts**
```bash
curl "https://apis.data.go.kr/B553766/ntce/getNtceList?serviceKey=${DATA_GO_KR_KEY}&dataType=JSON&pageNo=1&numOfRows=10"
```

---

## Output Format Guide

### Real-time Arrival

**Korean:**
```
[강남역 도착 정보]

| 호선 | 방향 | 도착 | 위치 | 유형 |
|------|------|------|------|------|
| 2호선 | 성수행 | 3분 | 역삼 | 일반 |
```

**English:**
```
[Gangnam Station Arrivals]

| Line | Direction | Arrival | Location | Type |
|------|-----------|---------|----------|------|
| Line 2 | Seongsu-bound | 3 min | Yeoksam | Regular |
```

### Station Search

**Korean:**
```
[강남역]

| 호선 | 역코드 | 외부코드 |
|------|--------|----------|
| 2호선 | 222 | 0222 |
```

**English:**
```
[Gangnam Station]

| Line | Station Code | External Code |
|------|--------------|---------------|
| Line 2 | 222 | 0222 |
```

### Route Search

**Korean:**
```
[강남 -> 홍대입구]

소요시간: 38분 | 거리: 22.1 km | 요금: 1,650원 | 환승: 1회

1. 09:03 강남 출발 (2호선 성수방면)
2. 09:18 신도림 환승 (2호선 -> 1호선)
3. 09:42 홍대입구 도착
```

**English:**
```
[Gangnam -> Hongdae]

Time: 38 min | Distance: 22.1 km | Fare: 1,650 KRW | Transfers: 1

1. 09:03 Depart Gangnam (Line 2 towards Seongsu)
2. 09:18 Transfer at Sindorim (Line 2 -> Line 1)
3. 09:42 Arrive Hongdae
```

### Service Alerts

**Korean:**
```
[운행 알림]

[1호선] 종로3가역 무정차 (15:00 ~ 15:22)
- 코레일 열차 연기 발생으로 인함

[2호선] 정상 운행
```

**English:**
```
[Service Alerts]

[Line 1] Jongno 3-ga Non-stop (15:00 ~ 15:22)
- Due to smoke from Korail train

[Line 2] Normal operation
```

### Error

**Korean:**
```
오류: 역을 찾을 수 없습니다.
"강남" (역 이름만)으로 검색해 보세요.
```

**English:**
```
Error: Station not found.
Try searching with "Gangnam" (station name only).
```

### API Key Errors

**Korean:**
```
오류: API 인증키가 설정되지 않았습니다.
환경 변수를 설정해주세요: SEOUL_OPENAPI_KEY

발급 안내:
- 서울열린데이터광장: https://data.seoul.go.kr
- 공공데이터포털: https://www.data.go.kr
```

**English:**
```
Error: API key is not configured.
Please set environment variable: SEOUL_OPENAPI_KEY

Get your API key:
- Seoul Open Data Plaza: https://data.seoul.go.kr
- Korea Public Data Portal: https://www.data.go.kr
```

**Korean:**
```
오류: API 인증키가 유효하지 않습니다.
인증키를 확인해주세요.
```

**English:**
```
Error: Invalid API key.
Please verify your API key.
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
