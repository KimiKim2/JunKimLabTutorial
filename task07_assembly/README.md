- 유전체 조립을 진행하기에 앞서, 우리가 다운 받은 데이터셋을 좀 더 가공합시다. 그냥 진행해도 되지만 데이터가 꽤 커서 바로 돌리면 프로그램 다 돌아가는 데 시간이 한참 걸릴 거예요. 염색체 3번에 해당하는 데이터를 먼저 뽑아봅시다. 염색체 3번에 해당할 거 같은 리드의 이름은 제가 준비해놨습니다. 다음 명령어를 입력해서 염색체 3번에 해당하는 리드 이름이 적힌 파일을 다운 받아 봅시다.
```console
(basicGenomics) 어쩌구@저쩌구:~/07_assembly$ wget https://raw.githubusercontent.com/JunKimCNU/JunKimLabTutorial/main/task07_assembly/chr3ReadName.txt
```
- (seqtk 활용) 이제 ```seqtk```와 이 ```chr3ReadName.txt``` 파일을 활용해서, ```ALT1.hifi.fq.gz``` 파일에 들어있는 데이터 중 염색체 3번의 리드만을 추출해봅시다. 아웃풋 파일 이름은 ```chr3Read.fq```로 지정하시면 됩니다. 참고로 이전 task에서는 안 다뤘던 커맨드 중 하나를 써서 진행하실 수 있습니다.
- (hifiasm 활용) 이제 이렇게 추출한 ```chr3Read.fq``` 파일을 활용해서 염색체 3번에 해당하는 리드를 조립해서 컨티그로 만들어봅시다. ```hifiasm``` 프로그램을 활용하면 됩니다. 터미널에 ```hifiasm```이라고만 치면 헬프 페이지가 뜨는데요, 이걸 잘 읽고 (1) 아웃풋 파일의 접두사(prefix)는 "chr3"로 지정합시다. (2) 활용할 thread 숫자도 지정해봅시다. 제 서버라면 3 정도를 추천 드리며, 이 정도라면 10분이면 유전체 조립이 끝납니다. (3) 마지막으로 purge-level을 0으로 지정해줍시다. 그 뒤 인풋 파일을 지정하고 ```hifiasm```을 돌리면 끝입니다. 각 옵션에 해당하는 걸 잘 입력해서 ```hifiasm``` 프로그램을 돌려봅시다.
- (awk 활용) 이렇게 돌리고 나면 [GFA 포맷](https://github.com/GFA-spec/GFA-spec)으로 지정된 아웃풋 파일들을 포함해 다양한 파일들이 생성될 겁니다. 이 [아웃풋 파일들에 대한 정보](https://hifiasm.readthedocs.io/en/latest/interpreting-output.html)를 한번 읽어보시고, 이중 우리가 원하는 3번 염색체 정보가 어떤 파일에 들어있을지 확인해봅시다. 그리고 [hifiasm 공식 홈페이지](https://github.com/chhylp123/hifiasm)에 나와있는 정보를 활용해, GFA 포맷으로 저장된 파일을 FASTA 파일로 바꿔봅시다.
- 이렇게 완성한 컨티그들에 관련된 다양한 통계치를 ```assembly-stats```, ```seqtk```, ```samtools``` 등을 활용해 살펴봅시다.
- 이렇게 하면 유전체 조립이 끝나는 겁니다. 쉽죠? 처음 돌릴 땐 버거울 수 있지만, 몇 번 하다 보면 나중에는 엔터 쳐서 끝내게 될 겁니다.
