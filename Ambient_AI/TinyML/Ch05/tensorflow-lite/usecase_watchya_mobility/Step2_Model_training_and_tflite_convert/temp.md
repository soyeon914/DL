```python
!ls
%cd /content/gdrive/"My Drive"/data/

# 혹시 이전에 스크립트릴 실행했을 수 있으니, 다시 실행시키려면 그 전에 미리 잘 지워줍시다.
!rm -r helmetclassification 

# 경로들을 만들어 줍시다.
!mkdir helmetclassification
!mkdir helmetclassification/helmet
!mkdir helmetclassification/non_helmet

# 압축 해제!
!unzip helmet_crop.zip -d /content/gdrive/"My Drive"/data/helmetclassification/helmet
!unzip nonhelmet_crop.zip -d /content/gdrive/"My Drive"/data/helmetclassification/non_helmet
!unzip nonhelmet2.zip -d /content/gdrive/"My Drive"/data/helmetclassification/non_helmet

# 현재 디렉터리 이동
%cd /content/gdrive/"My Drive"/data/helmetclassification/

# /content/gdrive/"My Drive"/data/helmetclassification/ 에 train 과 test 폴더를 만들어 줍니다.
!mkdir train
!mkdir train/helmet
!mkdir train/non_helmet
!mkdir test
!mkdir test/helmet
!mkdir test/non_helmet

# /content/gdrive/"My Drive"/data/helmetclassification/helmet 경로부터 작업해 줍시다.
%cd /content/gdrive/"My Drive"/data/helmetclassification/helmet

helmet_data_directory = os.getcwd()
file_list = os.listdir(helmet_data_directory)
print('Count of file :', len(file_list))

import random
sampled_helmet_file_list = random.sample(file_list, int(len(file_list) * 0.4))
print('Count of sampled file :', len(sampled_helmet_file_list))

# 이제 sample 된 데이터를 /content/gdrive/"My Drive"/data/helmetclassification/test/helmet 으로 옮겨 줄 차례입니다.
import shutil
target_dir = os.path.join(os.path.join(data_dir, 'test'), 'helmet')
for f in sampled_helmet_file_list :
  current_file = os.path.join(helmet_data_directory, f)
  shutil.move(current_file, os.path.join(target_dir, f))
  # print(current_file,'\t->\t',os.path.join(target_dir, f))

# 이제 test 데이터를 모두 옮겼으니, train 데이터도 모두 옮겨 줍시다.
%cd /content/gdrive/"My Drive"/data/helmetclassification/
!mv helmet/ train/
!ls

# /content/gdrive/"My Drive"/data/helmetclassification/non_helmet 경로를 작업할 차례입니다.
%cd /content/gdrive/"My Drive"/data/helmetclassification/non_helmet

# 해당 경로는, 다양한 경로로부터 사람의 이미지를 취득했기에, 이를 모두 모아주는 작업이 필요합니다.
file_list = os.listdir(os.getcwd())
print(file_list)

# 내부에 MACOS 용 파일과 자잘한 더미 파일이 존재하니 이를 제거해 줍니다.
# 또한, pedestrian dataset 은 noise 가 있을 수 있기 때문에, 이를 모두 제거해야 합니다.
!rm -r __MACOSX
!rm -r pedestrian
!ls

%cd /content/gdrive/"My Drive"/data/helmetclassification/non_helmet

file_list = []
for (root, dirs, files) in os.walk(os.getcwd()):
  print("root : " + root)
  if len(files) > 0:
    for file_name in files:
      if file_name[-3:] in ['jpg', 'png'] :
        file_full_path = os.path.join(root, file_name)
        # print('append to file_list : ', file_full_path)
        file_list.append(file_full_path)


import random
sampled_nonhelmet_file_list = random.sample(file_list, int(len(file_list) * 0.4))
print('Count of sampled file :', len(sampled_nonhelmet_file_list), 'out of', len(file_list))

# 이제 sample 된 데이터를 /content/gdrive/"My Drive"/data/helmetclassification/test/helmet 으로 옮겨 줄 차례입니다.
import shutil
target_dir = os.path.join(os.path.join(data_dir, 'test'), 'non_helmet')
for cnt, f in enumerate(sampled_nonhelmet_file_list) :
  # 새로운 임시 이름 (cnt) + 확장자 (.xxx) 로 새로운 이름을 부여
  postfix = str(cnt) + f[-4:] 
  shutil.move(f, os.path.join(target_dir, postfix))
  # print('[test data]', f,'\t->\t',os.path.join(target_dir, postfix))

# test 데이터를 모두 옮겼으니, train 데이터도 모두 옮겨 줍시다.
cnt = 0
target_dir = os.path.join(os.path.join(data_dir, 'train'), 'non_helmet')
for f in file_list:
  if os.path.isfile(f):
    postfix = str(cnt) + f[-4:]
    shutil.move(f, os.path.join(target_dir, postfix))
    # print('[train data]', f,'\t->\t',os.path.join(target_dir, postfix))
    cnt += 1

# 원래 존재하던 폴더를 지워 버립시다.
%cd /content/gdrive/"My Drive"/data/helmetclassification/
!rm -r non_helmet
!ls


# 이미지의 size 를 재기 위해, PIL 을 import 합니다
from PIL import Image


%cd /content/gdrive/"My Drive"/data/helmetclassification/train/helmet/
file_list = os.listdir(os.getcwd())
remove_candidate_helmet_training_file_list = []
cnt = 0
for i, img_name in enumerate(file_list):
  print(i, '/', len(file_list))
  img = Image.open(img_name)
  if img.size[0] * img.size[1] < IMG_WIDTH * 0.4  * IMG_WIDTH * 0.4 : # 이미지의 해상도가 input 해상도의 일정 수준이라면. 
                                                                      # 0.4 로 잡은 이유는, nonhelmet data 의 개수와 비슷하게 맞추기 위함입니다.
    cnt+=1
    remove_candidate_helmet_training_file_list.append(img_name)
print("low resolution ratio : ", cnt, '/', len(file_list))

%cd /content/gdrive/"My Drive"/data/helmetclassification/test/helmet/
file_list = os.listdir(os.getcwd())
remove_candidate_helmet_testing_file_list = []
cnt = 0
for i, img_name in enumerate(file_list):
  print(i, '/', len(file_list))
  img = Image.open(img_name)
  if img.size[0] * img.size[1] < IMG_WIDTH * 0.4  * IMG_WIDTH * 0.4 :
    cnt+=1
    remove_candidate_helmet_testing_file_list.append(img_name)    
print("low resolution ratio : ", cnt, '/', len(file_list))


%cd /content/gdrive/"My Drive"/data/helmetclassification/train/non_helmet/
file_list = os.listdir(os.getcwd())
remove_candidate_nonhelmet_training_file_list = []
cnt = 0
for i, img_name in enumerate(file_list):
  print(i, '/', len(file_list))
  img = Image.open(img_name)
  if img.size[0] * img.size[1] < IMG_WIDTH * 0.4  * IMG_WIDTH * 0.4 : # 이미지의 해상도가 input 해상도의 일정 수준이라면. 
                                                                      # 0.4 로 잡은 이유는, nonhelmet data 의 개수와 비슷하게 맞추기 위함입니다.
    cnt+=1
    remove_candidate_nonhelmet_training_file_list.append(img_name)
print("low resolution ratio : ", cnt, '/', len(file_list))

%cd /content/gdrive/"My Drive"/data/helmetclassification/test/non_helmet/
file_list = os.listdir(os.getcwd())
remove_candidate_nonhelmet_testing_file_list = []
cnt = 0
for i, img_name in enumerate(file_list):
  print(i, '/', len(file_list))
  img = Image.open(img_name)
  if img.size[0] * img.size[1] < IMG_WIDTH * 0.4  * IMG_WIDTH * 0.4 :
    cnt+=1
    remove_candidate_nonhelmet_testing_file_list.append(img_name)    
print("low resolution ratio : ", cnt, '/', len(file_list))


import os
%cd /content/gdrive/"My Drive"/data/helmetclassification/train/helmet/
for img_name in remove_candidate_helmet_training_file_list :
  os.remove(img_name)

%cd /content/gdrive/"My Drive"/data/helmetclassification/test/helmet/
for img_name in remove_candidate_helmet_testing_file_list :
  os.remove(img_name)


%cd /content/gdrive/"My Drive"/data/helmetclassification/train/non_helmet/
for img_name in remove_candidate_nonhelmet_training_file_list :
  os.remove(img_name)

%cd /content/gdrive/"My Drive"/data/helmetclassification/test/non_helmet/
for img_name in remove_candidate_nonhelmet_testing_file_list :
  os.remove(img_name)
```

