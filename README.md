# face-recogination-management-system


import cv2
import numpy as np
import face_recognition
# WE ARE CONVERTING THE RGB IMAGE TO GRAYSCALE IMAGE ON WHICH ALGORITHM WORKS
imgIssac = face_recognition.load_image_file('Images/4.jpg')
imgIssac = cv2.cvtColor(imgIssac, cv2.COLOR_BGR2RGB)
imgTest = face_recognition.load_image_file('Images/4.jpg')
imgTest = cv2.cvtColor(imgTest, cv2.COLOR_BGR2RGB)
# WE ARE DETECTING THE FACE FROM THE IMAGE SO THAT WE COMPARE THE OTHER FACE
faceLoc = face_recognition.face_locations(imgIssac)[0]
encodeIssac = face_recognition.face_encodings(imgIssac)[0]
cv2.rectangle(imgIssac,(faceLoc[3],faceLoc[0]),(faceLoc[1],faceLoc[2]),(255,0
,255),2)
faceLocTest=face_recognition.face_locations(imgTest)[0]
encodeTest=face_recognition.face_encodings(imgTest)[0]
cv2.rectangle(imgTest,(faceLocTest[3],faceLocTest[0]),(faceLocTest[1],faceLoc
Test[2]),(255,0,255),2)
# WE ARE COMPARING BOTH THE FACE
results=face_recognition.compare_faces([encodeIssac],encodeTest)
# WE ARE CALCULATING HOW MUCH DIFFERENCE IN THE DIMENSION OF THE FACE
faceDis=face_recognition.face_distance([encodeIssac],encodeTest)
print(results,faceDis)
# SHOWING THE DIMENSION ON THE IMAGE
cv2.putText(imgTest,f'{results}{round(faceDis[0],2)}',(50,50),cv2.FONT_HERSHE
Y_COMPLEX,1,(0,0,255),2)
cv2.imshow('Issac Newton', imgIssac)
cv2.imshow('Issac Test', imgTest)
cv2.waitKey(0)
