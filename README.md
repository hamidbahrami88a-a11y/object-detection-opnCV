import cv2
from cvzone.FaceDetectionModule import FaceDetector

cap = cv2.VideoCapture(1)
cap.set(3, 640)
cap.set(4, 480)
if not cap.isOpened():
    print("دوربین شما باز نشد. لطفاً بررسی کنید.")
    exit()

detector = FaceDetector(minDetectionCon=0.5)

while True:
    success, img = cap.read()

    if not success:
        break

    img, bboxs = detector.findFaces(img, draw=True)
    
    cv2.imshow("Image", img)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
