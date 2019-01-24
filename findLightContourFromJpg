# -*-coding:utf-8 -*
import sys
reload(sys)
sys.setdefaultencoding('gbk')

import cv2
jpg_path = 'E:/1.jpg'
im1 = cv2.imread(jpg_path) #此图片用来最后画框显示以及提取品红色
im1 = cv2.resize(im1, (1440, 900))
# im2 = im1.copy()
img = cv2.imread(jpg_path, cv2.IMREAD_GRAYSCALE) #此灰度图片有来图片处理
img = cv2.resize(img, (1440, 900))
kernal = cv2.getStructuringElement(cv2.MORPH_RECT, (3, 3))
dilated = cv2.dilate(img, kernal)  # 膨胀
eroded = cv2.erode(img, kernal)  # 腐蚀
result = cv2.absdiff(dilated, eroded) #膨胀减去腐蚀，得到边

ret, frame = cv2.threshold(result,40,255,cv2.THRESH_BINARY)
result = cv2.bitwise_not(frame)
image, contours, hierarchy = cv2.findContours(frame, 1, 2)
j = 0
j_list = []
for counter in contours:
    # print(counter)
    for i in counter:
        # print i[0]
        x = i[0][0]
        y = i[0][1]
        # print(im2[y][x])
        if im1[y][x][0]>110 and im1[y][x][0]<170 and im1[y][x][2]>100 and im1[y][x][2]<160 and im1[y][x][1] <10:
            #判断这些边框是否被品红色所包围
            print(j)
            j_list.append(j)
        else:
            try:
                j_list.pop(j_list.index(j))
                #剔除掉并不是所有包含品红色的边框
            except:
                pass
    j+=1

contours = [contours[j] for j in j_list]
im = cv2.drawContours(im1, contours, -1, (0, 255, 0), 1)
cv2.imshow('img', im)
cv2.waitKey(0)
