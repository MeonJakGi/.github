# 비었쇼 | Be:show
<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/5162bbed-0af2-4377-9e50-6cedd72e9887" />

## 1) 프로젝트 개요
### 소개
**Be:show(비었쇼)** 는 편의점 매대 이미지를 Computer Vision 기반으로 분석하여 보충 필요, 확인 필요, 발주 필요 상품을 빠르게 파악할 수 있도록 돕는  
**AI 기반 매대 진열 상태 관리 보조 시스템**입니다.

편의점에서는 POS 데이터를 통해 판매량과 장부상 재고를 확인할 수 있지만, 실제 고객이 보는 매대의 결품, 오진열, 앞열 공백 상태는 POS만으로 즉시 파악하기 어렵습니다.

이로 인해 작업자는 매대를 직접 확인한 뒤 POS 재고를 조회하고, 다시 창고에서 상품을 찾아 매대에 진열하는 과정을 반복하게 됩니다.

특히 POS 재고와 실제 재고가 일치하지 않거나, 매대 상태와 창고 재고를 따로 확인해야 하는 경우 보충·발주 판단이 작업자 경험에 의존하게 되어 대응이 늦어질 수 있습니다.

Be:show는 이러한 반복 확인 업무를 줄이기 위해 매대 상태를 고정 카메라와 CV 모델이 먼저 감지하고, 기준 진열표 및 재고 정보와 결합해 작업자가 바로 실행할 수 있는 보충·확인·발주 리스트를 제공합니다.

### 개발 기간
2026.04.28. ~ 2026.06.04.


### 팀 소개

| <img src="./img/minjeong.jpg" alt="김민정" width="200" height="200">  | <img src="./img/yourim.png" alt="노유림" width="200" height="200"> | <img src="./img/raeyoon.jpg" alt="박래윤" width="200" height="200"> | <img src="./img/dajeong.jpg" alt="최다정" width="200" height="200"> |
|:---:|:---:|:---:|:---:|
| 김민정 | 노유림 | 박래윤 | 최다정 |
| AI | Backend | Frontend | AI |
| [isakacindy](https://github.com/isakacindy) | [yourim01](https://github.com/yourim01) | [prprpray](https://github.com/prprpray) | [da-jeong](https://github.com/da-jeong) |

<br />

## 2) 주요 개발 내용
### 아키텍처 도식도
<img width="1308" height="709" alt="Image" src="https://github.com/user-attachments/assets/25e8b04f-4ceb-40c5-a4a3-2789f9d2689a" />

Be:show는 고정 카메라가 촬영한 매대 이미지를 S3에 저장하고, AI 서버가 이미지를 분석한 뒤 결과를 DB에 저장하여 대시보드에 제공하는 구조로 동작합니다.

### 처리 흐름 요약

#### 1. 이미지 업로드  
`Camera → Backend → S3`  
고정 카메라가 Presigned URL을 받아 매대 이미지를 S3에 업로드합니다.

#### 2. AI 분석 요청  
`Backend → AI Server`  
백엔드 서버가 업로드된 이미지 정보를 AI 서버에 전달하고 분석을 요청합니다.

#### 3. 분석 및 저장  
`AI Server → S3 / DB`  
AI 서버가 이미지를 로드하고, 슬롯·진열표·재고 정보를 조회한 뒤 분석 결과를 DB에 저장합니다.

#### 4. 결과 조회  
`Dashboard → Backend → DB / S3`  
대시보드가 분석 결과와 이미지 URL을 받아 선반 상태와 작업 리스트를 표시합니다.

### ERD
<img width="3275" height="1494" alt="Image" src="https://github.com/user-attachments/assets/bbf2657e-7aab-4243-bd2d-8aa3502bad26" />

### 기술 스택
#### AI
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![YOLO](https://img.shields.io/badge/YOLO-111F68?style=for-the-badge&logo=yolo&logoColor=white)
![OpenCV](https://img.shields.io/badge/opencv-%23white.svg?style=for-the-badge&logo=opencv&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C.svg?style=for-the-badge&logo=pytorch&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243.svg?style=for-the-badge&logo=numpy&logoColor=white)

#### FE
![React](https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB)
![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/vite-%23646CFF.svg?style=for-the-badge&logo=vite&logoColor=white)
![CSS](https://img.shields.io/badge/css-%23663399.svg?style=for-the-badge&logo=css&logoColor=white)

#### BE
![Spring](https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-005571.svg?style=for-the-badge&logo=fastapi)
![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white)

#### Infra / DevOps
![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Amazon S3](https://img.shields.io/badge/Amazon%20S3-FF9900?style=for-the-badge&logo=amazons3&logoColor=white)
![Amazon RDS](https://img.shields.io/badge/Amazon%20RDS-FF9900?style=for-the-badge&logo=amazonrds&logoColor=white)
![Docker](https://img.shields.io/badge/docker-2496ED.svg?style=for-the-badge&logo=docker&logoColor=white)
![NVIDIA](https://img.shields.io/badge/NVIDIA-76B900.svg?style=for-the-badge&logo=nvidia&logoColor=white)
![Nginx](https://img.shields.io/badge/nginx-009639.svg?style=for-the-badge&logo=nginx&logoColor=white)
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)

<br />

## 3) 서비스 소개
### 화면
<table>
  <thead>
    <tr>
      <th width="12%">화면</th>
      <th width="55%">이미지</th>
      <th width="33%">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>선반 모니터링</td>
      <td>
        <img width="100%" alt="선반 모니터링" src="https://github.com/MeonJakGi/.github/blob/main/profile/img/scr-1-1.png" />
      </td>
      <td>
        AI가 분석한 매대 이미지를 기반으로<br>
        현재 선반의 진열 상태를 확인합니다.<br><br>
        정상, 보충 필요, 확인 필요 수량을 요약하고,<br>
        bbox로 문제 상품 위치를 시각화합니다.
      </td>
    </tr>
    <tr>
      <td>보충 필요<br>리스트</td>
      <td>
        <img width="100%" alt="보충 필요 리스트" src="https://github.com/MeonJakGi/.github/blob/main/profile/img/scr-1-2.png" />
      </td>
      <td>
        매대에서 즉시 처리해야 하는<br>
        보충 필요 및 확인 필요 상품을 제공합니다.<br><br>
        상품명, 상태, 위치, 탐지 시각을 확인하고<br>
        보충 완료 또는 확인 완료 처리를 할 수 있습니다.
      </td>
    </tr>
    <tr>
      <td>발주 필요<br>리스트</td>
      <td>
        <img width="100%" alt="발주 필요 리스트" src="https://github.com/MeonJakGi/.github/blob/main/profile/img/scr-2.png" />
      </td>
      <td>
        창고 재고가 부족하거나<br>
        재주문 기준점에 도달한 상품을<br>
        별도로 제공합니다.<br><br>
        재고 부족 상품과 발주 검토가 필요한 상품을<br>
        빠르게 확인할 수 있습니다.
      </td>
    </tr>
    <tr>
      <td>상세 모달</td>
      <td>
        <img width="100%" alt="상세 모달" src="https://github.com/MeonJakGi/.github/blob/main/profile/img/scr-1_modal.png" />
      </td>
      <td>
        선택한 상품의 탐지 결과와<br>
        판단 근거를 상세히 확인합니다.<br><br>
        선반, Slot, 현재 재고, ROP,<br>
        상태 reason을 함께 제공합니다.
      </td>
    </tr>
    <tr>
      <td>긴급 알림 패널</td>
      <td>
        <img width="100%" alt="긴급 알림 패널" src="https://github.com/MeonJakGi/.github/blob/main/profile/img/scr-opt.png" />
      </td>
      <td>
        즉시 확인이 필요한 작업을<br>
        알림으로 제공합니다.<br><br>
        SKU 완전 부재, 오진열 및 Slot 이탈 상황을<br>
        우선 안내합니다.
      </td>
    </tr>
  </tbody>
</table>

### 시연영상
> 시연 영상은 준비 중입니다.

<br />

## 4) 핵심 기능
### 매대 상태 감지
고정 카메라로 촬영된 매대 이미지를 기반으로 상품의 위치와 클래스를 탐지합니다.  
탐지 결과는 상품명, bbox, confidence 정보로 저장되며 이후 Slot 매핑과 상태 판정에 활용됩니다.

### Slot 매핑
탐지된 상품 bbox를 기준으로 상품이 어느 선반, 어느 Slot에 위치하는지 매핑합니다.  
이를 통해 기준 진열표와 실제 진열 상태를 비교할 수 있습니다.

### AI 상태 판정
탐지 결과를 기준 진열표, 앞열 수량, 창고 재고 정보와 결합하여 각 Slot의 상태를 작업자가 바로 이해할 수 있는 상태로 분류합니다.

- **정상** : 기준 SKU가 지정된 Slot에 있고, 앞열 최소 진열 수량 이상으로 탐지된 상태
- **보충 필요** : 앞열 최소 진열 수량보다 부족하지만 창고 재고로 보충 가능한 상태
- **확인 필요** : 상품이 지정된 Slot을 벗어나 진열된 상태
- **보충 불가** : 앞열 최소 진열 수량보다 부족하지만 창고 재고로 보충하기 어려운 상태

### 보충 필요 리스트 제공
보충 필요 리스트는 작업자가 매대에서 즉시 확인하거나 처리해야 하는 항목을 제공합니다.

- **보충 필요** : 앞열 최소 진열 수량보다 부족하고, 창고 재고로 보충 가능한 상품
- **확인 필요** : 지정된 Slot을 벗어나 진열되어 작업자 확인이 필요한 상품
- 상품명, Slot 위치, 상태, 현재 진열 수량, 판단 사유 제공
- 보충 완료 또는 확인 완료 처리 가능

### 발주 필요 리스트 제공
발주 필요 리스트는 단순 매대 보충으로 해결하기 어려운 상품을 별도로 제공합니다.

- 전체 재고가 재주문 기준점인 ROP에 도달한 상품
- 상품명, 현재 재고, ROP, 판단 사유 제공
- 발주 완료 처리 가능

### 긴급 알림 제공
긴급 알림은 단순 보충보다 작업자 확인이 우선 필요한 상황을 제공합니다.

- 기준 SKU가 매대에서 완전히 탐지되지 않은 경우
- 상품이 지정된 Slot을 벗어나 오진열된 경우

<br />

## 5) AI 모델 개발
### 합성 데이터 생성
실제 편의점 매대 환경을 가정하여  상품 이미지와 매대 배경을 합성한 학습 데이터를 구축했습니다.
정상 진열뿐 아니라 결품, 오진열, 조도 변화 등  실제 운영 중 발생할 수 있는 문제 상황을 함께 반영했습니다.

| 시나리오 | 설명 |
| --- | --- |
| S0 | 정상 진열 |
| S1 | 앞줄 일부 결손 |
| S2 | 앞줄 전체 공백 |
| S3 | 열 단위 공백 |
| S4 | SKU 완전 부재 |
| S5 | 오진열 |
| S6 | 복합 상황 |
| S7 | 조도 변화 |

### 모델 학습
단품 상품 이미지에 최적화된 기존 모델을 전체 매대 이미지 환경에 맞게 추가 학습했습니다.
상품이 작고 밀집되어 있는 매대 환경에서도 탐지할 수 있도록 시나리오 기반 합성 데이터를 활용했습니다.

### 최종 성능
| 항목 | 값 |
| --- | --- |
| Model | YOLO 기반 상품 탐지 모델 |
| mAP50 | 0.9950 |
| mAP50-95 | 0.9865 |
| Inference Setting | conf 0.25 / IoU 0.55 / imgsz 1280 |

※ 해당 성능은 시나리오 기반 합성 데이터 검증셋 기준입니다.

<br />

## 6) 기대 효과
### 매대 상태 가시화 및 반복 확인 업무 감소
POS 데이터만으로는 확인하기 어려운 고객 시점의 매대 상태를 이미지 기반으로 확인할 수 있습니다.  
상품이 실제로 진열되어 있는지, 앞열이 비어 있는지, 지정된 위치를 벗어났는지 등을 데이터로 기록하여 작업자가 매대를 직접 확인하고 POS·창고 재고를 반복 조회하는 과정을 줄일 수 있습니다.

### 작업 우선순위 분리
Be:show는 매대에서 바로 처리할 수 있는 작업과 발주 검토가 필요한 작업을 분리합니다.

- **보충 필요 리스트** : 매장 작업자가 즉시 처리할 수 있는 매대 보충·확인 작업
- **발주 필요 리스트** : 점장 또는 담당자가 검토해야 하는 재고 부족·발주 작업
- **긴급 알림** : SKU 완전 부재, 오진열 등 즉시 확인이 필요한 예외 상황

이를 통해 작업자는 전체 매대를 반복적으로 확인하지 않고, 우선순위가 높은 상품과 위치를 중심으로 작업할 수 있습니다.

### 재고 대응 속도 향상
매대 결품, 앞열 공백, 오진열 상황을 빠르게 감지하여 상품 보충과 확인 작업의 대응 속도를 높일 수 있습니다.

특히 고객이 보는 매대 상태를 기준으로 문제 상품을 파악하기 때문에 POS 재고만으로는 발견하기 어려운 진열 공백이나 위치 이탈 문제를 보완할 수 있습니다.

### 운영 데이터 축적

분석 결과는 상품별 결품, 오진열, 보충 필요, 발주 필요 이력으로 저장될 수 있습니다.  
이를 통해 반복적으로 문제가 발생하는 상품이나 Slot을 파악하고, 향후 진열 위치 조정, 작업 동선 개선, 발주 기준 검토에 활용할 수 있습니다.

### 서비스 안정성을 고려한 구조 설계

AI 서버와 백엔드 서버를 분리하여 상품 탐지와 상태 판정 로직이 일반 서비스 API와 독립적으로 동작하도록 구성했습니다.
이를 통해 모델 추론 과정에서 부하가 발생하더라도 대시보드 조회, 재고 데이터 관리, 사용자 작업 흐름을 분리하여 운영할 수 있는 구조를 마련했습니다.

<br />

## 7) 향후 확장 계획
### 판매 데이터 기반 재고 운영 고도화
향후 POS 판매 로그, 행사 상품 정보, 시간대별 판매량을 연동하면 현재 재고 부족 여부뿐 아니라 상품별 판매 흐름을 반영한 재고 관리로 확장할 수 있습니다.

예를 들어 잘 팔리는 상품이나 행사 상품은 보충 우선순위를 높이고, 판매 속도가 빠른 상품은 발주 기준을 더 민감하게 설정할 수 있습니다.

### 동적 진열표 및 행사 매대 대응
MVP에서는 기준 진열표와 Slot 구성이 고정되어 있다는 가정으로 구현했습니다.  
향후에는 점장 또는 관리자가 대시보드에서 기준 진열표를 직접 수정하고, 행사 상품·인기 상품·시즌 상품을 별도로 관리할 수 있도록 확장할 수 있습니다.

이를 통해 고정 매대뿐 아니라 행사 매대, 시즌 매대, 점포별 커스텀 진열표에도 대응할 수 있습니다.

### Lot, 입고일자, 소비기한 관리
상품의 Lot, 입고일자, 소비기한 정보를 함께 관리하면 단순 매대 보충을 넘어 폐기 대상 상품 추적과 선입선출 관리로 확장할 수 있습니다.

이를 통해 소비기한 임박 상품을 우선 확인하고, 폐기 손실을 줄이는 재고 회전 관리까지 지원할 수 있습니다.

### 적정 재고 및 안전재고 관리
현재 발주 필요 리스트는 전체 재고와 ROP 기준을 중심으로 판단합니다.  
향후에는 안전재고, 리드타임, 판매 속도, 권장 발주 수량을 함께 고려하여 상품별 적정 재고 수준을 관리하는 방향으로 확장할 수 있습니다.

이를 통해 단순히 재고가 부족한 상품을 알려주는 것을 넘어, 언제 얼마나 발주해야 하는지 제안하는 재고 운영 보조 시스템으로 발전시킬 수 있습니다.

### 발주 요청 기능 확장
현재는 발주가 필요한 상품을 리스트로 제공하고 발주 완료 상태를 관리하는 수준이지만, 향후에는 발주 필요 리스트에서 직접 발주 요청까지 생성할 수 있도록 확장할 수 있습니다.

예를 들어 전체 재고가 ROP 이하인 상품에 대해 권장 발주 수량을 제안하고, 점장 또는 담당자가 수량을 확인한 뒤 발주 요청을 생성하는 방식입니다.

추후 POS, ERP, 구매 시스템 또는 외부 발주 API와 연동하면 발주 필요 감지부터 발주 요청, 승인, 완료 이력 관리까지 이어지는 재고 운영 흐름으로 고도화할 수 있습니다.

### 권한별 작업 화면 분리
실제 매장 운영에서는 사용자 역할에 따라 필요한 정보가 다릅니다.

- **매장 작업자** : 보충 필요 리스트, 확인 필요 리스트 중심
- **점장** : 발주 필요 리스트, 재고 부족 상품, 반복 문제 상품 중심
- **구매 담당자** : 발주 대상 상품, 안전재고, 판매 추이 중심

향후에는 사용자 권한에 따라 화면과 작업 리스트를 분리하여 각 담당자가 필요한 작업만 확인할 수 있도록 개선할 수 있습니다.

### 다양한 현업 환경으로 확장
Be:show의 핵심 구조는 이미지를 통해 현장 상태를 데이터화하고, 기준 정보와 비교하여 작업 리스트로 전환하는 방식입니다.

따라서 편의점 매대뿐 아니라 제조 현장의 자재 적치 상태, 창고 재고 모니터링, 물류 피킹 구역, 설비 주변 상태 점검 등 사람이 직접 확인해야 했던 다양한 현업 환경으로 확장할 수 있습니다.

<br />

## 8) 한계 및 보완점

비었쇼는 현재 합성 데이터와 제한된 매대 환경을 중심으로 구현되었습니다.  
실제 운영 적용을 위해서는 실매장 데이터 확대, 예외 상황 보완, 판매 데이터 연동이 필요합니다.

### 데이터 및 모델 한계

합성 데이터 중심으로 학습되어 실제 매장별 조명, 카메라 각도, 선반 구조, 상품 가림, 반사 등의 차이를 충분히 반영하지 못했습니다.

또한 유사 패키지, 후열 상품 가림, 상품 겹침 상황에서는 오탐·미탐이 발생할 수 있습니다.  
향후 실제 매장 이미지와 실패 케이스를 수집하고, 오탐·미탐 사례를 유형별로 태깅하여 데이터셋을 보강할 필요가 있습니다.

### 트러블슈팅 기반 개선 필요

실제 운영 환경에서는 높은 성능 지표보다 탐지가 실패했을 때 원인을 분석하고 예외 상황에 대응하는 과정이 중요합니다.

향후에는 탐지 실패 원인을 정리하고, 시나리오 기반 합성 데이터와 실제 매장 데이터를 함께 보강하여 모델의 현장 대응력을 높일 수 있습니다.

### 발주 판단 고도화 필요

현재 발주 필요 판단은 재고 수량과 ROP 기준에 의존합니다.  

추후 POS 판매 추이, 행사 정보, 계절성, 리드타임을 결합하면 수요예측 기반 발주 추천으로 확장할 수 있습니다.

### 운영 적용 범위 확대 필요

MVP는 일부 선반과 핵심 SKU 중심으로 검증되었습니다.  
향후 SKU와 카테고리 범위를 확대하고, 점포별 진열표 변경이나 다점포 운영 대시보드까지 고도화할 수 있습니다.

<br />

## 9) 프로젝트 의의

Be:show는 POS 데이터만으로는 확인하기 어려운 고객 시점의 매대 진열 상태를 Computer Vision 기반으로 데이터화한 매대 관리 보조 시스템입니다.

이 프로젝트의 핵심은 단순히 상품을 탐지하는 데 그치지 않고, 탐지 결과를 기준 진열표, Slot 정보, 재고 정보와 결합하여 작업자가 바로 실행할 수 있는 보충, 확인, 발주 판단으로 연결했다는 점입니다.

특히 매대 이미지를 분석하는 AI 서버와 서비스 운영을 담당하는 백엔드 서버를 분리하여 모델 추론, 결과 저장, 대시보드 조회가 독립적으로 동작할 수 있는 구조를 설계했습니다.  
이를 통해 AI 모델을 실제 서비스 흐름 안에 연결하고, 분석 결과가 화면과 작업 리스트로 이어지는 전체 파이프라인을 구현했습니다.

또한 합성 데이터를 활용하여 정상 진열뿐 아니라 앞열 공백, SKU 완전 부재, 오진열, 조도 변화 등 현장에서 발생할 수 있는 다양한 문제 상황을 시나리오로 정의하고 학습 데이터에 반영했습니다.  
이는 단순히 모델 성능을 높이는 것보다, 현장에서 어떤 문제가 발생할 수 있고 이를 어떻게 시스템적으로 대응할지 고민했다는 점에서 의미가 있습니다.

Be:show는 편의점 매대 관리라는 구체적인 문제에서 출발했지만, 이미지 기반 현장 상태 인식, 기준 정보와의 비교, 작업 리스트 생성이라는 구조를 통해 재고 모니터링, 적정 재고 관리, 폐기 관리, 권한별 작업 관리 등 다양한 비즈니스 업무로 확장될 수 있는 가능성을 확인했습니다.

결과적으로 본 프로젝트는 AI 모델 개발뿐 아니라 데이터 생성, 모델 추론, 서버 연동, DB 저장, 대시보드 시각화, 운영 시나리오 설계까지 포함한 하나의 현업형 AI 서비스 개발 과정을 경험했다는 점에 의의가 있습니다.
