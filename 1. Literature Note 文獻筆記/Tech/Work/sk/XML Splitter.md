---
tags: 
date: 2023-10-17-週二
time: 10:45
---
```python
import os
from PIL import Image
import xml.etree.ElementTree as ET

# get xml file from input
xml_path = input("輸入xml檔案路徑:")

# image file name is same as xml file name
image_path = os.path.splitext(xml_path)[0] + '.png'

# make a dir that at the same folder of image_path, and name it as image_path without extension
dir_name = os.path.splitext(os.path.basename(image_path))[0]
print("dir_name: ", dir_name)
if not os.path.exists(dir_name):
    os.mkdir(dir_name)

# 打開XML文件並解析
tree = ET.parse(xml_path)
root = tree.getroot()

# 遍歷XML文件中的每個小圖像信息

for item in root.findall('SubTexture'):
    name   = item.get('name')
    x      = int(item.get('x'))
    y      = int(item.get('y'))
    width  = int(item.get('width'))
    height = int(item.get('height'))

    # 打開原始圖像文件
    image = Image.open(image_path)

    # 根據小圖像信息，切割圖像
    cropped_image = image.crop((x, y, x + width, y + height))

    # 保存小圖像為單獨的文件
    # cropped_image.save(f'{name}.png')
    # save image at the dir_name
    cropped_image.save(f'{dir_name}/{name}.png')

    print("完成: ", name)

# 完成任務
print('分割完成')

```