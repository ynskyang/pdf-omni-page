# PDF-Omni 프로젝트 페이지 (Nerfies 스타일)

[nerfies/nerfies.github.io](https://github.com/nerfies/nerfies.github.io) 템플릿 기반의
**PDF-Omni: Poincaré Dual Disk Distortion Field-based Recurrent Update for Omnidirectional Stereo Matching** (ECCV 2026) 프로젝트 페이지입니다.

논문 내용(초록, 방법 설명, Table 1·2·3 수치, 효율성/일반화 결과)이 이미 반영되어 있고,
논문 PDF에서 추출한 Figure 1~5가 `static/images/`에 들어 있습니다.

## 페이지 구성 (FoundationStereo·Marigold·Helvipad 등 8개 레퍼런스 페이지의 공통 패턴 기준)

1. Hero — 제목 / ECCV 2026 배지 / 저자 / 링크 버튼
2. 티저 — 현재 Fig 1(seam 오차 분석), 추후 depth 파노라마 영상 권장
3. Abstract
4. Method — 파이프라인(Fig 2) → PDD field(Fig 3) → DAA+DiGRU(Fig 4) → LEC loss
5. Qualitative Results — Fig 5
6. Quantitative Results — 메인 표(5개 데이터셋), seam 분석 표, 효율성/일반화
7. (주석 처리) Video, OmniProx Dataset 섹션 — 준비되면 주석 해제
8. BibTeX / 푸터

## 영상 (static/videos/, 2026-08-11 생성)

| 파일 | 위치 | 내용 |
|---|---|---|
| `pointcloud.mp4` (5.1MB) | 티저(히어로) | Sunny test 780-930, Ours-ft 360° depth → 컬러 포인트 클라우드 궤도 뷰 |
| `comparison_depth.mp4` (0.7MB) | 결과 섹션 | **frame 968** (기둥이 PDD 고불확실성 구간). 입력(PDD tint)/GT/모델 3줄, baseline↔Ours 왕복 슬라이더(정지 구간에만 모델명 표시) |
| `comparison_pointcloud.mp4` (7.7MB) | 결과 섹션 | 같은 프레임 포인트 클라우드를 카메라 360° 궤도 이동하며 왕복 슬라이더 비교 |

생성 스크립트·프레임은 `~/websites/media_work/` (gen_pcd_sunny.py, gen_wipe.py — 파일 상단에
실행 커맨드 주석; gen_teaser.py·gen_seam.py는 폐기된 이전 버전). 프레임 재생성 후
`imageio_ffmpeg`의 ffmpeg로 인코딩 (커맨드는 memory/README 참고).
Sunny fine-tuned 예측 TIFF (4모델 300프레임 전부 보관):
`~/code/eval_models/pdf_omni/results/sunny/`(Ours), `~/code/eval_models/results/sunny/`(MDP·Romni),
`~/code/eval_models/omnimvs/results/sunny/`(OmniMVS+). 재현 검증: Ours-ft Sunny 지표 논문 Table 1
일치 (>1: 3.53/MAE 0.255), Romni-ft도 일치 (5.26/0.36).

## 남은 수정 항목 (index.html의 `TODO:` 주석 참고)

1. **저자/소속** — hero 섹션
2. **링크 버튼** — Paper / arXiv / Video / Code 의 `href="#"`
3. **BibTeX** — camera-ready 확정 후 저자 채우기
4. **시각자료 업그레이드(선택)** —
   - before/after 슬라이더(img-comparison-slider)·인터랙티브 3D 뷰어(Three.js) 추가
   - Figure들을 고품질 원본 이미지로 교체 (현재는 PDF에서 200 DPI 렌더링)

## 로컬 미리보기

```bash
cd ~/websites/pdf-omni-page
python3 -m http.server 8001
# 브라우저에서 http://localhost:8001 접속
```

## GitHub Pages 배포

개인 페이지(`<username>.github.io`)와 **별개의 저장소**로 만듭니다.
저장소 이름이 URL 경로가 됩니다 (예: `pdf-omni` → `https://<username>.github.io/pdf-omni/`).

```bash
cd ~/websites/pdf-omni-page
git init && git add -A
git commit -m "PDF-Omni project page"
git branch -M main
git remote add origin https://github.com/<username>/pdf-omni.git
git push -u origin main
```

그다음 GitHub 저장소의 **Settings → Pages → Source**에서 `main` 브랜치(`/ (root)`)를 선택하면
몇 분 뒤 `https://<username>.github.io/pdf-omni/` 에서 확인할 수 있습니다.

## 라이선스

Nerfies 템플릿은 CC BY-SA 4.0 라이선스이며, 푸터의 출처 표기를 유지해야 합니다.
