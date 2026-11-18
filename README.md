# Outlier PCA의 R 구현

Witten(2013)의 *Penalized unsupervised learning with outliers*에서 제안한 Outlier PCA(OPCA)를 R로 구현하고, 모의실험과 실제 다변량 자료에 적용한 코드입니다. 한국외국어대학교 통계학과 학사학위논문 「이상치가 존재하는 데이터에서의 주성분분석: Outlier PCA의 구현 및 분석」에 사용되었습니다.

## 파일 구성

```
outlier-pca-r/
├── README.md
├── OPCA_middle.Rmd      # 전체 구현 및 분석 코드
└── data/
    ├── track_m.csv      # 국가별 남자 육상 기록
    └── track_w.csv      # 국가별 여자 육상 기록
```

## Rmd 구성과 논문의 대응

| Rmd 섹션 | 내용 | 논문 |
|---|---|---|
| 1. Outlier PCA 알고리즘 | `outlier_pca` (Algorithm 3) | 3.1, 3.2절 |
| 2. Figure 4 | 2차원 예제 | 4.1절, 그림 4.1 |
| 3. 모의실험 데이터 생성 | `generate_pca_data` | 3.4절 |
| 4. 방법별 구현 | PCA, OPCA(λ 선택), OSPCA, PCAOS, VSA, OER | 3.2, 3.3, 3.6절 |
| 5. 모의실험 실행 | 6개 조건 × 50회 반복 | 4.2절 |
| 6. 결과 요약과 표 | 평균(표준오차) 표 | 표 4.1 |
| 7. 실제 다변량 자료 | 육상 기록 PCA/OPCA 비교 | 3.5, 4.4절, 표 4.2~4.4 |

## 실행 환경

- R (4.x 권장)
- RStudio (knit용)
- 필요 패키지: `ggplot2`, `patchwork`

```r
install.packages(c("ggplot2", "patchwork"))
```

그 외 `rmarkdown`, `knitr`는 RStudio가 필요할 때 설치를 안내합니다.

## 실행 방법

1. 저장소를 내려받습니다(Code → Download ZIP 또는 `git clone`).
2. **저장소 폴더 안에서** `OPCA_middle.Rmd`를 RStudio로 엽니다. 데이터를 상대경로(`data/track_m.csv`)로 읽으므로, Rmd와 `data/` 폴더가 같은 위치에 있어야 합니다.
3. **Knit** 버튼(`Cmd/Ctrl + Shift + K`)을 누릅니다.

## 유의사항

- **처음부터 순서대로 실행해야 합니다.** 난수 시드(`set.seed(123)`)가 n = 50 모의실험 청크와 육상 자료 청크에서 설정되고, n = 100 조건은 그 뒤로 이어지는 난수 흐름으로 실행됩니다. 청크를 일부만 따로 실행하면 논문과 다른 숫자가 나올 수 있습니다.
- **실행 시간이 깁니다.** 모의실험 300회(6개 조건 × 50회)와 육상 자료 60회(남녀 × 30회) 반복이 포함되어 있어 몇 분에서 수십 분이 걸릴 수 있습니다.
- Rmd 안에 OPCA 구현이 두 가지 있습니다. `outlier_pca`는 2차원 예제와 다변량 예제의 최종 실행에, `opca_fixed_lambda`는 모의실험과 λ 선택(`select_opca_lambda`)에 사용했습니다.

## 자료 출처

`data/`의 육상 기록 자료는 박흥선(2023), 『SAS를 이용한 다변량 자료분석』(제2판), 자유아카데미에 수록된 자료이며, 교재에서는 Johnson and Wichern(2014)을 원출처로 명시하고 있습니다.

## 참고문헌

Witten, D. M. (2013). Penalized unsupervised learning with outliers. *Statistics and Its Interface*, 6(2), 211–221.
