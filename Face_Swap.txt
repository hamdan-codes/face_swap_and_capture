## Face Swapper and capturer
### Contributor : CHAUDHARY HAMDAN
###### All you need is once the camera window is opened after running the code, press space to capture the photo and 'q' to quit 


import cv2
import numpy as np
from datetime import datetime


cap = cv2.VideoCapture(0)
prvdt_string = ''

face_cascade = cv2.CascadeClassifier('Haarcascade/haarcascade_frontal_face_detection.xml')
while True:
    ret,frame = cap.read()
    if ret == False:
        continue
    faces = face_cascade.detectMultiScale(frame,1.3,5)
    
    for i in range(0,len(faces),2):
        x1,y1,w1,h1 = faces[i]
        try:
            x2,y2,w2,h2 = faces[i+1]
            face1 = frame[y1:y1+h1,x1:x1+w1]
            face2 = frame[y2:y2+h2,x2:x2+w2]

            face1 = cv2.resize(face1,(w2,h2))
            face2 = cv2.resize(face2,(w1,h1))

            frame[y1:y1+h1,x1:x1+w1] = face2
            frame[y2:y2+h2,x2:x2+w2] = face1
        except:
            pass
    cv2.imshow('Frame',frame)
    key_pressed = cv2.waitKey(1) & 0xff
    
    if key_pressed == ord(' '):
        dt_string = datetime.now().strftime("%d%m%Y_%H%M%S")
        if prvdt_string == dt_string:
            c += 1
        else:
            prvdt_string = dt_string
            c = 0
        ans_string = dt_string+'_'+str(c)
        cv2.imwrite(filename=f'Photos_Face_Swapper/Hamdan_s_OpenCV_{ans_string}.jpg', img=frame)
    
    if key_pressed == ord('q') or key_pressed == ord('Q'):
        break
cap.release()
cv2.destroyAllWindows()





