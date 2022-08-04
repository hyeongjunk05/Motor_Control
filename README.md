# Motor_Control
Motor_Control
1. https://gitlab.com/clmnlab/labs/-/wikis/Research-Projects/IN
https://github.com/clmnlab/labs/tree/master/interference-project 이거 서버 내, 내 것에 다운 받아둚


논문에 언급된 총 피실험자 숫자
-> 18 female


server IN 경로에 있는 총 피실험자 데이터 갯수의 숫자. = 44 개.

1. https://gitlab.com/clmnlab/labs/-/wikis/Research-Projects/IN

IN

[IN] Interference project

작성자: 신윤하
작성일: 2020-05-07

개요
실험 정보
2017.12.19 ~ 2018.06.14

실험 진행

장비: MR compatible tablet

실험 디자인
논문 참조

데이터
Preprocessed data
xxxxxx /clmnlab/IN/AFNI_data/preprocessed_data/

000xxx script: /clmnlab/IN/scripts/preprocessing/step*.sh

beta values
2020.05.07 현재 LSS_trialtypes_pb04 를 사용

xxxxxx processed file 위치: /clmnlab/IN/MVPA/LSS_trialtypes_pb04(이게 비어있음 + LSS_* 다 비어있음)/02_deconvolve/

xxxxxx beta file 위치: /clmnlab/IN/MVPA/LSS_trialtypes_pb04(이게 비어있음 + LSS_* 다 비어있음)/03_data/

xxxxxx script: /clmnlab/IN/MVPA/LSS_trialtypes_pb04(이게 비어있음 + LSS_* 다 비어있음)/1_deconvolve_20190225.sh

관련 논문: The impact of study design on pattern estimation for single-trial multivariate pattern analysis

ROI masks
000000 /clmnlab/IN/new_label/04_ROIs/*.nii.gz

000000점검중 Visualization 코드: /clmnlab/IN/new_label/00_scripts/20200402_Visualization_definition-of-rois-in-surface.ipynb

분석
Behavior data
xxxxxx /clmnlab/IN/new_label/01_behav(이게 비어있음)/

Column 설명
run
behavior data 의 run
order
behavior data 의 run 별 trial 순서
group
Run 1, 2 의 경우: control 은 0, mixed block 은 1 로 태깅
Run 3, 4, 5 의 경우: 한 target 을 공유하는 12 trial 을 한 블록으로 정의하여 ij - Run i 의 j 번째 블록으로 태깅
actual_dgree
각 trial 별 hand degree.
color_type
target 의 conceptual color class. {1, 2, 3}. 2 = control.
rotate_type
각 trial 별로 주어진 rotational perturbation 타입. {-30, 0, 30} 중 하나.
target_position
각 trial 별로 화면에 보여진 target 의 위치. {middle, high, low}.
answer
Task type 에 따른 goal direction. {mid, up, down}.
degree_type
실제 subject 가 수행한 direction. {mid, up, down, none}.
actual_degree 기준으로 4515 = up; 15-15 = mid; -15~-45 = down; else = none.
valid
degree_type 과 answer 가 맞았는지 여부. 이후 GLM, MVPA 분석에서 valid 한 trial 만 선택하여 사용함
GLM analysis

xxxxxx regressor 파일 위치: /clmnlab/IN/new_label/02_GLM/regressors(이게 비어있음)/

script
000000 /clmnlab/IN/new_label/00_scripts/20200224_GLM_deconvolve-stats-seprun.sh 로 deconvolve 를 각 run 별로 2-class, on-off stat 값을 뽑은 다음

![image](https://user-images.githubusercontent.com/47169500/182741922-baee0e14-1ba3-4502-8e31-9c7f084c7f85.png)

.sh 돌리려는데, 여기서 AFNI_data/ 이후의 경로들 게 존재하지 않음..

000000 /clmnlab/IN/new_label/00_scripts/20200224_GLM_2-class_group-analysis-seprun.sh 로 run 별 2-class group analysis

이거 돌리면 

![image](https://user-images.githubusercontent.com/47169500/182743277-16b2e760-e6cf-47c4-bf42-42a249b66d34.png)

이렇게 이미 존재한다고 나옴

000000 /clmnlab/IN/new_label/00_scripts/20200225_GLM_on-off_group-analysis-seprun.sh 로 run 별 on-off group analysis

이거 돌리면

![image](https://user-images.githubusercontent.com/47169500/182743761-02d8da7a-e3bd-4e11-be71-5cfbec345752.png)

이렇게 이미 존재한다고 나옴

000000 individual stats files: /clmnlab/IN/new_label/02_GLM/stats_seprun/IN??/stats.IN??.r0?.nii.gz

이거는 총 stats_seprun/IN?? -> 에서 ??이 총 33개 유효 피실험자 데이터 존재함. 정확.

000000 group stats files: /clmnlab/IN/new_label/02_GLM/stats_seprun/group/

위에서들 봤듯이 이미 group/2-class & on-off 결과폴더들 존재.

Conjunction analysis visualization
000000 data: /clmnlab/IN/new_label/05_Visualization/conjunction/

존재. .HEAD file 들하고, nii.gz 파일들 존재.

000000 color scheme: /clmnlab/IN/new_label/00_scripts/IN_scheme.rgb

.rgb 파일 존재.

fsleyes 에서 import 하여 사용 가능

000000 code: /clmnlab/IN/new_label/00_scripts/20200414_Visualization_conjunction-analysis-results-in-surface.ipynb

첫번 쨰 cell에는 확실히 문제가 있는 코드. import 하는 library 중에 local_modules 라는 게 존재하지 않음

각 run 별 corrected p < 0.05 thresholded cluster mask image 를 가져온 다음
conjunction analysis 를 수행한 뒤에
이를 맞는 color scheme 으로
surface 에 volume 파일 올려서 그림 그림
duct taping 으로 nilearn.plotting.plot_surf 함수를 수정하여 사용함

Conjunction analysis anatomical region description

111000 code: /clmnlab/IN/new_label/00_scripts/20200416_Results_Cluster-region-description.ipynb

다 잘 돌아가는데, 맨 마지막 Cell에서 nii.gz 파일들에 대하여 자꾸 permission Error 뜸.

Searchlight analysis

script
xxxxxx 2-class individual: /clmnlab/IN/new_label/00_scripts/20200228_MVPA_searchlight-analysis_2-class.py
xxxxxx on-off individual: /clmnlab/IN/new_label/00_scripts/20200228_MVPA_searchlight-analysis_on-off.py
000000 group analysis: /clmnlab/IN/new_label/00_scripts/20200316_MVPA_searchlight-group-analysis.sh

![image](https://user-images.githubusercontent.com/47169500/182753983-46974727-82ca-48b9-bfce-e3c520659fe9.png)

실행하면 이렇게 LSS_beta 아래에 파일들 없어서 error 뜸

000000 individual accuracy map: /clmnlab/IN/new_label/03_MVPA/searchlight/2-class/ , on-off/

두 경로 모두에 .nii.gz 파일들 존재함.

000000 accuracy group stat map: /clmnlab/IN/new_label/03_MVPA/searchlight/2-class/group/, on-off/group/

두 경로 모두에 .BRIK.gz , .nii.gz , .HEAD , .1D(무슨 table 같은 내용들 있음) 파일들 존재함.


Searchlight analysis visualization

000000 data(이건 그냥 nii.gz 랑 .rgb 파일들임): /clmnlab/IN/new_label/05_Visualization/searchlight/`

000000 code: /clmnlab/IN/new_label/00_scripts/20200416_Visualization_searchlight-analysis-results-in-surface.ipynb

clmnlab_libs.mvpa_toolkits 에서 mvpa_toolkits.py 들어가면 어떤 library 없다고 해서 다른 데서 찾아서 해주니 첫번째 cell에서 에러 사라짐.

![image](https://user-images.githubusercontent.com/47169500/182758439-bd612317-b496-4abe-8b92-8829f9f7896d.png)

_crop_colorbar 이라는 거 import Error 계속 떠서 아래 링크에서 찾아서 복붙해서 library에 넣었더니 돌아감.

https://github.com/mne-tools/mne-python/blob/main/mne/fixes.py

![image](https://user-images.githubusercontent.com/47169500/182758344-16a8c3f9-2b8c-4174-b9a3-642670ae381e.png)

20200417_colormap.png 있는 부분 코드에서 PermissionError 발생 하는 거 빼고는 다 잘 돌아감.


Searchlight analysis anatomical region description
000000 code: /clmnlab/IN/new_label/00_scripts/20200420_Results_Cluster-region-description_searchlight.ipynb

ROI-based MVPA
000000 code & visualization: /clmnlab/IN/new_label/00_scripts/20200224_MVPA_ROI-based-MVPA-analysis.ipynb(MVPA-analysis(_old_dataset이 존재함).ipynb
)
data
000000 /clmnlab/IN/new_label/00_scripts/20200224_MVPA_results.pkl
