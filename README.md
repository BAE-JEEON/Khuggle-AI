# KHUGGLE-AI-Competition
팀명: SURE

1. 파일 구성
	제출한 파일의 파일 구성은 아래와 같습니다.

	- 사용설명서: 구성한 코드의 전체 내용과 설명서가 담겨 있는 문서가 담긴 폴더입니다 

	- code : 각 개별 모델의 코드와 앙상블 하는데 사용한 코드가 담긴 폴더입니다. 
		- ESRGAN.ipynb (모델)
		- BSRGAN_epoch_40.ipynb (모델)
		- REAL_HAT_GAN.inpynb (모델)
		- MMSR_SRResNet.ipynb (모델)
		- BSR_GAN_+_realESRGAN_+_SwinIR_large.ipynb(모델)
		- Esemble.ipynb(앙상블)

	- weight: 학습을 시킨 모델의 경우 모델이 학습한 후의 weight, pretrain model의 경우 다운 받은 weight가 담긴 폴더입니다. weight가 없는 경우, ipynb 내부에서 다운 받을 수 있습니다. 

	- inference image: 각 개별 모델이 inference한 이미지가 담긴 폴더입니다. 해당 이미지를 앙상블에 사용하였습니다. 

2. 학습 방법
저희팀은 총 7개의 모델을 가중합 방식으로 앙상블 하는 방향으로 코드를 구성했으며 구체적인 모델의 내용은 아래와 같습니다.

1. ESR_GAN(Pretrain weight + fintuning 1 epochs)	#PSNR: 29.41
2. Real_ESR_GAN(Only using pretrain weight) #PSNR: 29.9675
3. Real_HAT_GAN(Only using pretrain weight) #PSNR: 30.15
4. Swin_IR_Large(Only using pretrain weight) #PSNR: 29.95
5. BSR_GAN(Only using pretrain weight) #PSNR: 29.90
6. BSR_GAN(Pretrain weight + fintuning 40 epochs) #PSNR: 29.98
7. MMSR_SRResNet(Only using pretrain weigh) #PSNR: 29.53


학습을 진행한 ESR_GAN과 BSR_GAN의 경우 아래와 같은 조건에서 학습했습니다.

ESR_GAN: 
	- batchSize : 64          
	- nEpochs : 1          
	- lr : 1e-4
	- Optimizer : Adam
	- Loss: MS-SSIM + L1
	- scheduler: none
	- DA: none

BSR_GAN:
	- batchSize : 4
	- nEpochs  : 40
	- lr : 1e-4
	- Optimizer: RAdam
	- Loss: MS-SSIM + L1 
	- scheduler: cosine annealing LR
	- DA: none

해당 모델들이 inference해서 생성한 이미지들을 차례 대로 아래와 같은 가중치로 가중합했습니다.

weight = [0.2,0.2,0.2,0.2,0.2/3,0.2/3,0.2/3]


3. 코드 실행

1) 먼저 아래의 모델 코드들을 각각 실행합니다.
      - ESRGAN.ipynb (모델)
      - BSRGAN_epoch_40.ipynb (모델)
      - REAL_HAT_GAN.inpynb (모델)
      - MMSR_SRResNet.ipynb (모델)
      - BSR_GAN_+_realESRGAN_+_SwinIR_large.ipynb(모델)

2) 위의 코드를 실행하여 얻은 inference 이미지를 통해서 아래의 코드를 실행하여 앙상블을 진행합니다.
inference 이미지들은 제출 폴더에 제공되었습니다.
앙상블을 진행할 시 이미지의 경로 폴더를 알맞게 수정하면 됩니다.
      - Esemble.ipynb(앙상블)



