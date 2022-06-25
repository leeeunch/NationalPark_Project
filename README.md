# **딥러닝 기술을 이용한 유해동물 퇴치 알림  서비스**

이 서비스는 국립 공원 공단과 협업 프로젝트를 진행하여 만든 서비스입니다. 

1. 프로젝트 배경
![image](https://user-images.githubusercontent.com/86611917/175793065-b0c58bc6-4de2-4c05-a2ac-8139d738c12c.png)
위 기사는 농가의 야생동물 피해 관련 기사들입니다. 이 기사들에서 국립 공원에서 야생동물로 인한 피해가 극심하다는 것을 알게 되었습니다. 그 중 2021년 을주군에선 "6천만원"의 예산을 편성했고, 그 외에도 매해 유해 야생동물로 인한 피해액은 "120억여원"으로 매우 크다는 것을 알 수 있습니다.  

![image](https://user-images.githubusercontent.com/86611917/175792831-fd8545de-37ae-4722-bdf6-1c9e994cbd37.png)
위의 그래포는 환경부에서 얻어낸 동물별 농작물 피해보상액을 그래프로 시각화 한것입니다. 단위는 백만원으로 유해동물로 인한 피해의 대부분이 멧돼지와 고라니에 편향되어 있는 것을 발견했습니다.

이런 문제점을 해결한 사례가 있나 찾아보던 중, "이지워치"라는 서비스를 알게 되었습니다. "이지워치"는 현재 국립 공원 공단에서 실제로 사용 중이며 카메라 반경 안에 일정한 무게가 넘는 생물체가 움직이는 것이 확인되면 호랑이 울음소리를 냄으로서 야생동물을 내쫓는 시스템입니다.

하지만 "이지워치"에도 3가지 문제점이 있었습니다.
 첫 번째로 기계하나에 99만원으로 가격적으로 부담이 있었기 때문에 가격적인 측면을 줄이도록 했습니다. 
 두 번째로는 한가지 경고음만을 사용해 야생동물이 이에대해 학습해서 내성이 생길만한 여지가 있기 때문에 여러가지 경고음으로 내성이 생기지 않도록 했습니다. 
 세 번째는 이 프로젝트를 진행한 가장 큰 이유입니다. 국립공원공단 담당자님께 들은바로 25kg 이상의 열이나는 물체를 감지만 하면 호랑이 소리를 짖어내는 바람에 소리가 나오는 횟수가 너무 많아져 소음으로 인한 민원이 많이 생긴다고합니다. 저희는 이러한 소음문제를 해결하기위해 딥러닝을 이용하여 유해동물중 가장 많은 피해를 주는 “멧돼지와 고라니”를 인식하는 퇴치 서비스를 고안하게 되었습니다.
 
 ![image](https://user-images.githubusercontent.com/86611917/175793241-c6217fe1-9244-4ecc-b33c-7fb664d4a689.png)
 저희는 실시간 영상처리를 어떤 객체인식 시스템을 이용해야할지에 대한 고민을 하게되었습니다. 많은 객체인식 시스템이 있었지만 크게 메가디텍터와 욜로 두가지에대해 고민하게 되었습니다. 결론적으로 메가디텍터는 높은 정확도를 보장하지만 20초짜리 영상을 처리하는데 2분이 걸린다는 사실을 알게되었습니다. 그에반해 욜로의 경우 1분의 영상을 처리하는데 40초가 걸려 실시간 리얼 타임 객체인식에 문제가 없다는 것을 확인했습니다. 겹쳐진 사물의 구분이 힘듦다는 단점 또한 확인 할 수 있었습니다. 하지만 저희는 유해동물을 인식하는것에 중점이 있기때문에 사물구분이 안된다는 부분에선 단점이 되지 않는다 생각하였습니다. 그렇기 때문에 저희는 yolo 모델을 사용하게 되었습니다. 
 
 ![image](https://user-images.githubusercontent.com/86611917/175793255-ea6cdc62-7410-4255-98a2-90d0c9a198db.png)
 그중에서도 yolo모델의 다양한 종류중에 무엇을 사용할까에 대한 토의를 했습니다. 위 그래프는 바의 길이가 길수록 속도가 “느려지며” 정확도가 향상되는것을 나타냅니다. 저희는 실시간으로 유해동물을 발견하는것을 가장 중점으로 뒀기도 했고 yolo5s 모델이 어느정도 정확도를 보장한다는것을 확인해서 이 yolov5s 모델을 사용하개 되었습니다.
