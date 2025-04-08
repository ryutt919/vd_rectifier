## 캘리브레이션 결과
- K값 <br>
[603.51030778, 0, 674.89585317] <br>
[0, 603.45260428, 381.01122663] <br>
[0, 0, 1]

- 왜곡계수 <br>
[0.03412314, -0.16458017, 0.0032529, 0.00097189, 0.17881176]

## 왜곡 보정 결과
![disto_rect](https://github.com/user-attachments/assets/16277d7b-00a3-4f9c-9954-8e23bef170c9)
![disto_og](https://github.com/user-attachments/assets/3a290090-8938-483a-991f-5c23f9c2f198)

---
## dist_rectify
🎥 Geometric Distortion Correction Viewer
카메라 보정 파라미터를 사용해 왜곡된 비디오 영상을 실시간으로 보정하고, 원본 영상과 보정된 영상을 토글하며 비교할 수 있는 OpenCV 기반 도구입니다.

📂 파일 설명
video_file: 왜곡된 원본 비디오 경로 (./data/myChess.mp4)

K: 보정된 카메라 내부 파라미터 (Camera Intrinsics Matrix)

dist_coeff: 왜곡 계수 (Distortion Coefficients)

⚙️ 주요 기능
렌즈 왜곡 실시간 보정
카메라 보정 행렬(K)과 왜곡 계수(dist_coeff)를 이용해 OpenCV의 remap 함수를 통해 실시간 보정 적용.

프레임 회전 및 리사이즈
원본 비디오 프레임은 90도 반시계 방향으로 회전되고, 보기 좋게 리사이즈 됩니다.

보정 여부 토글 기능
Tab 키를 통해 보정된 영상과 원본 영상 간 실시간 전환이 가능합니다.

일시정지 및 비교
Space 키를 눌러 재생을 일시정지하고, 정지 상태에서 Tab 키로 보정 전/후 영상 전환이 가능합니다.

루프 재생
비디오가 끝나면 자동으로 처음부터 다시 재생됩니다.

종료
ESC 키로 프로그램을 종료할 수 있습니다.

⌨️ 단축키 안내
키	기능
Space	재생/일시정지
Tab	보정된 영상 ↔ 원본 영상 전환
ESC	프로그램 종료
🔍 기술적 포인트
cv.initUndistortRectifyMap() 함수로 보정용 리맵 맵(map1, map2) 생성

cv.remap()를 이용한 픽셀 단위 위치 재매핑으로 왜곡 보정


--- 
## calibration
🎯 Camera Calibration using Chessboard Pattern
체스보드 패턴이 포함된 비디오를 사용해 카메라의 왜곡 계수를 추정하고, 내부 파라미터(K)를 계산하는 OpenCV 기반 카메라 보정 도구입니다.

🧭 동작 흐름
체스보드 이미지 추출
영상에서 프레임을 하나씩 읽으며 사용자가 선택한 체스보드 패턴 이미지들을 수집합니다.

체스보드 기반 보정 수행
수집된 이미지들을 이용하여 OpenCV의 calibrateCamera() 함수로 카메라 매트릭스와 왜곡 계수를 계산합니다.

🧩 주요 함수 설명
1. select_img_from_video(...)
입력 비디오에서 프레임을 읽고 체스보드가 검출되는 이미지를 수동으로 선택.

Space: 해당 프레임에서 체스보드 검출 시도

Enter: 검출 성공 시 이미지 저장

ESC: 선택 종료

매개변수 주요 내용:

board_pattern: 체스보드 내부 코너 수 (cols, rows)

resize_scale: 프레임 축소 비율

select_all: True이면 자동으로 모든 프레임 저장

2. calib_camera_from_chessboard(...)
수집된 체스보드 이미지들을 이용해 내부 파라미터(K), 왜곡 계수(dist_coeff)를 추정

체스보드의 실제 셀 크기를 사용해 실제 3D 좌표계 구성

cv.calibrateCamera를 통해 보정 수행

## Camera Calibration Results
* The number of selected images = 12
* RMS error = 0.2145
* Camera matrix (K) = 
[[603.5     0.     673.9 ]
 [  0.     602.8   380.2 ]
 [  0.       0.       1. ]]
* Distortion coefficient (k1, k2, p1, p2, k3, ...) = [0.03, -0.16, 0.002, 0.001, 0.17]
🔍 기술 포인트
cv.findChessboardCorners로 코너 검출 및 시각화

사용자 개입 기반 이미지 선택 → 보정 정확도 향상

board_cellsize를 기반으로 실세계 단위 반영

회전 및 리사이징으로 다양한 영상 포맷 대응
