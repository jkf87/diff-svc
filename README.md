# Diff-SVC
확산 모델을 통한 노래 음성 변환

## 업데이트:
2022.12.4 44.1kHz 보코더 오픈 애플리케이션, 공식적으로 44.1kHz 지원 제공 \.
2022.11.28 일부 네트워크를 최적화하고, 학습 속도를 개선하며, 모델 크기를 줄이고, 향후 새로운 학습 모델에 효과적 일 수있는 기본 no_fs2 옵션이 추가되었습니다.
2022.11.23 추론에 사용되는 원본 gt 오디오가 샘플 속도를 22.05kHz로 변경할 수있는 주요 버그 수정, 영향을 주셔서 죄송합니다. 테스트 오디오를 확인하고 업데이트 된 코드를 사용하십시오 \.
2022.11.22 추론 효과에 큰 영향을 미치는 몇 가지 버그를 포함하여 많은 버그가 수정되었습니다 \\.
2022.11.20 다른 소프트웨어로 수동 변환없이 추론을위한 대부분의 형식의 입력 및 저장 추가 \.
2022.11.13 중단 후 모델 읽기의 에포크 / 단계 표시 문제 수정, f0 처리의 디스크 캐시 추가, 실시간 사운드 변경 추론을위한 지원 파일 추가 \\.
2022.11.11 슬라이스 지속 시간 오류 수정, 44.1khz 적응 추가, contentvec\ 지원 추가.
2022.11.4 Merle 스펙트럼 저장 기능 추가\.
2022.11.2 새로운 보코더 코드 통합, 파셀마우스 알고리즘 업데이트\.
2022.10.29 추론 섹션 개편, 긴 오디오 자동 슬라이스 기능 추가 \\.
2022.10.28 휴버트의 onnx 인터페이스를 파이토치 인터페이스로 마이그레이션하고 인터페이스 로직을 깔끔하게 정리하였습니다. \
<font color=#FFA500>기존에 다운로드한 onnx hubert 모델을 다시 다운로드하여 pt 모델로 교체해야 하는 경우</font>, c구성은 변경할 필요가 없으며,  현재 1060 6G 비디오 메모리에 대해 직접 GPU 추론 및 전처리를 구현할 수 있으며 자세한 내용은 설명서를 참조하세요. 
2022.10.27 종속성 파일을 업데이트하여 중복 종속성을 제거합니다. \
2022.10.27 Hubert가 여전히 GPU 서버에서 CPU 추론을 사용하여 속도가 3~5배 느려지고 전처리 및 추론에 영향을 미치지만 훈련에는 영향을 미치지 않는 심각한 버그 수정 \.
2022.10.26 윈도우에서 데이터 전처리가 리눅스에서 작동하지 않는 문제 수정, 일부 문서 업데이트 \.
2022.10.25 추론/훈련에 대한 상세 문서 작성, 코드 일부 수정 및 통합, ogg 형식 오디오 지원 추가(wav와 구분할 필요 없이 바로 사용) \\.
2022.10.24 사용자 지정 데이터 세트에 대한 교육 지원 및 코드 간소화 \
2022.10.22 오픈팝 데이터 세트에 대한 교육 완료 및 리포지토리 생성

## Caution/Notes.
>본 프로젝트는 학술적 커뮤니케이션 목적으로 제작되었으며, 프로덕션 환경을 위한 것이 아니므로 본 프로젝트의 모델에서 생성된 사운드의 저작권 문제에 대해 책임을 지지 않습니다. \
본 리포지토리의 코드를 두 번 배포하거나 본 프로젝트로 제작한 결과물을 공개적으로 게시할 경우(동영상 웹사이트 기고 포함, 이에 국한되지 않음) 원저작자와 코드의 출처(본 리포지토리)를 반드시 명시해 주세요. \
다른 프로젝트에 본 프로젝트를 사용할 경우, 사전에 본 저장소의 작성자에게 연락하여 알려주시기 바랍니다. \이 프로젝트는 학술적 용도로 개설되었습니다.
>이 프로젝트는 학술적 교류를 목적으로 설립되었으며 프로덕션 환경을 위한 것이 아닙니다. 이 프로젝트의 모델에서 생성된 사운드로 인해 발생하는 문제.
이 저장소의 코드를 재배포하거나 이 프로젝트에서 생성된 결과물(동영상 웹사이트 제출을 포함하되 이에 국한되지 않음)을 공개적으로 게시하는 경우, 원저자와 소스 코드(이 저장소)를 표시해 주세요. \
이 프로젝트를 다른 계획에 사용할 경우, 사전에 이 리포지토리의 작성자에게 연락하여 알려주시기 바랍니다.

## 추론/inference.

>View. /inference.ipynb


## 전처리/preprocessing:
```
export PYTHONPATH=.
CUDA_VISIBLE_DEVICES=0 python preprocessing/binarize.py --config training/config.yaml
```
## training/training:
```
CUDA_VISIBLE_DEVICES=0 python run.py --config training/config.yaml --exp_name [사용자 프로젝트 이름] --reset
```
훈련 과정과 다양한 파라미터에 대한 자세한 설명은 [추론 및 훈련 노트](. /doc/train_and_inference.markdown)\를 참조하세요.
자세한 훈련 과정과 다양한 파라미터에 대한 소개는 [추론 및 훈련 지침](. /doc/training_and_inference_EN.markdown)을 참조하시기 바랍니다. 번역을 제공해 주신 @ρoem님께 감사드립니다.
### 훈련된 모델/trained models
>이 프로젝트는 수많은 데이터 세트에서 학습 및 테스트를 거쳤습니다. 추론 훈련에 필요한 일부 ckpt 파일, 데모 오디오 및 기타 파일은 아래 QQ 채널에서 다운로드할 수 있습니다(채널 번호: 5763z98e4m)\.
QQ를 사용하여이 QR 코드를 스캔하십시오 (가입 할 수없는 경우 적절한 네트워크 환경을 시도하십시오) :\.
이 프로젝트는 많은 데이터 세트에서 학습 및 테스트를 거쳤습니다. 추론 및 훈련에 필요한 ckpt 파일, 데모 오디오 및 기타 파일을 다운로드할 수 있습니다 QQ를 사용하여 이 QR 코드를 스캔하면 아래 QQ 채널에서 추론 및 훈련에 필요한 ckpt 파일, 데모 오디오 및 기타 파일을 다운로드할 수 있습니다(참여가 불가능한 경우 적합한 네트워크 환경을 시도해 보세요). \

<img src="./ckpt.png" width=256/>\
영어 지원을 받으려면 이 디스코드에 가입하세요: 

[![디스코드](https://img.shields.io/discord/1044927142900809739?color=%23738ADB&label=Discord&style=for-the-badge)](https://discord.gg/jvA5c2xzSE)

## 감사
>프로젝트 기반:[diffsinger](https://github.com/MoonInTheRiver/DiffSinger),[diffsinger(openvpi维护版)](https://github.com/openvpi/DiffSinger),[soft-vc](https://github.com/bshall/soft-vc)开发.\
동시에 개발 과정에서 도움을 주신 OpenVPI 개발자에게도 감사드립니다.
이 프로젝트는 [diffsinger](https://github.com/MoonInTheRiver/DiffSinger), [diffsinger (openvpi 유지보수 버전)](https://github.com/openvpi/DiffSinger), [soft-vc](https://github.com/bshall/soft-vc)를 기반으로 합니다. 또한 개발 및 교육 과정에서 도움을 주신 openvpi 회원 여러분께도 감사의 말씀을 드립니다. \
>注意：此项目与同名论文[DiffSVC](https://arxiv.org/abs/2105.13871)无任何联系，请勿混淆！\
참고: 이 프로젝트는 같은 이름의 논문 [DiffSVC](https://arxiv.org/abs/2105.13871)와 관련이 없으니 혼동하지 마세요!
